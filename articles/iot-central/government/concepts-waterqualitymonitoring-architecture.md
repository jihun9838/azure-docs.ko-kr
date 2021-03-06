---
title: Azure IoT Central로 빌드된 용수 품질 모니터링 솔루션을 위한 참조 아키텍처| Microsoft Docs
description: Azure IoT Central로 빌드된 용수 품질 모니터링 솔루션의 개념에 대해 알아보세요.
author: miriambrus
ms.author: miriamb
ms.date: 10/23/2019
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.openlocfilehash: cffa571028dac192e8b8806ee9ec932cf89eb1fe
ms.sourcegitcommit: c22327552d62f88aeaa321189f9b9a631525027c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73498776"
---
# <a name="water-quality-monitoring-reference-architecture"></a>용수 품질 모니터링 참조 아키텍처 

[!INCLUDE [iot-central-pnp-original](../../../includes/iot-central-pnp-original-note.md)]

용수 품질 모니터링 솔루션은 **Azure IoT Central 앱 템플릿**을 사용하여 킥 스타터 IoT 애플리케이션으로 빌드할 수 있습니다. 이 문서는 엔드투엔드 솔루션 빌드에 관한 높은 수준의 참조 아키텍처를 제공합니다. 


![용수 품질 모니터링 아키텍처](./media/concepts-waterqualitymonitoring-architecture/concepts-waterqualitymonitoring-architecture1.png)

개념:

1. 디바이스 및 연결  
1. IoT Central 
2. 확장성 및 통합
3. 비즈니스 애플리케이션

용수 품질 모니터링 솔루션에 일반적으로 관여하는 주요 구성 요소를 살펴보겠습니다.

## <a name="devices-and-connectivity"></a>디바이스 및 연결 
이 섹션에서는 용수 품질 모니터링 또는 용수 사용량 모니터링에 사용되는 디바이스를 스마트 워터 디바이스라고 통칭합니다. 스마트 워터 디바이스에는 유량계, 용수 품질 모니터, 스마트 밸브, 누출 감지기 등이 포함될 수 있습니다.

스마트 워터 솔루션에 사용되는 디바이스는 일반적으로 타사 네트워크 사업자를 통한 저전력 광대역 네트워크(LPWAN)를 통해 연결됩니다. 이러한 유형의 디바이스는 [Azure IoT Central Device Bridge](https://docs.microsoft.com/azure/iot-central/core/howto-build-iotc-device-bridge)를 사용하여 Azure IoT Central의 IoT 애플리케이션으로 디바이스 데이터를 전송할 수 있습니다. 또는 IP 기능이 포함된 디바이스 게이트웨이를 보유한 경우 IoT Central에 직접 연결할 수 있습니다.

## <a name="iot-central"></a>IoT Central 
Azure IoT Central은 IoT 솔루션을 빠르게 시작하거나 실행하도록 도와주는 IoT 앱 플랫폼입니다. 솔루션을 브랜딩 및 사용자 지정하거나 타사 서비스와 통합할 수 있습니다.
스마트 워터 디바이스를 IoT Central에 연결하면 디바이스 명령 및 제어, 모니터링 및 경고, RBAC가 내장된 사용자 인터페이스, 구성 가능한 인사이트 대시보드, 확장성 옵션을 이용할 수 있습니다. 

## <a name="extensibility-and-integrations"></a>확장성 및 통합 
IoT Central에서 IoT 애플리케이션을 확장하고 선택적으로 다음을 수행할 수 있습니다.
* 고급 분석을 위해 IoT 데이터를 변환하고 통합(예: IoT Central 애플리케이션에서 데이터를 지속적으로 내보내 기계 학습 모델을 교육)
* IoT Central 애플리케이션의 웹후크 또는 Microsoft Flow를 통해 작업을 트리거하여 다른 시스템의 워크플로 자동화
* IoT Central API를 통해 IoT Central의 IoT 애플리케이션에 프로그래밍 방식으로 액세스

## <a name="business-applications"></a>비즈니스 애플리케이션 
IoT 데이터는 상수도 시설 내 다양한 비즈니스 애플리케이션을 지원하는 데 사용될 수 있습니다. IoT Central 용수 품질 모니터링 애플리케이션을 필드 서비스와 연결하는 방법은 [Dynamics 365 Field Services와 통합하는 방법](./how-to-configure-connected-field-services.md) 문서를 참조하세요. 


## <a name="next-steps"></a>다음 단계
* [용수 품질 모니터링](./tutorial-water-quality-monitoring.md) IoT Central 애플리케이션을 만드는 방법 알아보기
* [IoT Central 정부 기관 템플릿](./overview-iot-central-government.md)에 대해 자세히 알아보기
* IoT Central에 대해 자세히 알아보기 위해 [IoT Central 개요](https://docs.microsoft.com/azure/iot-central/core/overview-iot-central) 참조

