---
title: 데이터 관리 게이트웨이에 대한 릴리스 정보
description: 데이터 관리 게이트웨이 릴리스 정보
services: data-factory
author: nabhishek
manager: anandsub
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: abnarain
robots: noindex
ms.openlocfilehash: 9d0e31a89494477e048c7a2f9f7b8165e08d1a2f
ms.sourcegitcommit: a5ebf5026d9967c4c4f92432698cb1f8651c03bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74924271"
---
# <a name="release-notes-for-data-management-gateway"></a>데이터 관리 게이트웨이에 대한 릴리스 정보
> [!NOTE]
> 이 문서는 Data Factory 버전 1에 적용됩니다. 현재 버전의 Data Factory 서비스를 사용 중인 경우, [V2의 자체 호스팅 통합 런타임](../create-self-hosted-integration-runtime.md)을 참조하세요.

최신 데이터 통합의 과제 중 하나는 온-프레미스 간 및 온-프레미스에서 클라우드로 데이터를 이동하는 것입니다. Data Factory를 사용하면 하이브리드 데이터 이동을 지원하기 위해 온-프레미스에 설치할 수 있는 에이전트인 데이터 관리 게이트웨이와 이러한 통합을 수행할 수 있습니다.

데이터 관리 게이트웨이 및 사용 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

*  [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)
*  [Azure 데이터 팩터리를 사용하여 온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version"></a>현재 버전 
여기에서 릴리스 정보를 더 이상 유지하지 않습니다. [여기](https://go.microsoft.com/fwlink/?linkid=853077)에서 최신 릴리스 정보 가져오기




## <a name="earlier-versions"></a>이전 버전
## <a name="21063477"></a>2.10.6347.7
### <a name="enhancements-"></a>향상된 기능
- 필요한 경우 방화벽의 모든 Azure IP 주소를 허용 목록에 포함하는 대신 DNS 항목을 추가하여 서비스 버스를 허용 목록에 포함할 수 있습니다. Azure Portal에서 각각의 DNS 항목을 찾을 수 있습니다(Data Factory -> '작성자 및 배포' -> '게이트웨이' -> JSON의 “serviceUrls”).
- 이제 HDFS 커넥터는 SSL 유효성 검사를 건너뛸 수 있도록 하여 자체 서명된 공용 인증서를 지원합니다.
- 업데이트 중에 클록 오차(clock skew)로 인해 발생하는 게이트웨이 오프라인 문제가 수정되었습니다.


## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>향상된 기능
-   (필요한 경우) 방화벽의 모든 Azure IP 주소를 허용 목록에 포함하는 대신 DNS 항목을 추가해 Service Bus를 허용 목록에 추가할 수 있습니다. 자세한 내용은 다음을 참조하세요.
-   이제, 단일 블록 Blob에/에서 데이터를 최대 4.75TB까지 복사할 수 있습니다. 이 크기는 단일 블록 Blob에 대해 지원되는 최대값입니다. 이전에는 195GB까지로 제한되었습니다.
-   복사 작업 중 작은 파일 여러 개의 압축을 푸는 동안 발생하는 메모리 부족 문제가 수정되었습니다.
-   멱등 기능을 사용하여 DocumentDB에서 온-프레미스 SQL Server로 복사하는 중에 범위를 벗어나는 인덱스 문제가 수정되었습니다.
-   SQL 정리 스크립트가 복사 마법사에서 온-프레미스 SQL Server와 작동하지 않는 문제가 수정되었습니다.
-   끝에 공백이 있는 열 이름이 복사되지 않는 문제가 수정되었습니다.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>향상된 기능
- 게이트웨이 컴퓨터를 다시 부팅할 때 자격 증명이 누락되는 문제가 수정되었습니다.
- 백업 파일을 사용하여 게이트웨이를 복원하는 중에 발생하는 등록 문제가 수정되었습니다.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>향상된 기능
- Oracle에서 10진수 null 값을 원본으로 잘못 읽는 문제가 수정되었습니다.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>새 소식
- 고객이 게이트웨이 등록 경험에 대한 피드백을 제공할 수 있습니다.
- 새 압축 형식 지원: ZIP (Deflate)

### <a name="enhancements-"></a>향상된 기능
- Oracle Sink, HDFS 원본에 대한 성능 개선
- 게이트웨이 자동 업데이트, 게이트웨이 병렬 처리 용량에 대한 버그 수정


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>향상된 기능
- 더욱 강력하고 향상된 게이트웨이 등록 환경- 게이트웨이 등록 프로세스 동안 진행 상태를 추적할 수 있어, 더 나은 응답성의 등록 환경이 만들어졌습니다.
- 게이트웨이 복원 프로세스 개선-이 업데이트를 사용하여 게이트웨이 백업 파일이 없는 경우에도 게이트웨이를 복구할 수 있습니다. 포털에서 연결된 서비스 자격 증명을 다시 설정해야 합니다.
- 버그 수정

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>새 소식

- 이제 데이터 원본 자격 증명을 로컬로 저장할 수 있습니다. 자격 증명은 암호화됩니다. 데이터 원본 자격 증명은 기존 게이트웨이에서 내보낸 백업 파일을 사용하여 온-프레미스에서 모두 복구하고 복원할 수 있습니다.

### <a name="enhancements-"></a>향상된 기능

- 더 강력하게 향상된 게이트웨이 등록 환경을 제공합니다.
- 복사 마법사에서 텍스트 형식의 QuoteChar 구성에 대한 자동 검색을 지원하고 향상된 전체 형식 검색 정확도를 제공합니다.

## <a name="2361002"></a>2.3.6100.2

- 온-프레미스 파일 시스템 및 HDFS의 텍스트 파일에 대해 복사 마법사의 firstRowAsHeader 및 SkipLineCount 자동 검색을 지원합니다.
- 게이트웨이와 Service Bus 간의 네트워크 연결 안정성이 향상되었습니다.
- 몇 가지 버그 수정


## <a name="2260721"></a>2.2.6072.1

*  게이트웨이 구성 관리자를 사용하여 게이트웨이의 HTTP 프록시를 설정할 수 있습니다. Azure Blob, Azure 테이블, Azure Data Lake 및 DocumentDB가 구성되어 있는 경우 HTTP 프록시를 통해 액세스할 수 있습니다.
*  Azure Blob, Azure Data Lake Store, 온-프레미스 파일 시스템 및 온-프레미스 HDFS를 원본/대상으로 사용하여 데이터를 복사할 때 TextFormat의 헤더 처리가 지원됩니다.
*  이미 복사가 지원되는 블록 Blob는 물론 추가 Blob 및 페이지 Blob에서도 데이터를 복사할 수 있습니다.
*  새로운 게이트웨이 상태인 **온라인(제한됨)** 이 도입되었습니다. 이 상태는 복사 마법사의 대화형 작업 지원을 제외한 게이트웨이의 기본 기능이 작동함을 나타냅니다.
*  등록 키를 사용하여 게이트웨이를 보다 안정적으로 등록할 수 있습니다.

## <a name="216040"></a>2.1.6040.

*  DB2 드라이버는 이제 게이트웨이 설치 패키지에 포함됩니다. 별도로 설치할 필요가 없습니다.
*  이제 DB2 드라이버는 이미 지원되는 플랫폼(Linux, Unix 및 Windows)과 함께 i(AS/400)용 z/OS 및DB2를 지원합니다.
*  온-프레미스 데이터 저장소에 대한 Azure Cosmos DB를 원본 또는 대상으로 사용하도록 지원합니다.
*  이미 지원되는 범용 스토리지 계정과 함께 콜드/핫 Blob Storage에서/으로 데이터를 복사하도록 지원합니다.
*  원격 로그인 권한이 있는 게이트웨이를 통해 온-프레미스 SQL Server에 연결할 수 있습니다.  

## <a name="2060131"></a>2.0.6013.1

*  수동으로 설치하는 동안 게이트웨이에서 사용할 언어/문화권을 선택할 수 있습니다.

*  게이트웨이가 정상적으로 작동하지 않으면 문제를 쉽게 해결할 수 있도록 지난 7일 동안의 게이트웨이 로그를 Microsoft에 전송할 수 있습니다. 게이트웨이가 클라우드 서비스에 연결되어 있지 않으면 게이트웨이 로그를 저장하고 보관할 수 있습니다.  

*  게이트웨이 구성 관리자에 대한 사용자 인터페이스 개선 사항:

    *  게이트웨이 상태가 홈 탭에 잘 보이도록 합니다.

    *  재구성되고 간소화된 컨트롤입니다.

    *  [코드가 없는 복사 도구](data-factory-copy-data-wizard-tutorial.md)를 사용하여 스토리지에서 데이터를 복사할 수 있습니다. 이 기능에 대한 전반적인 세부 정보는 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy) 를 참조하세요.
*  데이터 관리 게이트웨이를 사용하여 온-프레미스 SQL Server 데이터베이스에서 Azure Machine Learning으로 직접 데이터를 수신할 수 있습니다.

*  성능 개선

    * 코드가 없는 복사 도구에서 SQL Server에 대해 스키마/미리 보기를 보는 성능이 향상됩니다.

## <a name="11259531"></a>1.12.5953.1

*  버그 수정

## <a name="11159181"></a>1.11.5918.1

*  게이트웨이 이벤트 로그의 최대 크기가 1MB에서 40MB로 증가되었습니다.

*  게이트웨이를 자동 업데이트하는 동안 다시 시작이 필요하면 경고 대화 상자가 표시됩니다. 바로 또는 나중에 다시 시작하도록 선택할 수 있습니다.

*  자동 업데이트가 실패하면 게이트웨이 설치 관리자는 자동 업데이트를 최대 3회까지 다시 시도합니다.

*  성능 개선

    * 코드가 없는 복사 시나리오를 통해 온-프레미스 서버의 큰 테이블을 로드하는 성능을 개선합니다.

*  버그 수정

## <a name="11058921"></a>1.10.5892.1

*  성능 개선

*  버그 수정

## <a name="1958652"></a>1.9.5865.2

*  0 터치 자동 업데이트 기능
*  게이트웨이 상태 표시기 포함 새 트레이 아이콘
*  클라이언트에서 "지금 업데이트"하는 기능
*  업데이트 일정 시간을 설정하는 기능
*  자동 업데이트를 설정/해제하기 위한 PowerShell 스크립트
*  JSON 형식 파일 지원  
*  성능 개선
*  버그 수정

## <a name="1858221"></a>1.8.5822.1

*  문제 해결 환경 개선
*  성능 개선
*  버그 수정

### <a name="1757951"></a>1.7.5795.1

*  성능 개선
*  버그 수정

### <a name="1757641"></a>1.7.5764.1

*  성능 개선
*  버그 수정

### <a name="1657351"></a>1.6.5735.1

*  온-프레미스 HDFS 원본/싱크 지원
*  성능 개선
*  버그 수정

### <a name="1656961"></a>1.6.5696.1

*  성능 개선
*  버그 수정

### <a name="1656761"></a>1.6.5676.1

*  구성 관리자에서 진단 도구 지원
*  Azure 데이터 팩터리에 대 한 테이블 데이터 원본의 테이블 열 지원
*  Azure 데이터 팩터리에 대 한 SQL DW 지원
*  Azure 데이터 팩터리에 대한 BlobSource 및 FileSource의 단독 지원
*  CopyBehavior 지원 – Azure Data Factory의 이진 복사 기능을 통해 BlobSink 및 FileSink에서 MergeFiles, PreserveHierarchy, FlattenHierarchy 지원
*  Azure 데이터 팩터리의 진행률을 보고하는 복사 작업 지원
*  Azure 데이터 팩터리에 대한 데이터 원본 연결 유효성 검사 지원
*  버그 수정

### <a name="1656721"></a>1.6.5672.1

*  Azure 데이터 팩터리에 대 한 ODBC 데이터 원본의 테이블 이름 지원
*  성능 개선
*  버그 수정

### <a name="1656581"></a>1.6.5658.1

*  Azure 데이터 팩터리에 대 한 파일 싱크 지원
*  Azure 데이터 팩터리에 대 한 이진 복사본에서 계층 구조 유지 지원
*  Azure 데이터 팩터리에 대한 복사 작업 멱등성 지원
*  버그 수정

### <a name="1656401"></a>1.6.5640.1

*  Azure 데이터 팩터리(ODBC, OData, HDFS)에 대 한 3개 더 많은 데이터 원본 지원
*  Azure 데이터 팩터리에 대 한 csv 파서에서 따옴표 문자 지원
*  압축 지원(BZip2)
*  버그 수정

### <a name="1556121"></a>1.5.5612.1

*  Azure Data Factory에 대해 관계형 데이터베이스 5개(MySQL, PostgreSQL, DB2, Teradata, Sybase) 지원
*  압축 지원(Gzip 및 Deflate)
*  성능 개선
*  버그 수정

### <a name="1455491"></a>1.4.5549.1

*  Azure 데이터 팩터리에 대 한 Oracle 데이터 원본 지원 추가
*  성능 개선
*  버그 수정

### <a name="1454921"></a>1.4.5492.1

*  Microsoft Azure 데이터 팩터리 및 Office 365 Power BI 서비스를 지원하는 통합 된 이진 파일
*  구성 UI 및 등록 프로세스 구체화
*  Azure 데이터 팩터리 - SQL Server 데이터 원본에 대한 Azure 수신 및 송신 지원

### <a name="1253031"></a>1.2.5303.1

*  더 많은 시간이 소비되는 데이터 원본 연결을 지원하도록 시간 초과 문제를 해결합니다.

### <a name="1155268"></a>1.1.5526.8

*  설치하는 동안 필수 요소로 .NET Framework 4.5.1이 필요합니다.

### <a name="1051442"></a>1.0.5144.2

*  Azure 데이터 팩터리 시나리오에 영향을 주는 변경은 없습니다.
