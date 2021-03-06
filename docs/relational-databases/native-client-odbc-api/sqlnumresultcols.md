---
description: SQLNumResultCols
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9931959038f84b34b1e9cac28db721c7ef7623e9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485038"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para instruções executadas, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não visita o servidor para informar o número de colunas em um conjunto de resultados. Nesse caso, **SQLNumResultCols** não provoca uma viagem de ida e volta ao servidor. Como [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) e [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), chamar **SQLNumResultCols** em instruções preparadas mas não executadas gera uma viagem de ida e volta ao servidor.  
  
 Quando uma instrução ou lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna vários conjuntos de linha como resultado, é possível que o número de colunas do conjunto de resultados seja alterado de um conjunto para o outro. **SQLNumResultCols** deve ser chamado para cada conjunto. Quando o número de colunas é alterado, o aplicativo deve associar novamente os valores de dados antes de buscar resultados de linha. Para obter mais informações sobre como manipular vários retornos de conjunto de resultados, consulte [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Melhorias no mecanismo de banco de dados começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLNumResultCols para obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados pelo SQLNumResultCols em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLNumResultCols](../../odbc/reference/syntax/sqlnumresultcols-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
