---
title: 지도 스타일 기능 | Microsoft Azure 맵
description: 이 문서에서는 Microsoft Azure Maps 웹 SDK에서 제공 되는 스타일 관련 기능에 대해 알아봅니다.
author: walsehgal
ms.author: v-musehg
ms.date: 07/29/2019
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: b92e03c4e5346dd39eaba84cfeeedb93e418678c
ms.sourcegitcommit: f9601bbccddfccddb6f577d6febf7b2b12988911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75911790"
---
# <a name="choose-a-map-style-in-azure-maps"></a>Azure Maps에서 지도 스타일 선택

[Azure Maps에서 지원](./supported-map-styles.md) 되는 다양 한 지도 스타일은 웹 SDK에서 사용할 수 있습니다. 이 문서에서는 스타일 관련 기능을 사용하여 지도 로드 시 스타일을 설정하고, 새 스타일을 설정하고, 스타일 선택 컨트롤을 사용하는 방법을 보여 줍니다.

## <a name="set-style-on-map-load"></a>지도 로드 시 스타일 설정

다음 코드에서 맵의 `style` 옵션은 초기화할 때 `grayscale_dark`로 설정 됩니다.

<br/>

<iframe height='500' scrolling='no' title='지도 로드 시 스타일 설정' src='//codepen.io/azuremaps/embed/WKOQRq/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>에서 Azure Maps(<a href='https://codepen.io/azuremaps'>@azuremaps</a>)로 펜 <a href='https://codepen.io/azuremaps/pen/WKOQRq/'>지도 로드 시 스타일 설정</a>을 참조하세요.
</iframe>

## <a name="update-the-style"></a>스타일 업데이트

다음 코드에서 map 인스턴스가 로드 된 후 맵의 [system.windows.forms.control.setstyle](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) 함수를 사용 하 여 지도 스타일이 `road`에서 `satellite`로 업데이트 됩니다.

<br/>

<iframe height='500' scrolling='no' title='스타일 업데이트' src='//codepen.io/azuremaps/embed/yqXYzY/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>에서 Azure Maps(<a href='https://codepen.io/azuremaps'>@azuremaps</a>)로 펜 <a href='https://codepen.io/azuremaps/pen/yqXYzY/'>스타일 업데이트</a>를 참조하세요.
</iframe>

## <a name="add-the-style-picker"></a>스타일 선택 추가

다음 코드는 사용자가 다양 한 지도 스타일 사이를 쉽게 전환할 수 있도록 맵에 [StyleControl](/javascript/api/azure-maps-control/atlas.control.stylecontrol) 를 추가 합니다. 

<br/>

<iframe height='500' scrolling='no' title='스타일 선택 추가' src='//codepen.io/azuremaps/embed/OwgyvG/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>에서 Azure Maps(<a href='https://codepen.io/azuremaps'>@azuremaps</a>)로 펜 <a href='https://codepen.io/azuremaps/pen/OwgyvG/'>스타일 선택 추가</a>를 참조하세요.
</iframe>

> [!TIP]
> 기본적으로 스타일 선택 컨트롤은 기본적으로 Azure Maps의 S0 가격 책정 계층을 사용할 때 사용할 수 있는 모든 스타일을 나열 합니다. 이 목록에 있는 스타일의 수를 줄이려면 목록에 표시할 스타일의 배열을 스타일 선택기의 `mapStyle` 옵션으로 전달 합니다. S1을 사용 중이 고 사용 가능한 모든 스타일을 표시 하려면 스타일 선택기의 `mapStyles` 옵션을 `"all"`로 설정 합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서 사용된 클래스 및 메서드에 대해 자세히 알아려보면 다음 항목을 참조하세요.

> [!div class="nextstepaction"]
> [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)

지도에 컨트롤을 추가 합니다.

> [!div class="nextstepaction"]
> [맵 컨트롤 추가](map-add-controls.md)

> [!div class="nextstepaction"]
> [핀 추가](map-add-pin.md)
