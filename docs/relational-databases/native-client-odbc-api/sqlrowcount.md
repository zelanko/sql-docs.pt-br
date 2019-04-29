---
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13a1019d2781ea71f5f1017051f113a985f989be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014148"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando matrizes de valores de parâmetro são associadas para execução de instrução, **SQLRowCount** retornará SQL_ERROR se qualquer linha de valores de parâmetro gerar uma condição de erro na execução da instrução. Nenhum valor é retornado pelo argumento *RowCountPtr* da função.  
  
 O aplicativo pode tirar proveito do atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para capturar o número de parâmetros processados antes de ocorrer o erro.  
  
 Além disso, o aplicativo pode usar uma matriz de valores de status, associada usando o atributo da instrução SQL_ATTR_PARAM_STATUS_PTR, para capturar os deslocamentos de matriz de linhas de parâmetro incorretas. O aplicativo pode atravessar a matriz de status para determinar o número real de linhas processadas.  
  
 Quando um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução INSERT, UPDATE, DELETE ou MERGE com uma cláusula OUTPUT for executada, SQLRowCount não retornará a contagem de linhas afetadas até que todas as linhas no conjunto de resultados gerado pela cláusula OUTPUT tenham sido consumidas. Para consumir essas linhas, você chamará SQLFetch ou SQLFetchScroll. SQLResultCols retornará -1 até que todas as linhas de resultados tenham sido consumidas. Depois de SQLFetch ou SQLFetchScroll retorna SQL_NO_DATA, o aplicativo deve chamar SQLRowCount para determinar o número de linhas afetadas antes de chamar SQLMoreResults para mover para o próximo resultado.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLRowCount](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
