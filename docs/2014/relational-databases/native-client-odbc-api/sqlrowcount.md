---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: rothja
ms.author: jroth
ms.openlocfilehash: 410023d960bad6dde1060a509cc1bf46f67d77cc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021705"
---
# <a name="sqlrowcount"></a>SQLRowCount
  Quando as matrizes de valores de parâmetro são associadas à execução da instrução, o `SQLRowCount` retorna SQL_ERROR se qualquer linha de valores de parâmetro gera uma condição de erro na execução da instrução. Nenhum valor é retornado pelo argumento *RowCountPtr* da função.  
  
 O aplicativo pode tirar proveito do atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para capturar o número de parâmetros processados antes de ocorrer o erro.  
  
 Além disso, o aplicativo pode usar uma matriz de valores de status, associada usando o atributo da instrução SQL_ATTR_PARAM_STATUS_PTR, para capturar os deslocamentos de matriz de linhas de parâmetro incorretas. O aplicativo pode atravessar a matriz de status para determinar o número real de linhas processadas.  
  
 Quando uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução INSERT, Update, Delete ou Merge com uma cláusula OUTPUT é executada, SQLRowCount não retornará a contagem de linhas afetadas até que todas as linhas do conjunto de resultados geradas pela cláusula OUTPUT tenham sido consumidas. Para sconsume essas linhas, você chama SQLFetch ou SQLFetchScroll. SQLResultCols retornará-1 até que todas as linhas de resultado tenham sido consumidas. Depois que SQLFetch ou SQLFetchScroll retorna SQL_NO_DATA, o aplicativo deve chamar SQLRowCount para determinar o número de linhas afetadas antes de chamar SQLMoreResults para mover para o próximo resultado.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLRowCount](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
