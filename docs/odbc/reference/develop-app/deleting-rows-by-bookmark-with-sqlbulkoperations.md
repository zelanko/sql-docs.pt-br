---
title: Excluindo linhas por indicador com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43a4df5ba921cba83d51ce6cfab34bfe32ee98ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Excluindo linhas por indicador com SQLBulkOperations
Ao excluir uma linha pelo indicador, **SQLBulkOperations** faz com que a fonte de dados exclua uma ou mais linhas selecionadas da tabela. As linhas são identificadas pelo indicador em uma coluna de indicador associado.  
  
 Para excluir linhas por indicador com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem excluídos. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de indicadores e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Chamadas **SQLBulkOperations** com *operação* definido como SQL_DELETE_BY_BOOKMARK.
