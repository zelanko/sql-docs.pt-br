---
title: SQLrowCount | Microsoft Docs
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
ms.openlocfilehash: 3cfb76dbd1732e32238c484f589d3b4696ff89d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302293"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando matrizes de valores de parâmetro são associadas para execução de instrução, **SQLRowCount** retornará SQL_ERROR se qualquer linha de valores de parâmetro gerar uma condição de erro na execução da instrução. Nenhum valor é retornado pelo argumento *RowCountPtr* da função.  
  
 O aplicativo pode tirar proveito do atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para capturar o número de parâmetros processados antes de ocorrer o erro.  
  
 Além disso, o aplicativo pode usar uma matriz de valores de status, associada usando o atributo da instrução SQL_ATTR_PARAM_STATUS_PTR, para capturar os deslocamentos de matriz de linhas de parâmetro incorretas. O aplicativo pode atravessar a matriz de status para determinar o número real de linhas processadas.  
  
 Quando [!INCLUDE[tsql](../../includes/tsql-md.md)] uma instrução INSERT, UPDATE, DELETE ou MERGE com uma cláusula OUTPUT for executada, o SQLRowCount não retornará a contagem das linhas afetadas até que todas as linhas no conjunto de resultados gerados pela cláusula OUTPUT tenham sido consumidas. Para consumir essas linhas, você chama SQLFetch ou SQLFetchScroll. SQLResultCols retornará -1 até que todas as linhas de resultado tenham sido consumidas. Depois que SQLFetch ou SQLFetchScroll retornar SQL_NO_DATA, o aplicativo deve ligar para o SQLRowCount para determinar o número de linhas afetadas antes de chamar o SQLMoreResults para passar para o próximo resultado.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLrowcount](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
