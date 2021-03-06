---
title: REST API 및 템플릿을 사용 하 여 리소스 배포
description: Azure Resource Manager 및 리소스 관리자 REST API를 사용 하 여 Azure에 리소스를 배포 합니다. 리소스는 Resource Manager 템플릿에 정의됩니다.
ms.topic: conceptual
ms.date: 06/04/2019
ms.openlocfilehash: fc386f51073c256fd083a04bbed39316784827b1
ms.sourcegitcommit: 276c1c79b814ecc9d6c1997d92a93d07aed06b84
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2020
ms.locfileid: "76152513"
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>리소스 관리자 템플릿과 리소스 관리자 REST API로 리소스 배포

이 문서에서는 리소스 관리자 템플릿으로 리소스 관리자 REST API를 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.

요청 본문 또는 파일 링크에는 템플릿을 포함할 수 있습니다. 템플릿을 사용할 경우 템플릿은 로컬 파일이거나 URI를 통해 사용 가능한 외부 파일일 수 있습니다. 템플릿이 스토리지 계정에 있는 경우, 템플릿에 대한 액세스를 제한하고 배포 중에 SAS(공유 액세스 서명) 토큰을 제공할 수 있습니다.

## <a name="deployment-scope"></a>배포 범위

관리 그룹, Azure 구독 또는 리소스 그룹에 대 한 배포를 대상으로 지정할 수 있습니다. 대부분의 경우 리소스 그룹에 대 한 배포를 대상으로 합니다. 관리 그룹 또는 구독 배포를 사용 하 여 지정 된 범위에서 정책 및 역할 할당을 적용 합니다. 또한 구독 배포를 사용 하 여 리소스 그룹을 만들고 리소스를 배포 합니다. 배포의 범위에 따라 다른 명령을 사용 합니다.

**리소스 그룹**에 배포 하려면 [배포-만들기](/rest/api/resources/deployments/createorupdate)를 사용 합니다. 요청은 다음으로 전송 됩니다.

```HTTP
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Resources/deployments/{deploymentName}?api-version=2019-05-01
```

**구독**에 배포 하려면 [배포-구독 범위에서 만들기](/rest/api/resources/deployments/createorupdateatsubscriptionscope)를 사용 합니다. 요청은 다음으로 전송 됩니다.

```HTTP
PUT https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/{deploymentName}?api-version=2019-05-01
```

구독 수준 배포에 대 한 자세한 내용은 [구독 수준에서 리소스 그룹 및 리소스 만들기](deploy-to-subscription.md)를 참조 하세요.

**관리 그룹**에 배포 하려면 [배포-관리 그룹 범위에서 만들기](/rest/api/resources/deployments/createorupdateatmanagementgroupscope)를 사용 합니다. 요청은 다음으로 전송 됩니다.

```HTTP
PUT https://management.azure.com/providers/Microsoft.Management/managementGroups/{groupId}/providers/Microsoft.Resources/deployments/{deploymentName}?api-version=2019-05-01
```

관리 그룹 수준 배포에 대 한 자세한 내용은 [관리 그룹 수준에서 리소스 만들기](deploy-to-management-group.md)를 참조 하세요.

이 문서의 예제에서는 리소스 그룹 배포를 사용 합니다.

## <a name="deploy-with-the-rest-api"></a>REST API를 사용하여 배포

1. 인증 토큰을 포함하여 [공통 매개 변수 및 헤더](/rest/api/azure/)를 설정합니다.

1. 기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다. 솔루션에 필요한 구독 ID, 새 리소스 그룹 이름 및 위치를 제공합니다. 자세한 내용은 [리소스 그룹 만들기](/rest/api/resources/resourcegroups/createorupdate)를 참조하세요.

   ```HTTP
   PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2019-05-01
   ```

   다음과 같은 요청 본문을 사용합니다.

   ```json
   {
    "location": "West US",
    "tags": {
      "tagname1": "tagvalue1"
    }
   }
   ```

1. 배포를 실행하기 전에 [템플릿 배포 유효성 검사](/rest/api/resources/deployments/validate) 작업을 실행하여 배포 유효성을 검사합니다. 배포를 테스트할 때는 배포를 실행할 때처럼 정확하게 매개 변수를 제공합니다(다음 단계에 표시됨).

1. 템플릿을 배포 하려면 구독 ID, 리소스 그룹 이름, 요청 URI의 배포 이름을 제공 합니다.

   ```HTTP
   PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2019-05-01
   ```

   요청 본문에서 템플릿 및 매개 변수 파일에 대 한 링크를 제공 합니다. 매개 변수 파일에 대 한 자세한 내용은 [리소스 관리자 매개 변수 파일 만들기](parameter-files.md)를 참조 하세요.

   **mode**가 **Incremental**로 설정되어 있습니다. 전체 배포를 실행하려면 **mode**를 **Complete**로 설정합니다. 이 완전한 모드를 사용할 때는 템플릿에 없는 리소스를 실수로 삭제할 수 있으므로 주의해야 합니다.

   ```json
   {
    "properties": {
      "templateLink": {
        "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
        "contentVersion": "1.0.0.0"
      },
      "parametersLink": {
        "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
        "contentVersion": "1.0.0.0"
      },
      "mode": "Incremental"
    }
   }
   ```

    요청 콘텐츠와 응답 콘텐츠 중 하나 또는 둘 다를 기록하려면 요청에 **debugSetting** 을 포함합니다.

   ```json
   {
    "properties": {
      "templateLink": {
        "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
        "contentVersion": "1.0.0.0"
      },
      "parametersLink": {
        "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
        "contentVersion": "1.0.0.0"
      },
      "mode": "Incremental",
      "debugSetting": {
        "detailLevel": "requestContent, responseContent"
      }
    }
   }
   ```

    공유 액세스 서명(SAS) 토큰을 사용하여 스토리지 계정을 설정할 수 있습니다. 자세한 내용은 [공유 액세스 서명을 사용하여 액세스 위임](/rest/api/storageservices/delegating-access-with-a-shared-access-signature)을 참조하세요.

    매개 변수에 대해 중요한 값(예: 암호)을 제공해야 할 경우 해당 값을 주요 자격 증명 모음에 추가합니다. 앞의 예제에 표시된 대로 배포하는 동안 주요 자격 증명 모음을 검색합니다. 자세한 내용은 [배포 중 보안 값 전달](key-vault-parameter.md)을 참조하세요.

1. 템플릿 및 매개 변수의 파일에 연결하는 대신, 요청 본문에 포함할 수 있습니다. 다음 예제에서는 템플릿 및 매개 변수 인라인이 포함 된 요청 본문을 보여 줍니다.

   ```json
   {
      "properties": {
      "mode": "Incremental",
      "template": {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
          "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_LRS",
            "allowedValues": [
              "Standard_LRS",
              "Standard_GRS",
              "Standard_ZRS",
              "Premium_LRS"
            ],
            "metadata": {
              "description": "Storage Account type"
            }
          },
          "location": {
            "type": "string",
            "defaultValue": "[resourceGroup().location]",
            "metadata": {
              "description": "Location for all resources."
            }
          }
        },
        "variables": {
          "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
        },
        "resources": [
          {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2018-02-01",
            "name": "[variables('storageAccountName')]",
            "location": "[parameters('location')]",
            "sku": {
              "name": "[parameters('storageAccountType')]"
            },
            "kind": "StorageV2",
            "properties": {}
          }
        ],
        "outputs": {
          "storageAccountName": {
            "type": "string",
            "value": "[variables('storageAccountName')]"
          }
        }
      },
      "parameters": {
        "location": {
          "value": "eastus2"
        }
      }
    }
   }
   ```

1. 템플릿 배포의 상태를 가져오려면 [배포-get](/rest/api/resources/deployments/get)을 사용 합니다.

   ```HTTP
   GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2018-05-01
   ```

## <a name="next-steps"></a>다음 단계

- 오류가 발생할 때 성공적인 배포로 롤백하려면 [성공적인 배포에 대 한 오류 발생 시 롤백](rollback-on-error.md)을 참조 하세요.
- 리소스 그룹에 있지만 템플릿에 정의되지 않은 리소스를 처리하는 방법을 지정하려면 [Azure Resource Manager 배포 모드](deployment-modes.md)를 참조하세요.
- 비동기 REST 작업 처리에 대해 알아보려면 [Azure 비동기 작업 추적](../management/async-operations.md)을 참조하세요.
- 템플릿에 대 한 자세한 내용은 [Azure Resource Manager 템플릿의 구조 및 구문 이해](template-syntax.md)를 참조 하세요.

