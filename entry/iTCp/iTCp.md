# [Docker] Swarmモード利用時に one-off でタスクを実行して不要なイメージを削除する

Swarmモードではサービスを作成してタスクを実行します。
サービスは自動的に再起動されます。
サービス作成（デプロイ）時に一度だけタスクを実行したかったので色々試してうまくいった方法を残しておきます。

## Docker Stack Deploy と composeファイル

Docker 1.13 から複数のDockerイメージで構成されるサービスをまとめて複数のコンテナに対してデプロイできる [^1] ようになりました。


```bash
docker stack deploy --with-registry-auth -c production.yml production
```

`production` という名前の `stack` を作成しています。
`stack` を作成すると指定されたcomposeファイルの内容にしたがって `service` も作成されます。


```yml:docker-compose.yml
version: "3"

services:
  rmi:
    image: docker:17.03.2-ce
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    environment:
      KEEP_NUM: 5
    entrypoint: |
      ash -c '
        set -eux
        images=$$(docker image ls -f "label=com.example.name=target" -q | tail -n +$$(($${KEEP_NUM}+1)))
        [ -n "$${images}" ] && docker image rm -f $${images}
        docker container prune -f
      '
    deploy:
      mode: global
      restart_policy:
        condition: none

networks:
  backend:
    driver: "overlay"
```

- `version` を __3__ にします。
- 直近にpullしたイメージは削除せずに保持します。[^2]
    - 環境変数 `$KEEP_NUM` が保持するイメージ数です。
- `restart_policy` を `condition: none` にします。
    - サービスは稼働し続けることを前提としているためデフォルトでは正常終了時も自動で再起動されます。
- 削除するイメージをラベルでフィルタリング[^3]します。
    - イメージ作成時にラベル付けしておきます。
- `mode: global` にして Swarmクラスターの各ノードに一つタスクを割り当てます。

## サービスを削除する

`restart_policy` を `none` にすると `docker service update --force ${service}` のようにサービスを更新してもタスクは再実行されません。
一旦サービスを削除し、再度 deploy してサービスを作り直すとタスクが実行されます。

```bash
docker service rm production_rmi
docker stack deploy --with-registry-auth -c production.yml production
```


[^1]: [Docker 1.13正式版登場。複数Dockerイメージをまとめてデプロイする「Docker Stack Deploy」、使われていないイメージを削除する「Docker System Prune」など新機能](http://www.publickey1.jp/blog/17/docker_113dockerdocker_stack_deploydocker_system_prune.html)

[^2]: Swarmモードには作成したサービスをロールバックする機能がありますが直近のイメージを削除してしまうとロールバックできなくなります。

[^3]: https://docs.docker.com/engine/reference/commandline/images/#filtering