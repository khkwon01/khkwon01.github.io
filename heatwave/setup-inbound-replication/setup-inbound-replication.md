# MySQL HeatWave Inbound Replication 설정

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## 세션 소개

Inbound replication는 MySQL HeatWave Service에서 구성된 복제 채널을 사용하여 다른 위치에서 DB 시스템으로 트랜잭션을 복사합니다. 채널은 source(MySQL 인스턴스 또는 다른 DB 시스템)를 replica(Heatwave DB 시스템)에 연결하고 source에서 replica으로 데이터를 복사합니다.

자세한 내용은 OCI 문서를 참조하세요:
[MySQL HeatWave Inbound Replication](https://docs.oracle.com/en-us/iaas/mysql-database/doc/inbound-replication.html).

_Estimated Time:_ 20 minutes 소요

### 목표

이 Lab에서는 다음 작업을 안내해 드립니다:

- Replication Channel 생성
- Channel Enable or Disable
- Channel 재가동 (Resume)
- Channel Reset
- Channel 변경

### Prerequisites (필수사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험


## 작업 1: Replication Channel 생성

inbound replication의 경우 복제 채널은 source(MySQL 인스턴스나 다른 DB 시스템)를 replica(Heatwave DB 시스템)에 연결하고, source에서 replica으로 데이터를 복사합니다.

replication channel 생성하기 위해 Console를 사용하세요:

아래 링크로 이동하여 **Creating a Replication Channel Using the Console** 지침을 따르세요.

[Creating a Replication Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/creating-replication-channel.html#GUID-3C42FF94-3DEE-409C-B8A3-467890AA7FE3)

## 작업 2: Channel Enable or Disable

비활성 상태인 복제 채널(replication channel)을 활성화하면 오류가 없으면 source에서 복제가 시작됩니다. 복제 채널을 비활성화하면 복제가 중지되고 채널이 비활성 상태로 전환됩니다.

replication channel 생성하기 위해 Console를 사용하세요.

아래 링크로 이동하여 **Enabling or Disabling a Channel** 지침을 따르세요:

[Enabling or Disabling a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## 작업 3: Channel 재가동 (Resume)

inbound replication 채널이 주의 필요 상태(Needs Attention)인 경우 오류를 수정한 다음 채널을 재개하여 복제를 다시 시작합니다. 채널 페이지의 세부 정보 열은 복제 채널에 주의(needs attention)가 필요한 이유를 설명합니다.

Needs Attention 상태는 DB 시스템이 INACTIVE 상태이기 때문에 표시될 수도 있습니다. 이 경우 DB 시스템이 활성화될 때까지 복제를 다시 시작할 수 없습니다.

replication channel 생성하기 위해 Console를 사용하세요.

아래 링크로 이동하여 **Resuming a Channel** 지침을 따르세요:

[Resuming a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## 작업 4: Channel Reset

inbound replication 채널을 재설정하면 채널 구성을 제외한 채널의 모든 데이터가 제거됩니다. RESET REPLICA ALL FOR CHANNEL과 동일합니다. 복구할 수 없는 문제가 있는 경우 재설정 작업은 복제와 관련된 레코드를 지워 채널이 깨끗하게 시작될 수 있도록 합니다.

Target DB system은 source binary log에서 해당 위치를 삭제하고, 복제 메타데이터 저장소를 지우고, relay log 파일을 삭제하고, new relay log 파일을 시작합니다.

replication channel 생성하기 위해 Console를 사용하세요.

아래 링크로 이동하여 **Resuming a Channel** 지침을 따르세요.:

[Resuming a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## 작업 5: Channel 변경

채널 이름, 설명, 소스 연결 세부 정보와 같은 구성 항목을 생성한 후 변경해야 하는 경우 inbound replication 채널을 편집합니다.

replication channel 생성하기 위해 Console를 사용하세요.

아래 링크로 이동하여 **Editing a Channel** 지침을 따르세요:

[Editing a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)


이제 **다음 Lab으로 진행**할 수 있습니다.

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, July 2024
