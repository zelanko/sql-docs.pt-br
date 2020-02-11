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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085520"
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
