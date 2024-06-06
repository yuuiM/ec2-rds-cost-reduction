# 毎日停止する

勉強環境など毎日停止して必要な時に作成するという環境に対して有効なCloudFormation

***対象***

- RDS
- EC2

## schedule-only-stop.yml

毎日21時に各サービスを停止する。
RDSは毎週起動するため、必要に応じて[stop_rds](../stop_rds/README.md)を行うこと。

***環境変数***

デフォルトで全てのRDSとEC2が対象となる。
対象外とする場合は環境変数に設定する。

|変数名|説明|
|--|--|
|ExcludeRdsClusterNameList|除外するRDSクラスター名を,で区切る|
|ExcludeEC2InstanceIdList|除外するEC2Instance名を,で区切る|
