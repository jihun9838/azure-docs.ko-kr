---
title: 개발 모범 사례
description: Azure SQL Data Warehouse에 대한 솔루션을 개발하면서 알아야 할 권장 사항 및 모범 사례입니다.
services: sql-data-warehouse
author: XiaoyuMSFT
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.subservice: development
ms.date: 09/04/2018
ms.author: xiaoyul
ms.reviewer: igorstan
ms.custom: seo-lt-2019
ms.openlocfilehash: 3a75be7eef69acb499222b39bc4f59962462b493
ms.sourcegitcommit: 609d4bdb0467fd0af40e14a86eb40b9d03669ea1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73685902"
---
# <a name="development-best-practices-for-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse에 대한 개발 모범 사례
이 문서에서는 데이터 웨어하우스 솔루션을 개발할 때 도움이 되는 지침 및 모범 사례에 대해 설명합니다. 

## <a name="tune-query-performance-with-new-product-enhancements"></a>새로운 제품 향상으로 쿼리 성능 조정  
- [구체화 된 뷰로 성능 조정](https://docs.microsoft.com/azure/sql-data-warehouse/performance-tuning-materialized-views)
- [순서가 지정 된 클러스터형 columnstore 인덱스로 성능 튜닝](https://docs.microsoft.com/azure/sql-data-warehouse/performance-tuning-ordered-cci)
- [결과 집합 캐싱을 사용한 성능 조정](https://docs.microsoft.com/azure/sql-data-warehouse/performance-tuning-result-set-caching)

## <a name="reduce-cost-with-pause-and-scale"></a>일시 중지 및 규모 조정으로 비용 절감
일시 중지 및 크기 조정을 통해 비용을 절감하는 방법에 대한 자세한 내용은 [컴퓨팅 관리](sql-data-warehouse-manage-compute-overview.md)를 참조하세요. 

## <a name="maintain-statistics"></a>통계 유지 관리
열에 대 한 통계를 자동으로 검색 하 고 만들려면 Azure SQL Data Warehouse를 구성할 수 있습니다.  최적화 프로그램에서 생성 하는 쿼리 계획은 사용 가능한 통계 만큼만 사용할 수 있습니다.  데이터베이스에 대해 AUTO_CREATE_STATISTICS를 사용 하도록 설정 하 고 매일 또는 각 로드 후 통계를 업데이트 하 여 쿼리에 사용 되는 열에 대 한 통계가 항상 최신 상태를 유지 하도록 하는 것이 좋습니다. 

모든 통계를 업데이트 하는 데 시간이 너무 오래 걸리면 자주 통계를 업데이트 해야 하는 열을 선택 하는 것이 좋습니다. 예를 들어 새 값이 매일 추가될 수 있는 날짜 열을 업데이트하려고 합니다. **조인에 포함 된 열, WHERE 절에 사용 된 열 및 GROUP BY에 있는 열에 대 한 통계를 업데이트 하 여 가장 많은 이점을 얻을 수 있습니다.**

참고 항목: [테이블 통계 관리][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="hash-distribute-large-tables"></a>해시 배포 대형 테이블
기본적으로 테이블은 라운드 로빈 분산됩니다.  이 디자인을 사용 하면 사용자가 테이블을 배포 하는 방법을 결정 하지 않고도 쉽게 테이블을 만들 수 있습니다.  라운드 로빈 테이블은 일부 워크로드에 대해서는 잘 작동하지만 대체로 배포 열을 선택하면 성능이 훨씬 향상됩니다.  열로 배포된 테이블이 라운드 로빈 테이블의 성능을 능가하는 가장 일반적인 예는 두 개의 대형 팩트 테이블이 조인된 경우입니다.  예를 들어 order_id로 배포되는 주문 테이블과 order_id로 배포되는 트랜잭션 테이블이 있고 주문 테이블을 order_id로 트랜잭션 테이블에 조인하는 경우 이 쿼리는 통과 쿼리가 되어 데이터 이동 작업을 제거합니다.  단계가 적을수록 쿼리는 빨라집니다.  데이터 이동이 적을수록 쿼리는 빨라집니다.  이 설명에서는 화면을 스크래치만 합니다. 분산된 테이블을 로드할 때 로드가 느려지므로 들어오는 데이터가 배포 키로 정렬되지 않도록 합니다.  배포 열을 선택 하 여 성능을 향상 시킬 수 있는 방법 및 CREATE TABLES 문의 WITH 절에서 분산 테이블을 정의 하는 방법에 대 한 자세한 내용은 아래 링크를 참조 하세요.

참고 항목: [테이블 개요][Table overview], [테이블 배포][Table distribution], [테이블 배포 선택][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>과도한 분할 피하기
분할 데이터는 파티션 전환을 통해 데이터를 유지 관리 하거나 파티션 제거를 사용 하 여 검색을 최적화 하는 데 효과적일 수 있지만 너무 많은 파티션이 있으면 쿼리 속도가 느려질 수 있습니다.  종종 SQL Server에서 잘 작동할 수 있는 높은 세분성 분할 전략이 SQL Data Warehouse에서 잘 작동 하지 않을 수 있습니다.  너무 많은 파티션을 포함하면 각 파티션에 100만 개 미만의 행이 포함된 경우 클러스터형 columnstore 인덱스의 효율성이 떨어질 수도 있습니다.  배후에서 SQL Data Warehouse가 사용자 데이터를 60개 데이터베이스로 분할했다면 100개 파티션이 있는 한 개의 테이블을 만들면 실제로는 6000개의 파티션이 생기는 것입니다.  각 워크로드가 서로 다르므로 가장 좋은 방법은 분할 실험을 통해 사용자의 워크로드에 가장 적합한 방법을 찾는 것입니다.  SQL Server에서 작업한 것보다 낮은 세분성을 고려합니다.  예를 들어 매일 분할보다는 매주 또는 매달 분할을 사용하는 것이 좋습니다.

참고 항목: [테이블 분할][Table partitioning]

## <a name="minimize-transaction-sizes"></a>트랜잭션 크기 최소화
INSERT, UPDATE, DELETE 문은 트랜잭션에서 실행되며 실패할 경우 롤백해야 합니다.  긴 롤백에 대한 가능성을 최소화하려면 가능한 경우 항상 트랜잭션 크기를 최소화합니다.  INSERT, UPDATE 및 DELETE 문을 부분으로 나누어 이를 수행할 수 있습니다.  예를 들어 1 시간이 소요 될 것으로 예상 되는 삽입이 있는 경우 가능한 경우 삽입을 4 개의 부분으로 분할 합니다. 그러면 각각 15 분 이내에 실행 됩니다.  CTAS, TRUNCATE, DROP TABLE 또는 INSERT와 같은 특수한 로깅 사례를 최소한 활용하여 롤백 위험을 줄입니다.  롤백을 제거하는 다른 방법은 데이터 관리를 위한 파티션 전환과 같은 메타데이터 전용 작업을 사용하는 것입니다.  예를 들어 테이블에서 order_date가 2001년 10월인 모든 행을 제거하기 위해 DELETE 문을 실행하는 대신 데이터를 매달 분할한 후 해당 파티션을 다른 테이블의 비어 있는 파티션의 데이터로 전환할 수 있습니다(ALTER TABLE 예 참조).  분할되지 않은 테이블의 경우 DELETE를 사용하는 대신, 테이블에 유지할 데이터를 기록하도록 CTAS를 사용하는 것이 좋습니다.  CTAS가 같은 시간을 사용 하는 경우 최소한의 트랜잭션 로깅을 사용 하 고 필요한 경우 신속 하 게 취소할 수 있으므로 실행 하는 것이 훨씬 안전 합니다.

참고 항목: [트랜잭션 이해][Understanding transactions], [트랜잭션 최적][Optimizing transactions], [테이블 분할][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [CTAS(Create Table As Select)][Create table as select (CTAS)]

## <a name="use-the-smallest-possible-column-size"></a>가능한 가장 작은 열 크기 사용
DDL을 정의할 때 데이터를 지원할 가장 작은 데이터 형식을 사용 하면 쿼리 성능이 향상 됩니다.  이것은 CHAR 및 VARCHAR 열에 대해 특히 중요합니다.  열에서 가장 긴 값이 25자인 경우 열을 VARCHAR(25)로 정의합니다.  모든 문자 열을 큰 기본 길이로 정의하지 마세요.  또한 반드시 필요한 경우에는 열을 NVARCHAR를 사용하는 것보다 VARCHAR로 정의하세요.

참고 항목: [테이블 개요][Table overview], [테이블 데이터 형식][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="optimize-clustered-columnstore-tables"></a>클러스터형 Columnstore 테이블 최적화
columnstore 클러스터형 인덱스는 Azure SQL Data Warehouse에 데이터를 저장할 수 있는 가장 효율적인 방법 중 하나입니다.  기본적으로 SQL Data Warehouse의 테이블은 클러스터형 ColumnStore로 만들어집니다.  columnstore 테이블에서 쿼리에 대해 최상의 성능을 얻으려면 좋은 세그먼트 품질을 갖는 것이 중요합니다.  메모리 부족 상황에서 행이 columnstore 테이블에 기록되는 경우 columnstore 세그먼트 품질이 저하될 수 있습니다.  세그먼트 품질은 압축된 행 그룹에 있는 행의 수로 측정할 수 있습니다.  클러스터형 columnstore 테이블에 대해 세그먼트 품질을 감지하고 개선하는 단계별 지침은 [테이블 인덱스][Causes of poor columnstore index quality] 문서의 [Columnstore 인덱스 품질 저하 원인][Table indexes] 섹션을 참조하세요.  고품질 columnstore 세그먼트가 중요 하기 때문에 데이터를 로드 하기 위해 중간 규모 또는 대규모 리소스 클래스에 있는 사용자 Id를 사용 하는 것이 좋습니다. 낮은 [데이터 웨어하우스 단위](what-is-a-data-warehouse-unit-dwu-cdwu.md)를 사용하면 로드하는 사용자에게 더 큰 리소스 클래스를 할당하려는 것입니다.

columnstore 테이블은 일반적으로 테이블당 100개 이상의 행이 있고 각 SQL Data Warehouse 테이블이 60개 테이블로 파티션될 때까지 데이터를 압축된 columnstore 세그먼트에 푸시하지 않으므로 경험에 따르면 테이블에서 행 수가 6천만 개를 초과하지 않는다면 columnstore 테이블은 쿼리에 이점을 제공하지 않습니다.  6천만 개 미만의 행이 있는 테이블의 경우 columnstore 인덱스를 포함하는 것이 적절하지 않을 수 있습니다.  오히려 상황을 악화시킬 수 있습니다.  또한 데이터를 분할하는 경우 클러스터형 columnstore 인덱스의 이점을 얻기 위해 각 파티션에는 100개의 행을 포함하는 것이 좋습니다.  테이블에 파티션 수가 100개라면 클러스터형 columnstore에서 이점을 얻으려면 60억 개 이상의 행을 포함해야 합니다(60개 배포 * 100개 파티션 * 1백만 행).  이 예에서 테이블에 60억 개의 행이 없으면 파티션 수를 줄이거나 대신 힙 테이블을 사용하는 것이 좋습니다.  또한 실험을 통해 columnstore 테이블 대신 보조 인덱스가 있는 힙 테이블로 더 나은 성능을 얻을 수 있는지도 확인할 수 있습니다.

columnstore 테이블을 쿼리할 때 필요한 열만 선택하면 쿼리가 더 빨리 실행됩니다.  

참고 항목: [테이블 인덱스][Table indexes], [Columnstore 인덱스 가이드][Columnstore indexes guide], [Columnstore 인덱스 다시 빌드][Rebuilding columnstore indexes]

## <a name="next-steps"></a>다음 단계
이 문서에서 원하는 항목을 찾지 못한 경우이 페이지의 왼쪽에 있는 "문서 검색"을 사용 하 여 모든 Azure SQL Data Warehouse 문서를 검색 해 보세요.  [Azure SQL Data Warehouse 포럼][Azure SQL Data Warehouse MSDN Forum] 은 다른 사용자 및 SQL Data Warehouse 제품 그룹에 게 질문을 할 수 있는 장소입니다.  Microsoft는 이 포럼을 적극적으로 모니터링하여 사용자의 질문에 다른 사용자나 당사 직원이 응답하도록 합니다.  스택 오버플로에 질문하는 것을 선호하는 경우 [Azure SQL Data Warehouse 스택 오버플로 포럼][Azure SQL Data Warehouse Stack Overflow Forum]도 제공합니다.

마지막으로 [Azure SQL Data Warehouse 피드백][Azure SQL Data Warehouse Feedback] 페이지를 사용하여 기능을 요청합니다.  요청을 추가하거나 다른 요청에 투표를 하면 기능의 순위를 지정하는 데 도움이 됩니다.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./guidance-for-loading-data.md
[Load data]: ./design-elt-data-loading.md
[Move data with Azure Data Factory]: ../data-factory/transform-data-using-machine-learning.md
[Load data with Azure Data Factory]: ../data-factory/load-azure-sql-data-warehouse.md
[Load data with bcp]: /sql/tools/bcp-utility
[Load data with PolyBase]: ./load-data-wideworldimportersdw.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Scale compute resources]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/20../../choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  https://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/20../../azure-sql-data-warehouse-loading-patterns-and-strategies/
