---
title: Azure 가상 WAN에 대 한 글로벌 VNet 피어 링 구성 | Microsoft Docs
description: 다른 지역의 VNet을 가상 WAN 허브에 연결 합니다.
services: virtual-wan
author: cherylmc
ms.service: virtual-wan
ms.topic: conceptual
ms.date: 11/04/2019
ms.author: cherylmc
ms.openlocfilehash: 340472f84d2dd2c4f46d180992745a57e8ad1884
ms.sourcegitcommit: f4d8f4e48c49bd3bc15ee7e5a77bee3164a5ae1b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73588227"
---
# <a name="configure-global-vnet-peering-cross-region-vnet-for-virtual-wan"></a>가상 WAN에 대 한 글로벌 VNet 피어 링 (지역 간 VNet) 구성

다른 지역의 VNet을 가상 WAN 허브에 연결할 수 있습니다.

## <a name="before-you-begin"></a>시작하기 전에

다음 기준을 충족하는지 확인합니다.

* 지역 간 VNet (스포크)이 다른 가상 WAN 허브에 연결 되어 있지 않습니다. 스포크는 하나의 가상 허브에만 연결할 수 있습니다.
* VNet (스포크)에는 가상 네트워크 게이트웨이 (예: Azure VPN Gateway 또는 Express 경로 가상 네트워크 게이트웨이)가 포함 되어 있지 않습니다. VNet에 가상 네트워크 게이트웨이가 포함 된 경우 스포크 VNet을 허브에 연결 하기 전에 게이트웨이를 제거 해야 합니다.

## <a name="register"></a>이 기능 등록

PowerShell을 사용 하 여이 기능에 등록할 수 있습니다. 아래 예제에서 "시도"를 선택 하면 Azure Cloud Shell이 열립니다. PowerShell cmdlet을 컴퓨터에 로컬로 설치할 필요가 없습니다. 필요한 경우 ' AzSubscription-SubscriptionId <subid>' cmdlet을 사용 하 여 구독을 변경할 수 있습니다.

```azurepowershell-interactive
Register-AzProviderFeature -FeatureName AllowCortexGlobalVnetPeering -ProviderNamespace Microsoft.Network
Register-AzResourceProvider -ProviderNamespace 'Microsoft.Network'
```

## <a name="verify"></a>등록 확인

```azurepowershell-interactive
Get-AzProviderFeature -FeatureName AllowCortexGlobalVnetPeering -ProviderNamespace Microsoft.Network
```

## <a name="hub"></a>허브에 VNet 연결

이 단계에서는 허브와 지역 간 VNet 간에 피어 링 연결을 만듭니다. 연결하려는 각 VNet에 대해 이 단계를 반복합니다.

1. 가상 WAN에 대한 페이지에서 **가상 네트워크 연결**을 클릭합니다.
2. 가상 네트워크 연결 페이지에서 **+연결 추가**를 클릭합니다.
3. **연결 추가** 페이지에서 다음 필드를 채웁니다.

    * **연결 이름** - 연결의 이름을 지정합니다.
    * **허브** - 이 연결과 연결할 허브를 선택합니다.
    * **구독** - 구독을 확인합니다.
    * **가상 네트워크** - 이 허브에 연결할 가상 네트워크를 선택합니다. 가상 네트워크에는 기존의 가상 네트워크 게이트웨이를 사용할 수 없습니다.
4. **확인**을 클릭하여 피어링 연결을 만듭니다.

## <a name="next-steps"></a>다음 단계

가상 WAN에 대 한 자세한 내용은 [가상 Wan 개요](virtual-wan-about.md)를 참조 하세요.