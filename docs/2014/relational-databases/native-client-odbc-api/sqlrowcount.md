---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b1fc405b091f29c4d2660fc554fbbad47a7fdec
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431855"
---
# <a name="sqlrowcount"></a>SQLRowCount
  Quando matrizes de valores de parâmetro são associadas para execução da instrução, `SQLRowCount` retornará SQL_ERROR se qualquer linha de valores de parâmetro gerar uma condição de erro na execução da instrução. Nenhum valor é retornado pelo argumento *RowCountPtr* da função.  
  
 O aplicativo pode tirar proveito do atributo da instrução SQL_ATTR_PARAMS_PROCESSED_PTR para capturar o número de parâmetros processados antes de ocorrer o erro.  
  
 Além disso, o aplicativo pode usar uma matriz de valores de status, associada usando o atributo da instrução SQL_ATTR_PARAM_STATUS_PTR, para capturar os deslocamentos de matriz de linhas de parâmetro incorretas. O aplicativo pode atravessar a matriz de status para determinar o número real de linhas processadas.  
  
 Quando um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução INSERT, UPDATE, DELETE ou MERGE com uma cláusula OUTPUT for executada, SQLRowCount não retornará a contagem de linhas afetadas até que todas as linhas no conjunto de resultados gerado pela cláusula OUTPUT tenham sido consumidas. Para consumir essas linhas, você chamará SQLFetch ou SQLFetchScroll. SQLResultCols retornará -1 até que todas as linhas de resultados tenham sido consumidas. Depois de SQLFetch ou SQLFetchScroll retorna SQL_NO_DATA, o aplicativo deve chamar SQLRowCount para determinar o número de linhas afetadas antes de chamar SQLMoreResults para mover para o próximo resultado.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLRowCount](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
