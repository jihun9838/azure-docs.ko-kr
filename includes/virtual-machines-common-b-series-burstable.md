---
title: 포함 파일
description: 포함 파일
services: virtual-machines
author: ayshakeen
ms.service: virtual-machines
ms.topic: include
ms.date: 06/25/2019
ms.author: azcspmt;ayshak;cynthn
ms.custom: include file
ms.openlocfilehash: 17c9ea33f4706053ccde5e99686887aab7a823b6
ms.sourcegitcommit: b5106424cd7531c7084a4ac6657c4d67a05f7068
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75942742"
---
B 시리즈 VM 제품군을 사용하면 워크로드에 필요한 기준 수준 성능을 제공하는 VM 크기를 선택할 수 있으며, Intel® Broadwell E5-2673 v4 2.3GHz 또는 Intel® Haswell 2.4GHz E5-2673 v3 프로세서 vCPU의 CPU 성능을 최대 100%까지 버스트할 수 있습니다.

B 시리즈 VM은 웹 서버, 개념 증명, 소규모 데이터베이스 및 개발 및 빌드 환경과 같이 CPU의 전체 성능이 지속적으로 필요하지 않은 작업에 적합합니다. 이러한 작업에는 일반적으로 버스트 가능한 성능 요구 사항이 있습니다. B 시리즈는 기준 성능을 갖춘 VM 크기를 구입할 수 있는 기능을 제공하며, 기준 성능보다 적게 사용할 경우 VM 인스턴스에서 크레딧을 적립합니다. VM에 대한 크레딧이 적립되면 애플리케이션에 더 높은 CPU 성능이 필요할 때 VM이 vCPU의 최대 100%까지 사용하여 기준 이상으로 버스트할 수 있습니다.

B 시리즈는 다음과 같은 VM 크기를 제공 합니다.

| 크기             | vCPU  | 메모리: GiB | 임시 스토리지(SSD) GiB | VM의 CPU 기준 성능 | VM의 CPU 최대 성능 | 초기 크레딧 | 크레딧 획득/시간 | 최대 획득 크레딧 | 최대 데이터 디스크 수 | 최대 캐시 및 임시 저장소 처리량: IOPS/MBps | 최대 캐시되지 않은 디스크 처리량: IOPS/MBps | 최대 NIC 수 |          
|---------------|-------------|----------------|----------------------------|-----------------------|--------------------|--------------------|--------------------|----------------|----------------------------------------|-------------------------------------------|-------------------------------------------|----------|
| Standard_B1ls<sup>1</sup>  | 1           | 0.5              | 4                          | 5%                   | 100%                   | 30                   | 3                  | 72            | 2                                      | 200/10                                  | 160 / 10                                  | 2  |
| Standard_B1s  | 1           | 1              | 4                          | 10%                   | 100%                   | 30                   | 6                  | 144            | 2                        | 400 / 10                                  | 320 / 10                                  | 2  |
| Standard_B1ms | 1           | 2              | 4                          | 20%                   | 100%                   | 30                   | 12                 | 288           | 2                         | 800 / 10                                  | 640 / 10                                  | 2  |
| Standard_B2s  | 2           | 4              | 8                          | 40%                   | 200%                   | 60                   | 24                 | 576            | 4                                      | 1600 / 15                                 | 1280 / 15                                 | 3  |
| Standard_B2ms | 2           | 8              | 16                         | 60%                   | 200%                   | 60                   | 36                 | 864            | 4                                      | 2400 / 22.5                               | 1920 / 22.5                               | 3  |
| Standard_B4ms | 4           | 16             | 32                         | 90%                   | 400%                   | 120                   | 54                 | 1296           | 8                                      | 3600 / 35                                 | 2880 / 35                                 | 4  |
| Standard_B8ms | 8           | 32             | 64                         | 135%                  | 800%                   | 240                   | 81                 | 1944           | 16                                     | 4320/50                                 | 4320/50                                 | 4  |
| Standard_B12ms | 12           | 48             | 96                         | 202%                  | 1200%                   | 360                   | 121                 | 2909           | 16                                     | 6480/75                                 | 4320/50                                  | 6  |
| Standard_B16ms | 16           | 64             | 128                         | 270%                  | 1600%                   | 480                   | 162                 | 3888           | 32                                     | 8640 / 100                                 | 4320/50                                 | 8  |
| Standard_B20ms | 20           | 80             | 160                         | 337%                  | 2000%                   | 600                   | 203                 | 4860           | 32                                     | 10800/125                                 | 4320/50                                 | 8  |

<sup>1</sup> B1ls는 Linux 에서만 지원 됩니다.

## <a name="workload-example"></a>워크 로드 예제

Office 체크 인/아웃 응용 프로그램을 고려 합니다. 응용 프로그램에는 업무 시간 동안 CPU 급증이 필요 하지만, 업무 시간 외에는 컴퓨팅 전력이 많지 않습니다. 이 예제에서 작업은 효율적으로 작동 하려면 64GiB RAM이 있는 16vCPU 가상 머신이 필요 합니다.

다음 표에서는 매시간 트래픽 데이터를 보여 주고 차트는 해당 트래픽의 시각적 표현입니다.

B16 특징:

최대 CPU 성능: 16vCPU * 100% = 1600%

기준선: 270%

![시간별 트래픽 데이터 차트](./media/virtual-machines-common-b-series-burstable/office-workload.png)

| 시나리오 | 시간 | CPU 사용량 (%) | 누적 크레딧<sup>1</sup> | 크레딧을 사용할 수 있음 |
| --- | --- | --- | --- | --- |
| B16ms 배포 | 배포 | 배포  | 480 (초기 크레딧) | 480 |
| 트래픽 없음 | 0:00 | 0 | 162 | 642 |
| 트래픽 없음 | 1:00 | 0 | 162 | 804 |
| 트래픽 없음 | 2:00 | 0 | 162 | 966 |
| 트래픽 없음 | 3:00 | 0 | 162 | 1128 |
| 트래픽 없음 | 4:00 | 0 | 162 | 1290 |
| 트래픽 없음 | 5:00 | 0 | 162 | 1452 |
| 낮은 트래픽 | 6:00 | 270 | 0 | 1452 |
| 직원에 게 office가 제공 됩니다 (앱에는 80% vCPU가 필요 함). | 7:00 | 1280 | -606 | 846 |
| 직원이 계속 사무실에 제공 됩니다 (앱에는 80% vCPU가 필요 함). | 8:00 | 1280 | -606 | 240 |
| 낮은 트래픽 | 9:00 | 270 | 0 | 240 |
| 낮은 트래픽 | 10:00 | 100 | 102 | 342 |
| 낮은 트래픽 | 11:00 | 50 | 132 | 474 |
| 낮은 트래픽 | 12:00 | 100 | 102 | 576 |
| 낮은 트래픽 | 13:00 | 100 | 102 | 678 |
| 낮은 트래픽 | 14:00 | 50 | 132 | 810 |
| 낮은 트래픽 | 15:00 | 100 | 102 | 912 |
| 낮은 트래픽 | 16:00 | 100 | 102 | 1014 |
| 직원 체크 아웃 (앱 요구 100% vCPU) | 17:00 | 1600 | -798 | 216 |
| 낮은 트래픽 | 18:00 | 270 | 0 | 216 |
| 낮은 트래픽 | 19:00 | 270 | 0 | 216 |
| 낮은 트래픽 | 20:00 | 50 | 132 | 348 |
| 낮은 트래픽 | 21:00 | 50 | 132 | 480 |
| 트래픽 없음 | 22:00 | 0 | 162 | 642 |
| 트래픽 없음 | 23:00 | 0 | 162 | 804 |

<sup>1</sup> 시간 내에 사용 된 크레딧을 축적 하는 것은 `((Base CPU perf of VM - CPU Usage) / 100) * 60 minutes`입니다.  

16 개의 vCPUs 및 64 GiB의 메모리를 포함 하는 D16s_v3의 경우 시간당 요금은 시간당 $0.936 (월간 $673.92)이 고, 16 개의 vCPUs 및 64 GiB memory가 있는 B16ms (월별 $0.794)입니다. <b>그러면 15% 절감 효과가 발생 합니다.</b>

## <a name="q--a"></a>질문과 답변

### <a name="q-how-do-you-get-135-baseline-performance-from-a-vm"></a>Q: VM에서 135% 기준 성능을 얻으려면 어떻게 할까요?
**A**: 135%는 VM 크기를 구성하는 8개 vCPU에서 공유됩니다. 예를 들어 애플리케이션에서 일괄 처리를 수행하는 8개 코어 중 4개를 사용하고 해당 4개 vCPU에서 30% 사용률에서 실행하는 경우 총 VM CPU 성능은 120%가 됩니다.  즉 VM이 기준 성능에서 15% 델타에 따라 크레딧 시간을 적립한다는 것을 의미합니다.  그러나 동일한 VM에서 8개 vCPU를 모두 100% 사용하여 해당 VM에 최대 800% CPU 성능을 제공하는 크레딧을 사용할 수 있음도 의미합니다.


### <a name="q-how-can-i-monitor-my-credit-balance-and-consumption"></a>Q: 크레딧 잔액과 소비량을 모니터링하려면 어떻게 할까요?
**A**: 다음 주에 2 개의 새 메트릭을 도입 하 고, **크레딧** 메트릭은 vm에서 얼마나 많은 크레딧을 볼 수 있도록 하 고, **ConsumedCredit** 메트릭은 vm이 은행에서 사용한 CPU 크레딧 수를 표시 합니다.    포털의 메트릭 창에서 또는 Azure Monitor API를 통한 프로그래밍 방식으로 이러한 메트릭을 볼 수 있습니다.

Azure에 대한 메트릭 데이터에 액세스하는 방법에 대한 자세한 내용은 [Microsoft Azure의 메트릭 개요](../articles/monitoring-and-diagnostics/monitoring-overview-metrics.md)를 참조하세요.

### <a name="q-how-are-credits-accumulated"></a>Q: 크레딧은 어떻게 적립될까요?
**A**: 정확히 기준 성능 수준에서 실행되는 VM이 버스팅 크레딧의 순 적립 또는 소비가 적용되지 않도록 VM 적립 및 소비 속도가 설정됩니다.  VM이 기준 성능 수준 이하로 실행될 때마다 크레딧이 순 증가하고, VM이 기준 성능 수준보다 더 많은 CPU를 활용할 때마다 크레딧이 순 감소합니다.

**예제**: 내가 사용하는 적은 시간과 출석 데이터베이스 애플리케이션에 대해 B1ms 크기를 사용하여 VM을 배포합니다. 이 크기에 따라 애플리케이션에서 vCPU의 최대 20%를 기준으로 사용할 수 있으며, 사용하거나 적립할 수 있는 분당 크레딧은 0.2입니다. 

내 애플리케이션은 직원들의 작업일 중 업무 시작과 종료에 해당하는 오전 7-9시와 오후 4-6시 사이에 바쁘게 사용됩니다. 다른 20시간 동안에는 일반적으로 유휴 상태이며 vCPU의 10%만 사용합니다. 최대 사용 시간이 아닌 경우 분당 0.2 크레딧을 적립하지만 분당 0.1 크레딧만 사용하므로 VM은 시간당 0.1 x 60 = 6 크레딧을 적립합니다.  최대 사용 시간이 아닌 20시간 동안 나는 120 크레딧을 적립하게 됩니다.  

최대 사용 시간 동안에는 내 애플리케이션에서 평균 60%의 vCPU 사용률을 유지하지만 분당 0.2 크레딧을 적립하는 한편 분당 0.6 크레딧을 소비하므로 분당 0.4 크레딧 또는 시간당 0.4 x 60 = 24 크레딧의 순 비용이 발생합니다. 1일 최대 사용 시간이 4시간이므로 최대 사용량에 대해 4 x 24 = 96 크레딧이 필요합니다.

최대 사용 시간이 아닌 동안에 적립된 120 크레딧에서 최대 사용 시간 동안에 소비된 96 크레딧을 빼면, 하루 24 크레딧이 추가로 적립되어 다른 작업을 버스트하는 데 사용할 수 있습니다.

### <a name="q-how-can-i-calculate-credits-accumulated-and-used"></a>Q: 축적 된 크레딧을 계산 하 고 사용 하려면 어떻게 해야 하나요?
**A**: 다음 수식을 사용할 수 있습니다. 

(VM의 기본 CPU 성능-CPU 사용량)/100 = 크레딧 뱅크 또는 분당 사용

위의 인스턴스에서 기준은 20%이 고 CPU의 10%를 사용 하는 경우 100%-10%/100 = 0.1 크레딧을 사용 합니다.

### <a name="q-does-the-b-series-support-premium-storage-data-disks"></a>Q: B 시리즈에서 Premium Storage 데이터 디스크를 지원하나요?
**A**: 예, B 시리즈 크기는 모두 Premium Storage 데이터 디스크를 지원합니다.   
    
### <a name="q-why-is-my-remaining-credit-set-to-0-after-a-redeploy-or-a-stopstart"></a>Q: redepoy 또는 중지/시작 후에 남은 크레딧이 0으로 설정되는 이유는 무엇인가요?
**A** : VM이 "REDPLOYED" 상태이고 VM이 다른 노드로 이동한 경우 누적된 크레딧은 손실됩니다. VM이 중지/시작했지만 동일한 노드에 남아 있는 경우 VM은 누적된 크레딧을 유지합니다. VM이 노드에서 새로 시작할 때마다 초기 크레딧을 가져오는데 Standard_B8ms의 경우 240분입니다.
    
### <a name="q-what-happens-if-i-deploy-an-unsupported-os-image-on-b1ls"></a>Q: B1ls에 지원 되지 않는 OS 이미지를 배포 하면 어떻게 되나요?
**A** : B1ls는 Linux 이미지만 지원 하 고 다른 OS 이미지를 배포 하는 경우 고객 환경을 최대한 활용 하지 못할 수 있습니다.

### <a name="q-what-happens-if-i-run-out-of-credits"></a>Q: 크레딧이 소진 되 면 어떻게 되나요?
**A** : VM이 사용 가능한 크레딧을 모두 소비 하는 경우에는 기준 CPU만 사용 하 고 해당 기준 위에 버스트를 수행할 수 없습니다. 
