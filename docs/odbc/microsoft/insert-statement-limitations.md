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
manager: craigg
ms.openlocfilehash: 26d4be96ca4dabebd93ee96e2888e18d39257412
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610334"
---
# <a name="insert-statement-limitations"></a>Limitações da instrução INSERT
Dados inseridos serão truncados à direita sem aviso, se ele é grande demais para caber na coluna.  
  
 A tentativa de inserir um valor que está fora do intervalo da coluna tipo de dados faz com que um nulo a ser inserido na coluna.  
  
 Quando é usado um dBASE, Microsoft Excel, Paradox ou Textdriver, inserindo uma cadeia de caracteres de comprimento zero em uma coluna, na verdade, insere um valor nulo em vez disso.  
  
 Quando o driver do Microsoft Excel é usado, se uma cadeia de caracteres vazia é inserida em uma coluna, a cadeia de caracteres vazia é convertida em um valor nulo; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá êxito nessa coluna.  
  
 Uma tabela não é atualizável pelo driver do Paradox em duas condições:  
  
-   Quando um índice exclusivo não está definido na tabela. Isso não é verdadeiro para uma tabela vazia, o que pode ser atualizada com uma única linha, mesmo se um índice exclusivo não está definido na tabela. Se uma única linha é inserida em uma tabela vazia que não tem um índice exclusivo, um aplicativo não é possível criar um índice exclusivo ou inserir dados adicionais depois que a única linha foi inserida.  
  
-   Se o mecanismo de banco de dados Borland não for implementado, somente leitura e acrescentar instruções são permitidas na tabela Paradox.  
  
 Quando o driver de texto é usado, valores nulos são representados por uma cadeia de caracteres preenchida de espaço em branco nos arquivos de comprimento fixo, mas são representadas por nenhum espaço em arquivos delimitados. Por exemplo, na linha a seguir que contém três campos, o segundo campo é um valor nulo:  
  
```  
"Smith:,, 123  
```  
  
 Quando o driver de texto é usado, todos os valores de coluna podem ser preenchidos com espaços à esquerda. O comprimento de qualquer linha deve ser menor ou igual a 65,543 bytes.
