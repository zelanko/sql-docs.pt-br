---
title: Inserindo linhas com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05b8f71d6f4c885c7dc64887dd92b1f600005ca7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138919"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserir linhas com SQLBulkOperations
Inserindo dados com **SQLBulkOperations** é semelhante à atualização de dados com **SQLBulkOperations** porque ele usa dados dos buffers de associadas de aplicativo.  
  
 Para que cada coluna na nova linha tem um valor, todos vinculados colunas com um valor de comprimento/indicador de SQL_COLUMN_IGNORE e todas as colunas desassociadas devem aceitar valores nulos ou ter um padrão.  
  
 Para inserir linhas com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Define o atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem inseridas e coloca os novos valores de dados nos buffers associadas de aplicativo. Para obter informações sobre como enviar dados longos com **SQLBulkOperations**, consulte [dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas a buffers de cadeia de caracteres, o tamanho de bytes dos dados para colunas associadas a buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL. O aplicativo define o valor no buffer de comprimento/indicador das colunas que devem ser definidos no padrão (se houver) ou nulo (se não existir um organograma) para SQL_COLUMN_IGNORE.  
  
3.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_ADD.  
  
 Após **SQLBulkOperations** retorna, a linha atual é alterada. Se a coluna de indicador (coluna 0) é associada, **SQLBulkOperations** retorna os indicadores das linhas inseridas no buffer de conjunto de linhas associados a essa coluna.
