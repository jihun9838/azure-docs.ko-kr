---
title: Azure 가용성 영역이란?
description: Azure에서 가용성과 복원력이 높은 애플리케이션을 만들려면 가용성 영역에서 리소스를 실행하는 데 사용할 수 있는 별도의 실제 위치를 제공합니다.
author: cynthn
ms.service: azure
ms.topic: article
ms.date: 10/17/2019
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 4b1af742182d9c953846e723b6d48809818565b6
ms.sourcegitcommit: 5397b08426da7f05d8aa2e5f465b71b97a75550b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2020
ms.locfileid: "76271297"
---
# <a name="what-are-availability-zones-in-azure"></a>Azure에서 가용성 영역이란?
가용성 영역은 데이터 센터 오류에서 애플리케이션 및 데이터를 보호하는 고가용성 기능입니다. 가용성 영역은 Azure 지역 내의 고유한 물리적 위치입니다. 각 영역은 독립된 전원, 냉각 및 네트워킹을 갖춘 하나 이상의 데이터 센터로 구성됩니다. 복원력을 보장하려면 활성화된 모든 지역에서 최소한 세 개의 별도 영역이 필요합니다. 지역 내에서 가용성 영역의 물리적 구분은 애플리케이션 및 데이터를 데이터 센터 오류로부터 보호할 수 있습니다. 영역 중복 서비스는 단일 지점 오류에서 보호하기 위해 가용성 영역에서 애플리케이션 및 데이터를 복제합니다. Azure는 가용성 영역을 통해 업계 최고의 99.99% VM 작동 시간 SLA를 제공합니다. 전체 [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)는 Azure의 보장된 가용성에 대해 전반적으로 설명합니다.

Azure 지역의 가용성 영역은 장애 도메인과 업데이트 도메인의 조합입니다. 예를 들어 Azure 지역의 3개 영역에 VM을 3개 이상 만들면 장애 도메인 3개와 업데이트 도메인 3개에 VM이 효과적으로 분산됩니다. Azure 플랫폼은 업데이트 도메인에 분산된 VM을 인식하여 다른 영역에 있는 VM이 동시에 업데이트되지 않게 합니다.

영역 내에서 컴퓨팅, 스토리지, 네트워킹 및 데이터 리소스를 공동 배치하고 다른 영역에 복제하여 애플리케이션 아키텍처에 고가용성을 빌드합니다. 가용성 영역을 지원하는 Azure 서비스는 다음의 두 범주로 나뉩니다.

- 영역 **서비스** – 특정 영역 (예: 가상 머신, 관리 디스크, 표준 IP 주소)에 리소스를 고정 합니다.
- **영역 중복 서비스** – 플랫폼이 영역에서 자동으로 복제됩니다(예를 들어, 영역 중복 스토리지, SQL Database).

Azure에서 포괄적인 비즈니스 연속성을 구현하려면 Azure 지역 쌍과 가용성 영역의 조합을 사용하여 애플리케이션 아키텍처를 빌드하십시오. 고가용성에 대한 Azure 지역 내의 가용성 영역을 사용하여 애플리케이션 및 데이터를 동기적으로 복제하고 재해 복구 보호에 대한 Azure 지역에서 비동기적으로 복제할 수 있습니다.
 
![지역에서 차례로 한 영역의 개념 보기](./media/az-overview/az-graphic-two.png)

> [!IMPORTANT]
> 가용성 영역 식별자 (위 그림의 숫자 1, 2, 3)는 논리적으로 각 구독의 실제 실제 영역에 독립적으로 매핑됩니다. 즉, 지정 된 구독의 가용성 영역 1 다른 구독의 가용성 영역 1와 다른 실제 영역을 참조할 수 있습니다. 결과적으로 가상 머신 배치에 대해 다른 구독에서 가용성 영역 Id를 사용 하지 않는 것이 좋습니다.

## <a name="services-support-by-region"></a>지역별 서비스 지원

가용성 영역를 지 원하는 Azure 서비스와 지역의 조합은 다음과 같습니다.


|                                 |아메리카 |              |           |           | 유럽 |              |          |              | 아시아 태평양 |                 |
|----------------------------|----------|----------|---------|---------|--------------|------------|--------|----------|----------|-------------|
|          |미국 중부|미국 동부|미국 동부 2|미국 서부 2|프랑스 중부|북유럽|영국 남부|서유럽|일본 동부|동남아시아|
| **컴퓨팅**                         |            |              |           |           |                |              |          |             |            |                |
| Linux Virtual Machines          | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| Windows Virtual Machines        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| Virtual Machine Scale Sets      | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| Azure Kubernetes Service        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| **스토리지**   |            |              |           |           |                |              |          |             |            |                |
| Managed Disks                   | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| 영역 중복 저장소          | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| **네트워킹**                     |            |              |           |           |                |              |          |             |            |                |
| 표준 IP 주소        | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| 표준 Load Balancer     | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;   | &#10003;       |
| VPN Gateway            | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       |
| ExpressRoute 게이트웨이   | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       |
| Application Gateway (V2)    | &#10003;   |  &#10003;    | &#10003;  | &#10003;  | &#10003;       | &#10003;     |  &#10003;  | &#10003;    |  &#10003;   | &#10003;       |
| Azure Firewall           | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    |  &#10003;       | &#10003;       |
| **데이터베이스**                     |            |              |           |           |                |              |          |             |            |                |
| Azure Data Explorer                   | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;        | &#10003;       |
| SQL Database                    | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    | &#10003;모드      | &#10003;       |
| Azure Cache for Redis           | &#10003;   | &#10003;     | &#10003;  | &#10003;  | &#10003;       | &#10003;     | &#10003; | &#10003;    |  &#10003;       | &#10003;       |
| Azure Cosmos DB                    | &#10003;   |  &#10003;  |  &#10003; | &#10003; |       |     | &#10003; |  &#10003;   |            | &#10003;       |
| **분석**                       |            |              |           |           |                |              |          |             |            |                |
| Event Hubs                      | &#10003;   |   &#10003; | &#10003;  | &#10003;  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;       |
| **통합**                     |            |              |           |           |                |              |          |             |            |                |
| Service Bus(프리미엄 계층만 해당) | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |
| Event Grid | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |
| **ID**                     |            |              |           |           |                |              |          |             |            |                |
| Azure AD Domain Service | &#10003;   |  &#10003;  | &#10003;  | &#10003;  | &#10003;  | &#10003;     |&#10003;   | &#10003;    |&#10003;      | &#10003;       |

## <a name="services-resiliency"></a>서비스 복원 력
모든 Azure 관리 서비스는 지역 수준 오류에서 탄력적으로 대처할 수 있도록 설계 되었습니다. 오류가 발생 하는 경우 지역 내에서 하나 이상의 가용성 영역 오류는 전체 지역 오류와 비교 하 여 더 작은 오류 반지름이 있습니다. Azure는 지역 내에서 또는 다른 Azure 지역에서 관리 서비스의 영역 수준 오류 로부터 복구할 수 있습니다. Azure는 지역 내에서 한 번에 한 영역 내에서 중요 한 유지 관리를 수행 하 여 지역 내에서 가용성 영역에 배포 된 고객 리소스에 영향을 주는 오류를 방지 합니다.

## <a name="pricing"></a>가격 책정
가용성 영역에 배포된 가상 머신에 대한 추가 비용은 없습니다. Azure 지역 내에서 두 개 이상의 가용성 영역에 두 개 이상의 VM을 배포하면 VM 작동 시간 SLA 99.99%가 제공됩니다. 내부 가용성 영역 VM 대 VM 데이터 전송 요금이 추가됩니다. 자세한 내용은 [대역폭 가격 책정](https://azure.microsoft.com/pricing/details/bandwidth/) 페이지를 검토하세요.


## <a name="get-started-with-availability-zones"></a>가용성 영역 시작하기
- [가상 머신 만들기](../virtual-machines/windows/create-portal-availability-zone.md)
- [PowerShell을 사용하여 Managed Disk 추가](../virtual-machines/windows/attach-disk-ps.md#add-an-empty-data-disk-to-a-virtual-machine)
- [영역 중복 가상 머신 확장 집합 만들기](../virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones.md)
- [영역 중복 프런트엔드를 통해 표준 Load Balancer를 사용하여 영역에서 VM 부하 분산](../load-balancer/load-balancer-standard-public-zone-redundant-cli.md)
- [영역 중복 프런트엔드를 통해 표준 Load Balancer를 사용하여 영역 내에 VM 부하 분산](../load-balancer/load-balancer-standard-public-zonal-cli.md)
- [영역 중복 스토리지](../storage/common/storage-redundancy-zrs.md)
- [SQL 데이터베이스](../sql-database/sql-database-high-availability.md#zone-redundant-configuration)
- [Event Hubs 지리적 재해 복구](../event-hubs/event-hubs-geo-dr.md#availability-zones)
- [Service Bus 지리적 재해 복구](../service-bus-messaging/service-bus-geo-dr.md#availability-zones)
- [영역 중복 가상 네트워크 게이트웨이 만들기](../vpn-gateway/create-zone-redundant-vnet-gateway.md)
- [Azure Cosmos DB에 대 한 영역 중복 영역 추가](../cosmos-db/high-availability.md#availability-zone-support)
- [Redis 가용성 영역에 대 한 Azure 캐시 시작](https://aka.ms/redis/az/getstarted)
- [Azure Active Directory Domain Services 인스턴스 만들기](../active-directory-domain-services/tutorial-create-instance.md)
- [가용성 영역를 사용 하는 AKS (Azure Kubernetes Service) 클러스터 만들기](../aks/availability-zones.md)

## <a name="next-steps"></a>다음 단계
- [빠른 시작 템플릿](https://aka.ms/azqs)
