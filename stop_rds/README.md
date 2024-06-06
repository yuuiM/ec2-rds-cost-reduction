## stop_rds.yaml

### 目的

AWS RDS Auroraのクラスターを稼働料金が高く、また、節約のために停止したとしてもAWSの仕様上7日後に自動で起動してしまうので、
自動起動後すぐに停止させる仕組みをcloudFormationで構築する。

### 使い方

stop_rds.yamlを使用しcloudFormationスタックを作成
作成時、RdsClusterNameListパラメータには停止したいクラスターの識別子を指定する。
複数のクラスターの識別子を指定したい場合は","区切りで指定可能。

### 仕様

このcloudFormationスタックにより、
対象のクラスターの停止を試みるlambdaがaws eventBridgeにより毎時0分に実行されるようになる。
これにより、クラスターが自動起動しても1時間後までには再度停止されようになる。

### lambdaの実行を止めたい場合

aws eventBridgeの、stop-rds-StopRDSScheduleEvent-***というルールを無効化すれば
毎時0分に対象のクラスターの停止を試みるlambdaは実行されなくなる。
あるいはこのcloudformationスタックを削除してもよい。
