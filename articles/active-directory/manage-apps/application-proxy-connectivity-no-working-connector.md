---
title: 응용 프로그램 프록시 앱에 대 한 작동 중인 커넥터 그룹이 없습니다.
description: Azure AD 애플리케이션 프록시를 사용하는 애플리케이션에 대한 커넥터 그룹에 작동 중인 커넥터가 없을 때 발생할 수 있는 주소 문제
services: active-directory
documentationcenter: ''
author: msmimart
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: mimart
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96ab0d1b3bbab9c97c04da4f918f3aaa2f1d07e4
ms.sourcegitcommit: 653e9f61b24940561061bd65b2486e232e41ead4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74275614"
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>애플리케이션 프록시 애플리케이션에 대해 작동하는 커넥터 그룹 없음

이 문서는 Azure Active Directory와 통합된 애플리케이션 프록시 애플리케이션에 대해 검색된 커넥터가 없을 때 발생하는 일반적인 문제를 해결하는 데 도움이 됩니다.

## <a name="overview-of-steps"></a>단계 개요
애플리케이션의 커넥터 그룹에 작동 중인 커넥터가 없는 경우 몇 가지 방법을 사용하여 문제를 해결할 수 있습니다.

-   그룹에 커넥터가 없는 경우 다음을 수행할 수 있습니다.

    -   온-프레미스 서버에서 새 커넥터를 다운로드 하 여이 그룹에 할당 합니다.

    -   활성 커넥터를 그룹으로 이동합니다.

-   그룹에 활성 커넥터가 없는 경우 다음을 수행할 수 있습니다.

    -   커넥터가 비활성 상태인 이유를 식별하고 해결합니다.

    -   활성 커넥터를 그룹으로 이동합니다.

문제를 파악하려면 애플리케이션에서 "애플리케이션 프록시" 메뉴를 열고 커넥터 그룹 경고 메시지를 살펴봅니다. 그룹에 커넥터가 없으면 그룹에 하나 이상의 커넥터가 필요하다는 경고 메시지가 표시됩니다. 활성 커넥터가 없는 경우 경고 메시지에서 이에 대해 설명합니다. 일반적으로 비활성 커넥터가 있는 경우입니다. 

   ![Azure Portal에서 커넥터 그룹 선택](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

이러한 각 옵션에 대한 자세한 내용은 아래 해당 섹션을 참조하세요. 이 지침에서는 커넥터 관리 페이지에서 시작한다고 가정합니다. 위의 오류 메시지가 표시되면 경고 메시지를 클릭하여 이 페이지로 이동할 수 있습니다. 또한 **Azure Active Directory**로 이동하여 **엔터프라이즈 애플리케이션**, **애플리케이션 프록시**를 차례로 클릭하면 해당 페이지로 이동할 수 있습니다.

   ![Azure Portal에서 커넥터 그룹 관리](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>새 커넥터 다운로드

새 커넥터를 다운로드하려면 페이지 맨 위에 있는 "커넥터 다운로드" 단추를 사용합니다.

백 엔드 애플리케이션에 직접 연결되는 컴퓨터에 커넥터를 설치합니다. 일반적으로 커넥터는 애플리케이션과 동일한 서버에 설치됩니다. 다운로드 후 커넥터가 이 메뉴에 나타납니다. 커넥터를 클릭하고 "커넥터 그룹" 드롭다운을 사용하여 해당 그룹에 속하는지 확인합니다. 변경 내용을 저장합니다.

   ![Azure Portal에서 커넥터 다운로드](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>활성 커넥터 이동

그룹에 속해야 하며 대상 백 엔드 애플리케이션에 직접 연결된 활성 커넥터가 있는 경우 지정된 그룹으로 커넥터를 이동할 수 있습니다. 이렇게 하려면 커넥터를 클릭합니다. "커넥터 그룹" 필드에서 드롭다운을 사용하여 올바른 그룹을 선택하고 저장을 클릭합니다.

## <a name="resolve-an-inactive-connector"></a>비활성 커넥터 해결

그룹의 커넥터만 비활성 상태인 경우 필요한 모든 포트가 차단되지 않은 컴퓨터에 있을 수 있습니다.

이 문제를 조사하는 방법에 대한 자세한 내용은 포트 문제 해결 문서를 참조하세요.

## <a name="next-steps"></a>다음 단계
[Azure AD 애플리케이션 프록시 커넥터 이해](application-proxy-connectors.md)


