# Preparation
## CF CLIのインストール
https://network.pivotal.io/products/elastic-runtime/
```bash
## ローカライズしたい場合は
 cf config --locale ja-JP
```

## Login & setup
ログイン
```bash
cf login -a api.run.pivotal.io -u shashitani@pivotal.io -o hashi-org -s development
```
CF 基本コマンド
```bash
cf help
cf plugins
cf orgs
```
CF Space
```
cf spaces
cf delete-space test
cf create-space dev
cf create-space prod
cf target
cf target -s dev
cf target
cf target -s prod

```
- PWSに戻って作成したSpaceを確認

## Pal-Tracker
https://s3.amazonaws.com/pal-operator-jars/releases/pal-tracker.jar
```
cf push pal-tracker -p pal-tracker.jar --random-route
## -- Fail --
cf logs pal-tracker --recent
cf set-env pal-tracker WELCOME_MESSAGE "Hello from PCF"
```
稼動確認
pal-tracker-chipper-hedgehog.cfapps.io
```
cf restage pal-tracker
cf set-env pal-tracker WELCOME_MESSAGE "PCFからこんにちは"
cf restage pal-tracker
```
Spaceの状態を確認する
```
cf apps
cf routes
cf events pal-tracker
```

## スケーリング
```
cf app pal-tracker
cf scale pal-tracker -m 512M -f
## -- Fail --
cf scale pal-tracker -m 768M -f
cf scale pal-tracker -i 2
## アプリを削除
cf delete pal-tracker
```

## Spring Music
https://github.com/cloudfoundry-samples/spring-music
```bash
## cloing the repo
git clone https://github.com/cloudfoundry-samples/spring-music.git
cd spring-music
## Switching JDK to 8
export JAVA_HOME=`/usr/libexec/java_home -v 1.8`
PATH=${JAVA_HOME}/bin:${PATH}
## build
./gradlew clean assemble
cf target
cf push
```
