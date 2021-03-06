---
title: 저장소 자동 증가-Azure Portal-Azure Database for MySQL
description: 이 문서에서는를 사용 하 여 Azure Database for MySQL에 대 한 저장소 자동 증가를 사용 하도록 설정할 수 있는 방법을 설명 Azure Portal
author: ambhatna
ms.author: ambhatna
ms.service: mysql
ms.topic: conceptual
ms.date: 12/02/2019
ms.openlocfilehash: 7be3e7e1a0d2e48b37c319f67e3b382f825469df
ms.sourcegitcommit: 6bb98654e97d213c549b23ebb161bda4468a1997
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74770614"
---
# <a name="auto-grow-storage-in-azure-database-for-mysql-using-the-azure-portal"></a>Azure Portal를 사용 하 여 Azure Database for MySQL의 저장소 자동 증가
이 문서에서는 워크 로드에 영향을 주지 않고 확장 되도록 Azure Database for MySQL server 저장소를 구성 하는 방법을 설명 합니다.

서버가 할당 된 저장소 제한에 도달 하면 서버가 읽기 전용으로 표시 됩니다. 그러나 저장소 자동 증가를 사용 하도록 설정 하면 증가 하는 데이터에 맞게 서버 저장소가 늘어납니다. 프로 비전 된 저장소 수가 100 미만인 서버의 경우, 사용 가능한 저장소가 프로 비전 된 저장소의 1gb 또는 10%를 초과 하는 즉시 프로 비전 된 저장소 크기는 5gb 씩 증가 합니다. 프로 비전 된 저장소 수가 100 GB를 넘는 서버에서는 사용 가능한 저장소 공간이 프로 비전 된 저장소 크기의 5% 미만이 면 프로 비전 된 저장소 크기가 5% 증가 합니다. [여기](https://docs.microsoft.com/azure/mysql/concepts-pricing-tiers#storage) 에 지정 된 대로 최대 저장소 제한이 적용 됩니다.

## <a name="prerequisites"></a>전제 조건
이 방법 가이드를 완료하려면 다음이 필요합니다.
- [Azure Database for MySQL 서버](quickstart-create-mysql-server-database-using-azure-portal.md)

## <a name="enable-storage-auto-grow"></a>저장소 자동 증가 사용 

MySQL server storage 자동 증가를 설정 하려면 다음 단계를 수행 합니다.

1. [Azure Portal](https://portal.azure.com/)에서 기존 Azure Database for MySQL 서버를 선택 합니다.

2. MySQL server 페이지의 **설정** 머리글 아래에서 **가격 책정 계층** 을 클릭 하 여 가격 책정 계층 페이지를 엽니다.

3. 자동 증가 섹션에서 **예** 를 선택 하 여 저장소 자동 증가를 사용 하도록 설정 합니다.

    ![Azure Database for MySQL-Settings_Pricing_tier-자동 증가](./media/howto-auto-grow-storage-portal/3-auto-grow.png)

4. **확인** 을 클릭하여 변경 내용을 저장합니다.

5. 자동 증가가 성공적으로 설정 되었음을 알리는 알림이 나타납니다.

    ![Azure Database for MySQL-자동 증가 성공](./media/howto-auto-grow-storage-portal/5-auto-grow-success.png)

## <a name="next-steps"></a>다음 단계

[메트릭에 대 한 경고를 만드는 방법](howto-alert-on-metric.md)에 대해 알아봅니다.
