---
title: SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0e9a03b2e8635618afbdc615a6f77dfe05c533e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302564"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para as instruções [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executadas, o driver ODBC do Cliente Nativo não precisa consultar o servidor para descrever colunas em um conjunto de resultados. Neste caso, **sqldescribecol** não causa uma ida e volta do servidor. Como [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)e[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md), chamar **SQLDescribeCol** em declarações preparadas, mas não executadas, gera uma ida e volta do servidor.  
  
 Quando uma instrução ou um lote de instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna vários conjuntos de linha de resultado, é possível para uma coluna referenciada por ordinal ser originada em uma tabela separada ou consultar uma coluna inteiramente diferente no conjunto de resultados. **SQLDescribeCol** deve ser chamado para cada conjunto. Quando o conjunto de resultados for alterado, o aplicativo deverá associar novamente os valores de dados antes de buscar os resultados da linha. Para obter mais informações sobre como manipular vários retornos de conjunto de resultados, consulte [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Os atributos de coluna são informados somente para o primeiro conjunto de resultados quando vários conjuntos são gerados por um lote preparado de instruções SQL.  
  
 Para tipos de dados de grande valor, o valor devolvido no *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Um valor de SQL_SS_LENGTH_UNLIMITED no *ColumnSizePtr* indica que o tamanho é "ilimitado".  
  
 Melhorias no mecanismo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de banco de dados que começam com permitem que o SQLDescribeCol obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem diferir dos valores retornados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pelo SQLDescribeCol nas versões anteriores de . Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>Suporte de SQLDescribeCol a recursos aprimorados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*DataTypePtr*|*ColumnSizePtr*|*Digitsptr decimal*|  
|-|-------------------|---------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;da ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>Suporte de SQLDescribeCol para CLR UDTs grandes  
 **O SQLDescribeCol** suporta grandes tipos de UDTs (ClR definidos pelo usuário). Para obter mais informações, consulte [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDescribeCol](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
