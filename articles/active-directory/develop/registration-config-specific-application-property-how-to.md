---
title: 사용자 지정 개발 앱에 대 한 Azure Portal 등록 필드
description: Azure AD에서 사용자 지정 개발 된 응용 프로그램 등록에 대 한 지침
services: active-directory
documentationcenter: ''
author: rwike77
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: develop
ms.custom: aaddev
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/28/2019
ms.author: ryanwi
ms.openlocfilehash: 36d74b9926639bb4ec49821a3d73b5d615016394
ms.sourcegitcommit: af6847f555841e838f245ff92c38ae512261426a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2020
ms.locfileid: "76702677"
---
# <a name="azure-portal-registration-fields-for-custom-developed-apps"></a>사용자 지정 개발 앱에 대 한 Azure Portal 등록 필드

이 아티클에서는 [Azure Portal](https://portal.azure.com)에서 애플리케이션 등록 양식에 사용 가능한 모든 필드에 대해 간략하게 설명합니다.

## <a name="register-a-new-application"></a>새 애플리케이션 등록

-   새 애플리케이션을 등록하려면 [Azure Portal](https://portal.azure.com)로 이동합니다.

-   왼쪽 탐색 창에서 **Azure Active Directory**를 클릭합니다.

-   **앱 등록**을 선택하고 **추가**를 클릭합니다.

-   그러면 애플리케이션 등록 양식이 열립니다.

## <a name="fields-in-the-application-registration-form"></a>애플리케이션 등록 양식의 필드

| 필드            | Description                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| 이름             | 애플리케이션 이름입니다. 최소 4자 이상이어야 합니다.                |
| 지원되는 계정 유형| 응용 프로그램에서 지원할 계정 (이 조직 디렉터리의 계정에만 해당), 조직 디렉터리의 계정 또는 조직 디렉터리와 개인 Microsoft 계정의 계정을 선택 합니다.  |
| URI 리디렉션(선택 사항) | 빌드 중인 앱 유형, **웹** 또는 **공용 클라이언트 (모바일 & 데스크톱)** 를 선택 하 고 응용 프로그램에 대 한 리디렉션 URI 또는 회신 URL을 입력 합니다. 웹 애플리케이션의 경우 앱의 기준 URL을 제공합니다. 예를 들어 http://localhost:31544 은 로컬 컴퓨터에서 실행 중인 웹앱의 URL일 수 있습니다. 사용자는 이 URL을 사용하여 웹 클라이언트 애플리케이션에 로그인합니다. 공용 클라이언트 애플리케이션의 경우 Azure AD에서 토큰 응답을 반환하는 데 사용하는 URI를 제공합니다. 응용 프로그램에 특정 한 값 (예: myapp://auth)을 입력 합니다. 웹 응용 프로그램 또는 네이티브 응용 프로그램에 대 한 특정 예제를 보려면 빠른 [시작을 확인 하세요.](https://docs.microsoft.com/azure/active-directory/develop)|

위의 필드를 채우면 응용 프로그램이 Azure Portal에 등록 되 고 응용 프로그램 개요 페이지로 리디렉션됩니다. **관리** 아래의 왼쪽 창에 있는 설정 페이지에는 응용 프로그램을 사용자 지정할 수 있는 추가 필드가 있습니다. 아래 표에서는 모든 필드에 대해 설명 합니다. 웹 응용 프로그램을 만들었는지 아니면 공용 클라이언트 응용 프로그램을 만들었는지에 따라 이러한 필드의 하위 집합만 표시 됩니다.

### <a name="overview"></a>개요

| 필드           | Description        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 애플리케이션 UI  | 애플리케이션을 등록하면 Azure AD에서 애플리케이션에 애플리케이션 ID를 할당합니다. 애플리케이션 ID는 Graph API 같은 리소스에 액세스뿐만 아니라 Azure AD에 인증 요청 시 애플리케이션을 고유하게 식별하는 데 사용될 수 있습니다.                                                          |
| 앱 ID URI      | 고유한 URI여야 하며 일반적으로 형식은 **https://&lt;tenant\_name&gt;/&lt;application\_name&gt;입니다.** 이는 토큰을 발급할 리소스를 지정 하기 위한 고유 식별자로 권한 부여 흐름 중에 사용 됩니다. 또한 발급된 액세스 토큰의 'aud' 클레임이 됩니다. |

### <a name="branding"></a>브랜딩

| 필드           | Description        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 새 로고 업로드 | 애플리케이션에 대한 로고를 업로드하는 데 사용할 수 있습니다. 로고는 .bmp, .jpg 또는 .png 형식 이어야 하며 파일 크기는 100 미만 이어야 합니다. 이미지 크기는 215x215 픽셀이어야 합니다(중앙 이미지 크기는 94x94 픽셀).|
| 홈페이지 URL   | 애플리케이션 등록 시 지정된 로그온 URL입니다.|

### <a name="authentication"></a>인증

| 필드           | Description        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 로그아웃 URL      | 단일 로그 아웃 로그 아웃 URL입니다. 사용자가 다른 등록된 애플리케이션을 사용하여 Azure AD의세션을 지우면 Azure AD에서 이 URL로 로그아웃 요청을 전송합니다.|
| 지원되는 계정 유형  | 이 스위치는 여러 테넌트에서 애플리케이션을 사용할 수 있는지 여부를 지정합니다. 일반적으로 외부 조직에서 테넌트를 등록하고 조직의 데이터에 대한 액세스 권한을 부여하여 애플리케이션을 사용할 수 있습니다.|
| 리디렉션 URL      | 리디렉션 또는 회신 Url은 Azure AD가 응용 프로그램에서 요청 하는 토큰을 반환 하는 끝점입니다. 네이티브 애플리케이션의 경우 성공적인 권한 부여 후에 사용자에게 전송되는 URI입니다. Azure AD는 OAuth 2.0 요청에서 응용 프로그램이 제공 하는 리디렉션 URI가 포털의 등록 된 값 중 하 나와 일치 하는지 확인 합니다.|

### <a name="certificates-and-secrets"></a>인증서 및 비밀

| 필드           | Description        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 클라이언트 비밀            | 클라이언트 암호 또는 키를 만들어 사용자 개입 없이 Azure AD로 보호 되는 웹 Api에 프로그래밍 방식으로 액세스할 수 있습니다. **새 클라이언트 암호** 페이지에서 키 설명 및 만료 날짜를 입력 하 고 저장을 입력 하 여 키를 생성 합니다. 나중에 액세스하지 못하므로 키를 안전한 곳에 보관하세요.             |

## <a name="next-steps"></a>다음 단계

[Azure Active Directory로 애플리케이션 관리](../manage-apps/what-is-application-management.md)
