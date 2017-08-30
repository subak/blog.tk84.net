# Grafana の Alerting を Gmail で通知する

`Grafana` にはアラートの機能があります。  
`Prometheus` にも `Alertmanager` がありますが、アラートも `Grafana` で設定した方が簡単便利です。

## Configファイルを編集する

メールの設定はConfigファイルで行います。  
デフォルトのコンフィグファイルは `$WORKING_DIR/conf/defaults.ini` にあります。[^1]  
`deb` または `rpm` パッケージでインストールした場合は `/etc/grafana/grafana.ini` です。

### smtp セクション

`[smtp]` セクションを次のように設定します。

```conf:grafana.ini

[smtp]
enabled = true
host = smtp.gmail.com:587
user = example@gmail.com
password = changeme
skip_verify = false
from_address = example@gmail.com
from_name = Grafana
```

- `user`,`password`,`from_address`は書き換えてください。
- `user` はメールアドレスです。


[^1]: [Config file locations](http://docs.grafana.org/installation/configuration/#config-file-locations)






