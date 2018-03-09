---
title: "Limitações de instrução de inserção | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c8547de55d04aefbd3c847fca9b53b411b5ee80
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="insert-statement-limitations"></a>Limitações de instrução de inserção
Dados inseridos são truncados à direita sem aviso se ele é muito longo para caber na coluna.  
  
 Tentativa de inserir um valor que está fora do intervalo do tipo de dados da coluna faz com que um nulo a ser inserido na coluna.  
  
 Quando é usado um dBASE, Microsoft Excel, Paradox ou Textdriver, inserindo uma cadeia de caracteres de comprimento zero em uma coluna, na verdade, insere um valor nulo em vez disso.  
  
 Quando o driver do Microsoft Excel é usado, se uma cadeia de caracteres vazia é inserida em uma coluna, a cadeia de caracteres vazia é convertida em um valor nulo; uma instrução SELECT pesquisada que é executada com uma cadeia de caracteres vazia na cláusula WHERE não terá êxito nessa coluna.  
  
 Uma tabela não é atualizável pelo driver Paradox sob duas condições:  
  
-   Quando um índice exclusivo não está definido na tabela. Isso não é verdade para uma tabela vazia, o que pode ser atualizada com uma única linha, mesmo se um índice exclusivo não está definido na tabela. Se uma única linha é inserida em uma tabela vazia que não tem um índice exclusivo, um aplicativo não é possível criar um índice exclusivo ou inserir dados adicionais após a linha foi inserida.  
  
-   Se o mecanismo de banco de dados Borland não for implementado, somente leitura e acrescentar instruções são permitidas na tabela Paradox.  
  
 Quando o driver de texto é usado, valores nulos são representados por uma cadeia de caracteres preenchida em branco em arquivos de comprimento fixo, mas são representados por nenhum espaço em arquivos delimitados. Por exemplo, na linha seguinte que contém três campos, o segundo campo é um valor NULL:  
  
```  
"Smith:,, 123  
```  
  
 Quando o driver de texto é usado, todos os valores de coluna podem ser preenchidos com espaços à esquerda. O comprimento de qualquer linha deve ser menor ou igual a 65,543 bytes.
