---
title: Azure Monitor의 메트릭 경고에 대해 지원되는 리소스
description: Azure Monitor의 메트릭 경고에 대한 지원 메트릭 및 로그 참조
author: harelbr
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 12/17/2019
ms.author: harelbr
ms.subservice: alerts
ms.openlocfilehash: 14dc7b33a82b490f005d9684e4c9cb76bd947a7c
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75364495"
---
# <a name="supported-resources-for-metric-alerts-in-azure-monitor"></a>Azure Monitor의 메트릭 경고에 대해 지원되는 리소스

이제 Azure Monitor는 기존의 [클래식 메트릭 경고](../../azure-monitor/platform/alerts-classic.overview.md)에 비해 상당한 장점이 있는 [새 메트릭 경고 형식](../../azure-monitor/platform/alerts-overview.md)을 지원합니다. [다양한 Azure 서비스](../../azure-monitor/platform/metrics-supported.md)에 대해 메트릭을 사용할 수 있습니다. 최신 경고에서 지원하는 리소스 종류가 점점 증가하고 있습니다. 이 문서에서는 이러한 하위 집합이 나열되어 있습니다.

메트릭으로 추출 된 Log Analytics 작업 영역에 저장 된 인기 있는 로그 데이터에 대 한 최신 메트릭 경고를 사용할 수도 있습니다. 자세한 내용은 [로그에 대한 메트릭 경고](../../azure-monitor/platform/alerts-metric-logs.md)를 확인하세요.

## <a name="portal-powershell-cli-rest-support"></a>포털, PowerShell, CLI, REST 지원
현재는 Azure Portal, [REST API](https://docs.microsoft.com/rest/api/monitor/metricalerts/) 또는 [Resource Manager 템플릿](../../azure-monitor/platform/alerts-metric-create-templates.md)에서만 최신 메트릭 경고를 만들 수 있습니다. PowerShell 및 Azure CLI 버전 2.0 이상을 사용한 최신 경고 구성 지원이 곧 제공될 예정입니다.

## <a name="metrics-and-dimensions-supported"></a>지원되는 메트릭 및 차원
최신 메트릭 경고는 차원을 사용하는 메트릭에 대한 경고를 지원합니다. 차원을 사용하여 메트릭을 적절한 수준으로 필터링할 수 있습니다. 해당 차원과 함께 지원되는 모든 메트릭을 [Azure Monitor - 메트릭 탐색기](../../azure-monitor/platform/metrics-charts.md)에서 탐색하고 시각화할 수 있습니다.

최신 경고에서 지원하는 Azure Monitor 메트릭 원본의 전체 목록은 다음과 같습니다.

|리소스 유형  |지원되는 차원 |다중 리소스 경고| 사용 가능한 메트릭|
|---------|---------|-----|----------|
|Microsoft.ApiManagement/service | 예| 아닙니다. | [API Management](../../azure-monitor/platform/metrics-supported.md#microsoftapimanagementservice)|
|Microsoft AppPlatform/스프링 |아닙니다.| 예|
|Microsoft.Automation/automationAccounts | 예| 아닙니다. | [Automation 계정](../../azure-monitor/platform/metrics-supported.md#microsoftautomationautomationaccounts)|
|Microsoft.Batch/batchAccounts | N/A| 아닙니다. | [Batch 계정](../../azure-monitor/platform/metrics-supported.md#microsoftbatchbatchaccounts)|
|Microsoft.Cache/Redis|예| 아닙니다. |[Azure Cache for Redis](../../azure-monitor/platform/metrics-supported.md#microsoftcacheredis)|
|ClassicStorage/storageAccounts/mmxclassic|아닙니다.|예|
|ClassicStorage/storageAccounts/mmxclassic/blobServices|아닙니다.|예|
|ClassicStorage/storageAccounts/mmxclassic/fileServices|아닙니다.|예|
|ClassicStorage/storageAccounts/mmxclassic/queueServices|아닙니다.|예|
|ClassicStorage/storageAccounts/mmxclassic/tableServices|아닙니다.|예| |
|Microsoft.CognitiveServices/accounts| N/A | 아닙니다. | [Cognitive Services](../../azure-monitor/platform/metrics-supported.md#microsoftcognitiveservicesaccounts)|
|Microsoft.Compute/virtualMachines |예 | 예 | [Virtual Machines](../../azure-monitor/platform/metrics-supported.md#microsoftcomputevirtualmachines)|
|Microsoft.Compute/virtualMachineScaleSets |N/A | 예 |[가상 머신 확장 집합](../../azure-monitor/platform/metrics-supported.md#microsoftcomputevirtualmachinescalesets)|
|Microsoft.ContainerInstance/containerGroups | 예| 아닙니다. | [컨테이너 그룹](../../azure-monitor/platform/metrics-supported.md#microsoftcontainerinstancecontainergroups)|
|Microsoft.ContainerService/managedClusters | 예 | 아닙니다. | [관리되는 클러스터](../../azure-monitor/platform/metrics-supported.md#microsoftcontainerservicemanagedclusters)|
|Microsoft.DataBoxEdge/dataBoxEdgeDevices | 예 | 예 | |
|Microsoft.DataFactory/datafactories| 예| 아닙니다. | [데이터 팩터리 V1](../../azure-monitor/platform/metrics-supported.md#microsoftdatafactorydatafactories)|
|Microsoft.DataFactory/factories |예 | 아닙니다. |[데이터 팩터리 V2](../../azure-monitor/platform/metrics-supported.md#microsoftdatafactoryfactories)|
|DataShare/계정 |아닙니다.| 예|
|Microsoft.DBforMySQL/servers |N/A| 아닙니다. |[MySQL용 DB](../../azure-monitor/platform/metrics-supported.md#microsoftdbformysqlservers)|
|Microsoft.DBforPostgreSQL/servers |N/A | 아닙니다. | [PostgreSQL용 DB](../../azure-monitor/platform/metrics-supported.md#microsoftdbforpostgresqlservers)|
|Microsoft.Devices/IotHubs | N/A | 아닙니다. |[IoT Hub 메트릭](../../azure-monitor/platform/metrics-supported.md#microsoftdevicesiothubs)|
|Microsoft.Devices/provisioningServices| 예 | 아닙니다. |[DPS 메트릭](../../azure-monitor/platform/metrics-supported.md#microsoftdevicesprovisioningservices)|
|Microsoft.EventGrid/domains|아닙니다.|예| |
|Microsoft.EventGrid/topics |예 | 아닙니다. |[Event Grid 항목](../../azure-monitor/platform/metrics-supported.md#microsofteventgridtopics)|
|Microsoft.EventHub/clusters |예| 아닙니다. |[Event Hubs 클러스터](../../azure-monitor/platform/metrics-supported.md#microsofteventhubclusters)|
|Microsoft.EventHub/namespaces |예| 아닙니다. |[Event Hubs](../../azure-monitor/platform/metrics-supported.md#microsofteventhubnamespaces)|
|Microsoft.KeyVault/vaults| 아닙니다. |아닙니다. |[자격 증명 모음](../../azure-monitor/platform/metrics-supported.md#microsoftkeyvaultvaults)|
|Microsoft.Logic/workflows |N/A | 아닙니다. |[Logic Apps](../../azure-monitor/platform/metrics-supported.md#microsoftlogicworkflows) |
|Microsoft.MachineLearningServices/workspaces|예| 아닙니다. | [Machine Learning](../../azure-monitor/platform/metrics-supported.md#microsoftmachinelearningservicesworkspaces) |
|Microsoft.Network/applicationGateways|N/A| 아닙니다. |  |
|Microsoft.Network/dnsZones | N/A| 아닙니다. | [DNS 영역](../../azure-monitor/platform/metrics-supported.md#microsoftnetworkdnszones) |
|Microsoft.Network/expressRouteCircuits | N/A | 아닙니다. |[ExpressRoute 회로](../../azure-monitor/platform/metrics-supported.md#microsoftnetworkexpressroutecircuits) |
|Microsoft.Network/loadBalancers (표준 SKU 전용)| 예| 아닙니다. | [부하 분산 장치](../../azure-monitor/platform/metrics-supported.md#microsoftnetworkloadbalancers) |
|Microsoft. Network/natGateways|아닙니다.|예|
|Microsoft. Network/privateEndpoints|아닙니다.|예|
|Microsoft. Network/privateLinkServices|아닙니다.|예|
|Microsoft.Network/publicipaddresses |N/A | 아닙니다. |[공용 IP 주소](../../azure-monitor/platform/metrics-supported.md#microsoftnetworkpublicipaddresses)|
|Microsoft.Network/trafficManagerProfiles | 예 | 아닙니다. | [Traffic Manager 프로필](../../azure-monitor/platform/metrics-supported.md#microsoftnetworktrafficmanagerprofiles) |
|Microsoft.OperationalInsights/workspaces| 예 | 아닙니다. | [Log Analytics 작업 영역](../../azure-monitor/platform/metrics-supported.md#microsoftoperationalinsightsworkspaces)|
|Microsoft.Relay/namespaces | 예 | 아닙니다. | [중계](../../azure-monitor/platform/metrics-supported.md#microsoftrelaynamespaces)|
|Microsoft 피어 링/peeringServices|아닙니다.|예|
|Microsoft.PowerBIDedicated/capacities | N/A | 아닙니다. | [Capacities](../../azure-monitor/platform/metrics-supported.md#microsoftpowerbidedicatedcapacities)|
|Microsoft.Search/searchServices |N/A|아닙니다. | [Search 서비스](../../azure-monitor/platform/metrics-supported.md#microsoftsearchsearchservices)|
|Microsoft.ServiceBus/namespaces |예| 아닙니다. |[Service Bus](../../azure-monitor/platform/metrics-supported.md#microsoftservicebusnamespaces)|
|Microsoft.Sql/servers/elasticPools |   아닙니다. | 예 |
|Microsoft.Sql/servers/databases    | 아닙니다. | 예 |
|Microsoft.Storage/storageAccounts |예 | 아닙니다. | [Storage 계정](../../azure-monitor/platform/metrics-supported.md#microsoftstoragestorageaccounts)|
|Microsoft.Storage/storageAccounts/services | 예| 아닙니다. | [Blob 서비스](../../azure-monitor/platform/metrics-supported.md#microsoftstoragestorageaccountsblobservices), [파일 서비스](../../azure-monitor/platform/metrics-supported.md#microsoftstoragestorageaccountsfileservices), [큐 서비스](../../azure-monitor/platform/metrics-supported.md#microsoftstoragestorageaccountsqueueservices) 및 [테이블 서비스](../../azure-monitor/platform/metrics-supported.md#microsoftstoragestorageaccountstableservices)|
|Microsoft.StreamAnalytics/streamingjobs |N/A| 아닙니다. | [Stream Analytics](../../azure-monitor/platform/metrics-supported.md#microsoftstreamanalyticsstreamingjobs)|
|VMWareCloudSimple/virtualMachines |예|아닙니다. |[CloudSimple Virtual Machines](../../azure-monitor/platform/metrics-supported.md#microsoftvmwarecloudsimplevirtualmachines)|
|Microsoft.Web/serverfarms | 예 | 아닙니다. | [App Service 계획](../../azure-monitor/platform/metrics-supported.md#microsoftwebserverfarms)|
|Microsoft.Web/sites | 예 | 아닙니다. | [App Services](../../azure-monitor/platform/metrics-supported.md#microsoftwebsites-excluding-functions) 및 [Functions](../../azure-monitor/platform/metrics-supported.md#microsoftwebsites-functions)|
|Microsoft.Web/sites/slots | 예 | 아닙니다. | [App Service 슬롯](../../azure-monitor/platform/metrics-supported.md#microsoftwebsitesslots)|

## <a name="payload-schema"></a>페이로드 스키마

> [!NOTE]
> 웹 후크 통합을 위해 Azure Monitor의 모든 경고 서비스에서 확장 가능 하 고 통합 된 단일 경고 페이로드를 사용 하는 이점을 제공 하는 [일반적인 경고 스키마](https://aka.ms/commonAlertSchemaDocs)를 사용할 수도 있습니다. [일반적인 경고 스키마 정의에 대해 알아봅니다.](https://aka.ms/commonAlertSchemaDefinitions)


POST 작업에는 적절히 구성된 [작업 그룹](../../azure-monitor/platform/action-groups.md)이 사용될 때 모든 최신 메트릭 경고에 대해 다음과 같은 JSON 페이로드와 스키마가 포함됩니다.

```json
{
  "schemaId": "AzureMonitorMetricAlert",
  "data": {
    "version": "2.0",
    "status": "Activated",
    "context": {
      "timestamp": "2018-02-28T10:44:10.1714014Z",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/microsoft.insights/metricAlerts/StorageCheck",
      "name": "StorageCheck",
      "description": "",
      "conditionType": "SingleResourceMultipleMetricCriteria",
      "severity":"3",
      "condition": {
        "windowSize": "PT5M",
        "allOf": [
          {
            "metricName": "Transactions",
            "metricNamespace":"microsoft.storage/storageAccounts",
            "dimensions": [
              {
                "name": "AccountResourceId",
                "value": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
              },
              {
                "name": "GeoType",
                "value": "Primary"
              }
            ],
            "operator": "GreaterThan",
            "threshold": "0",
            "timeAggregation": "PT5M",
            "metricValue": 1
          }
        ]
      },
      "subscriptionId": "00000000-0000-0000-0000-000000000000",
      "resourceGroupName": "Contoso",
      "resourceName": "diag500",
      "resourceType": "Microsoft.Storage/storageAccounts",
      "resourceId": "/subscriptions/1e3ff1c0-771a-4119-a03b-be82a51e232d/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500",
      "portalLink": "https://portal.azure.com/#resource//subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
    },
    "properties": {
      "key1": "value1",
      "key2": "value2"
    }
  }
}
```

## <a name="next-steps"></a>다음 단계

* 새 [경고 환경](../../azure-monitor/platform/alerts-overview.md)에 대해 자세히 알아봅니다.
* [Azure의 로그 경고](../../azure-monitor/platform/alerts-unified-log.md)에 대해 알아봅니다.
* [Azure의 경고](../../azure-monitor/platform/alerts-overview.md)에 대해 알아봅니다.
