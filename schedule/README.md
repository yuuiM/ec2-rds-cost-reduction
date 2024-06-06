# 業務時間中のみ環境動作させる

月から金の9時から21時まで環境を動かす

対象サービスは以下

- EC2(ECS含む)
- RDS

***止める手順***

1. schedule.yamlのcloudformationを削除
2. AutoScalingグループのオートスケーリングで予定されたアクションのstopを削除

***再開手順***

1. CloudFormationでshcedule.yamlを実行

## schedule.yaml

9時に起動するのとAutoScalingのスケジュールを設定するLambdaと
21時に停止するLambdaを作成する。

***環境変数***

デフォルトで全てのRDSとEC2が対象となる。
対象外とする場合は環境変数に設定する。

|変数名|説明|
|--|--|
|ExcludeRdsClusterNameList|除外するRDSクラスター名を,で区切る|
|ExcludeEC2InstanceIdList|除外するEC2Instance名を,で区切る  AutoScalingも除外対象となる|

---

## elasticip.yaml

AutoScalingはEC2をシャットダウンして起動するためElastic IPが解放されてしまう。

ElasticIPが設定されていないとアカウント設定でIPアドレス制御するとサービスが利用できなくなってしまう。

DeviceLinkとDeviceMonitoringで別々にスタック作成する。

***環境変数***

|変数名|説明|
|--|--|
|AutoScalingName|Auto Scalingグループのlogical-idを使用。　※AutoScalingGroupの名称ではない|
|EipAllocationId|EC2のElastic IPから該当のIPを開く。概要内の割り当てIDを使用。|
