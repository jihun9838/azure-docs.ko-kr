---
title: 포함 파일
description: 포함 파일
services: azure-monitor
author: rboucher
tags: azure-service-management
ms.topic: include
ms.date: 02/07/2019
ms.author: robb
ms.custom: include file
ms.openlocfilehash: c68e58bb18a5dba07855234af07b0a8be767bed0
ms.sourcegitcommit: f34165bdfd27982bdae836d79b7290831a518f12
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75927927"
---
응용 프로그램당 메트릭 및 이벤트 수에는 몇 가지 제한이 있습니다. 즉, 계측 키 당 몇 가지 제한이 있습니다. 선택하는 [가격 책정 계층](https://azure.microsoft.com/pricing/details/application-insights/)에 따라 제한됩니다.

| 리소스 | 기본 제한 | 참고
| --- | --- | --- |
| 일당 총 데이터 | 100GB | 한도를 설정하여 데이터를 줄일 수 있습니다. 더 많은 데이터가 필요한 경우 포털에서 최대 1,000GB로 한도를 늘릴 수 있습니다. 1000 GB 보다 큰 용량의 경우 AIDataCap@microsoft.com에 전자 메일을 보냅니다.
| 제한 | 32000 이벤트/초 | 제한은 분을 기준으로 측정됩니다.
| 데이터 보존 | 90일 | 이 리소스는 [검색](../articles/azure-monitor/app/diagnostic-search.md), [분석](../articles/azure-monitor/app/analytics.md) 및 [메트릭 탐색기](../articles/azure-monitor/app/metrics-explorer.md)의 경우입니다.
| [가용성 다단계 테스트](../articles/azure-monitor/app/availability-multistep.md) 자세한 결과 보존 | 90일 | 이 리소스는 각 단계의 자세한 결과를 제공합니다.
| 최대 이벤트 크기 | 6400만 바이트 |
| 속성 및 메트릭 이름 길이 | 150 | [형식 스키마](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/EndpointSpecs/Schemas/Bond/)를 참조하세요.
| 속성 값 문자열 길이 | 8,192 | [형식 스키마](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/EndpointSpecs/Schemas/Bond/)를 참조하세요.
| 추적 및 예외 메시지 길이 | 32,768  | [형식 스키마](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/EndpointSpecs/Schemas/Bond/)를 참조하세요.
| 앱당 [가용성 테스트](../articles/azure-monitor/app/monitor-web-app-availability.md) 수 | 100 |
| [프로파일러](../articles/azure-monitor/app/profiler.md) 데이터 보존 | 5일 |
| 일일 전송된 [프로파일러](../articles/azure-monitor/app/profiler.md) 데이터 | 10GB |

자세한 내용은 [Application Insights의 가격 책정 및 할당량 정보](../articles/azure-monitor/app/pricing.md)를 참조하세요.
