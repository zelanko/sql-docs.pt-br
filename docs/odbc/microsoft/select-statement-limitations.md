---
title: Limitações da instrução SELECT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987855"
---
# <a name="select-statement-limitations"></a>Limitações da instrução SELECT
Uma coluna de função de agregação não pode ser misturada com uma coluna de não agregação em uma instrução SELECT.  
  
 Lista de seleção de uma instrução SELECT que tem uma cláusula GROUP BY só pode ter expressões da cláusula GROUP BY ou funções do conjunto.  
  
 Não há suporte para o uso de um asterisco (para selecionar todas as colunas) em uma instrução SELECT que contém uma cláusula GROUP BY. Os nomes das colunas a ser selecionado devem ser especificados.  
  
 Não há suporte para o uso de uma barra vertical em uma instrução SELECT. Use um parâmetro na instrução SELECT, se você precisar fazer referência a um valor de dados que contém uma barra vertical.  
  
 Ao usar um alias de coluna em uma instrução SELECT, a palavra "como" deve preceder o alias. Por exemplo, "SELECT col1 como um de b." Sem o "como", a instrução retornará um erro.  
  
 Se um nome de coluna incorreto está inserido em uma instrução SELECT, será retornado um erro SQLSTATE 07001, "Número de parâmetros incorretos," em vez de um erro SQLSTATE S0022, "coluna não encontrada."  
  
 Quando o driver do Microsoft Excel é usado, se uma cadeia de caracteres vazia é inserida em uma coluna, a cadeia de caracteres vazia é convertida em um valor nulo; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá êxito nessa coluna.
