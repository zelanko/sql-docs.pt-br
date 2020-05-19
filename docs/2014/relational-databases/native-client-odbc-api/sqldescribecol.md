---
title: SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dda7c4c0e2ae187f96883a32cac2528eceb90c74
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706294"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  Para instruções executadas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client não precisa consultar o servidor para descrever as colunas em um conjunto de resultados. Nesse caso, o `SQLDescribeCol` não causa um ida e volta do servidor. Como [SQLColAttribute](sqlnumresultcols.md), a chamada em instruções preparadas, `SQLDescribeCol` mas não executadas, gera um ida e volta do servidor.  
  
 Quando uma instrução ou um lote de instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna vários conjuntos de linha de resultado, é possível para uma coluna referenciada por ordinal ser originada em uma tabela separada ou consultar uma coluna inteiramente diferente no conjunto de resultados. `SQLDescribeCol`deve ser chamado para cada conjunto. Quando o conjunto de resultados for alterado, o aplicativo deverá associar novamente os valores de dados antes de buscar os resultados da linha. Para obter mais informações sobre como manipular vários retornos de conjunto de resultados, consulte [SQLMoreResults](sqlmoreresults.md).  
  
 Os atributos de coluna são informados somente para o primeiro conjunto de resultados quando vários conjuntos são gerados por um lote preparado de instruções SQL.  
  
 Para tipos de dados de valor grande, o valor retornado em *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Um valor de SQL_SS_LENGTH_UNLIMITED em *ColumnSizePtr* indica que o tamanho é "ilimitado".  
  
 Melhorias no mecanismo de banco de dados começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLDescribeCol para obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados pelo SQLDescribeCol em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>Suporte de SQLDescribeCol a recursos aprimorados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|data|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>Suporte de SQLDescribeCol para CLR UDTs grandes  
 `SQLDescribeCol` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDescribeCol](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
