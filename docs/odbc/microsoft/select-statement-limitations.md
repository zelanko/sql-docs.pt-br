---
title: Limitações de instrução SELECT | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987855"
---
# <a name="select-statement-limitations"></a>Limitações da instrução SELECT
Uma coluna de função de agregação não pode ser misturada com uma coluna não agregada em uma instrução SELECT.  
  
 A lista de seleção de uma instrução SELECT que tem uma cláusula GROUP BY só pode ter expressões da cláusula GROUP BY ou funções set.  
  
 Não há suporte para o uso de um asterisco (para selecionar todas as colunas) em uma instrução SELECT que contenha uma cláusula GROUP BY. Os nomes das colunas a serem selecionadas devem ser especificados.  
  
 Não há suporte para o uso de uma barra vertical em uma instrução SELECT. Use um parâmetro na instrução SELECT se você precisar fazer referência a um valor de dados que contém uma barra vertical.  
  
 Ao usar um alias de coluna em uma instrução SELECT, a palavra "as" deve preceder o alias. Por exemplo, "selecionar col1 como a partir de b". Sem o "as", a instrução retornará um erro.  
  
 Se um nome de coluna incorreto for inserido em uma instrução SELECT, um erro SQLSTATE 07001, "número incorreto de parâmetros", será retornado em vez de um erro de S0022 de SQLSTATE, "coluna não encontrada".  
  
 Quando o driver do Microsoft Excel for usado, se uma cadeia de caracteres vazia for inserida em uma coluna, a cadeia de caracteres vazia será convertida em NULL; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá sucesso nessa coluna.
