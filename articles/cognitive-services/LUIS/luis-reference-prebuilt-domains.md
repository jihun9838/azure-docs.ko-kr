---
title: 미리 빌드된 도메인 참조-LUIS
titleSuffix: Azure Cognitive Services
description: LUIS(Language Understanding Intelligent Services)에서 미리 작성된 의도 및 엔터티 컬렉션에 해당하는 미리 작성된 도메인에 대한 참조입니다.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 09/27/2019
ms.author: diberry
ms.openlocfilehash: 17d72ad51974bb0fb741ae19ebb19f313e646c62
ms.sourcegitcommit: 5f0f1accf4b03629fcb5a371d9355a99d54c5a7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71677645"
---
# <a name="prebuilt-domain-reference-for-your-luis-app"></a>LUIS 앱에 대한 미리 작성된 도메인 참조
이 참조는 LUIS에서 제공하는 의도 및 엔터티의 미리 작성된 컬렉션에 해당하는 [미리 작성된 도메인](luis-how-to-use-prebuilt-domains.md)에 대한 정보를 제공합니다.

반대로, [사용자 지정 도메인](luis-how-to-start-new-app.md)은 의도 및 모델 없이 시작합니다. 사용자 지정 모델에 미리 작성된 도메인 의도 및 엔터티를 추가할 수 있습니다.

## <a name="custom-domains-per-language"></a>언어별 사용자 지정 도메인

아래 표에는 현재 지원 되는 도메인이 요약 되어 있습니다. 영어 지원은 일반적으로 다른 항목 보다 더 완전 합니다. 

| 엔터티 형식       | EN-US      | ZH-CN-CN   | DE    | FR     | ES    | IT      | PT-BR |  JP  |      KO |        NL |    TR |
|:-----------------:|:-------:|:-------:|:-----:|:------:|:-----:|:-------:| :-------:| :-------:| :-------:| :-------:|  :-------:| 
| 달력  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
|통신  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| EMail     | ✓    | ✓       | ✓   | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| HomeAutomation          | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| 참고     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| 장소   | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| RestaurantReservation  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| ToDo     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| 공공 시설      | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Weather        | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Web    | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |

미리 작성 된 도메인은에서 **지원 되지 않습니다** .

* 프랑스어 (캐나다)
* 힌디어
* 스페인어 멕시코

## <a name="next-steps"></a>다음 단계

[간단한 엔터티](reference-entity-simple.md)를 알아보세요. 