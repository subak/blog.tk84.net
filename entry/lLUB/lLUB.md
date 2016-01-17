# brew cask でインストールに失敗する

久しぶりにbrew caskでGUIアプリをインストールしようとしたら失敗した。  
調べて解決するまでのメモ。

## こんなエラーが出てインストールできない！

```sh-session
$ brew cask install xmind
Error: Cask 'xmind' definition is invalid: Bad header line: parse failed
```

## ググったら次のコマンドを実行するといいよとのこと

```sh-session
$ brew update; brew cleanup; brew cask cleanup
$ brew uninstall --force brew-cask; brew update
```

## 何事もなかったようにインストールに成功！

```sh-session
$ brew cask install xmind
==> Satisfying dependencies
complete
==> Downloading http://www.xmind.net/xmind/downloads/xmind7-macosx-3.6.0.R-201511090408.dmg
######################################################################## 100.0%
==> Verifying checksum for Cask xmind
==> Symlinking App 'XMind.app' to '/Users/subak/Applications/XMind.app'
🍺  xmind staged at '/opt/homebrew-cask/Caskroom/xmind/3.6.0.R-201511090408' (3067 files, 301M)
```

## 参考
- https://github.com/caskroom/homebrew-cask/issues/15930#issuecomment-165844907
