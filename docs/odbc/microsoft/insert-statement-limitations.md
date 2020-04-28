---
title: Limitações da instrução INSERT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299996"
---
# <a name="insert-statement-limitations"></a>Limitações da instrução INSERT
Os dados inseridos são truncados à direita sem aviso se é muito longo para caber na coluna.  
  
 A tentativa de inserir um valor que está fora do intervalo do tipo de dados de uma coluna faz com que um NULL seja inserido na coluna.  
  
 Quando um dBASE, o Microsoft Excel, o Paradox ou o textdriver é usado, a inserção de uma cadeia de caracteres de comprimento zero em uma coluna insere, na verdade, um NULL.  
  
 Quando o driver do Microsoft Excel for usado, se uma cadeia de caracteres vazia for inserida em uma coluna, a cadeia de caracteres vazia será convertida em NULL; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá sucesso nessa coluna.  
  
 Uma tabela não é atualizável pelo driver do Paradox em duas condições:  
  
-   Quando um índice exclusivo não está definido na tabela. Isso não é verdadeiro para uma tabela vazia, que pode ser atualizada com uma única linha, mesmo que um índice exclusivo não esteja definido na tabela. Se uma única linha for inserida em uma tabela vazia que não tem um índice exclusivo, um aplicativo não poderá criar um índice exclusivo ou inserir dados adicionais depois que a linha única tiver sido inserida.  
  
-   Se o Borland Mecanismo de Banco de Dados não for implementado, somente instruções Read e Append serão permitidas na tabela do Paradox.  
  
 Quando o driver de texto é usado, os valores nulos são representados por uma cadeia de caracteres preenchida em branco em arquivos de comprimento fixo, mas são representados sem espaços em arquivos delimitados. Por exemplo, na linha a seguir contendo três campos, o segundo campo é um valor nulo:  
  
```  
"Smith:,, 123  
```  
  
 Quando o driver de texto é usado, todos os valores de coluna podem ser preenchidos com espaços à esquerda. O comprimento de qualquer linha deve ser menor ou igual a 65.543 bytes.
