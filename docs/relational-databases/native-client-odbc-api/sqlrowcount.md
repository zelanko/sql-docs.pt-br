---
description: SQLRowCount
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11156b3b3080c537f1fb65eee081632ce7f3c1e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423958"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Quando matrizes de valores de parâmetro são associadas para execução de instrução, **SQLRowCount** retornará SQL_ERROR se qualquer linha de valores de parâmetro gerar uma condição de erro na execução da instrução. Nenhum valor é retornado pelo argumento *RowCountPtr* da função.  
  
 O aplicativo pode tirar proveito do atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para capturar o número de parâmetros processados antes de ocorrer o erro.  
  
 Além disso, o aplicativo pode usar uma matriz de valores de status, associada usando o atributo da instrução SQL_ATTR_PARAM_STATUS_PTR, para capturar os deslocamentos de matriz de linhas de parâmetro incorretas. O aplicativo pode atravessar a matriz de status para determinar o número real de linhas processadas.  
  
 Quando uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução INSERT, Update, Delete ou Merge com uma cláusula OUTPUT é executada, SQLRowCount não retornará a contagem de linhas afetadas até que todas as linhas do conjunto de resultados geradas pela cláusula OUTPUT tenham sido consumidas. Para sconsume essas linhas, você chama SQLFetch ou SQLFetchScroll. SQLResultCols retornará-1 até que todas as linhas de resultado tenham sido consumidas. Depois que SQLFetch ou SQLFetchScroll retorna SQL_NO_DATA, o aplicativo deve chamar SQLRowCount para determinar o número de linhas afetadas antes de chamar SQLMoreResults para mover para o próximo resultado.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLRowCount](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
