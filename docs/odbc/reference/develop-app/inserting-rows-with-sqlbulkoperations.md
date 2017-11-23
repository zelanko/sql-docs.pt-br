---
title: Inserindo linhas com SQLBulkOperations | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 854db50773ce22ec96641cbb6848fe8884b0c61c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserindo linhas com SQLBulkOperations
Inserindo dados com **SQLBulkOperations** é semelhante à atualização de dados com **SQLBulkOperations** porque ele usa dados dos buffers de aplicativo associado.  
  
 Para que cada coluna na nova linha tem um valor, todos vinculados colunas com um valor de comprimento/indicador de SQL_COLUMN_IGNORE e todas as colunas desassociadas devem aceitar valores nulos ou ter um padrão.  
  
 Para inserir linhas com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Define o atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem inseridas e coloca os novos valores de dados em buffers do aplicativo associado. Para obter informações sobre como enviar dados longos com **SQLBulkOperations**, consulte [dados longos e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor do buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas aos buffers de cadeia de caracteres, o comprimento de bytes de dados para colunas vinculadas buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL. O aplicativo define o valor do buffer de comprimento/indicador das colunas que devem ser definidas para seu padrão (se houver) ou nulo (se não) a SQL_COLUMN_IGNORE.  
  
3.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_ADD.  
  
 Depois de **SQLBulkOperations** retorna, a linha atual é alterada. Se a coluna de indicador (coluna 0) é associada, **SQLBulkOperations** retorna os indicadores das linhas inseridas no buffer de linhas associados a essa coluna.
