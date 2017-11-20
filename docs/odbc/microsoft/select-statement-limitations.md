---
title: "Limitações da instrução SELECT | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53b3e18a07e14e6059a9d193d8659a09b87e6c65
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="select-statement-limitations"></a>Limitações da instrução SELECT
Uma coluna de função de agregação não pode ser misturada a uma coluna de não agregação em uma instrução SELECT.  
  
 Lista de seleção de uma instrução SELECT com uma cláusula GROUP BY só pode ter expressões da cláusula GROUP BY ou funções do conjunto.  
  
 Não há suporte para o uso de um asterisco (para selecionar todas as colunas) em uma instrução SELECT que contém uma cláusula GROUP BY. Os nomes de colunas a serem selecionadas devem ser especificados.  
  
 Não há suporte para o uso de uma barra vertical em uma instrução SELECT. Use um parâmetro na instrução SELECT, se você precisar fazer referência a um valor de dados que contém uma barra vertical.  
  
 Ao usar um alias de coluna em uma instrução SELECT, a palavra "como" deve preceder o alias. Por exemplo, "SELECT col1 como um de b." Sem o "como", a instrução retornará um erro.  
  
 Se um nome de coluna incorreto for inserido em uma instrução SELECT, será retornado um erro SQLSTATE 07001, "Número de parâmetros incorretos," em vez de um erro SQLSTATE S0022, "coluna não encontrada."  
  
 Quando o driver do Microsoft Excel é usado, se uma cadeia de caracteres vazia é inserida em uma coluna, a cadeia de caracteres vazia é convertida em um valor nulo; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá êxito nessa coluna.

