---
title: INSERIR limitações de instrução | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299996"
---
# <a name="insert-statement-limitations"></a>Limitações da instrução INSERT
Os dados inseridos são truncados à direita sem aviso se for muito longo para caber na coluna.  
  
 A tentativa de inserir um valor fora do intervalo do tipo de dados de uma coluna faz com que um NULL seja inserido na coluna.  
  
 Quando um dBASE, Microsoft Excel, Paradox ou Textdriver é usado, inserir uma string de comprimento zero em uma coluna realmente insere um NULL.  
  
 Quando o driver do Microsoft Excel é usado, se uma seqüência de string vazia for inserida em uma coluna, a seqüência de string vazia será convertida em UM NULL; uma declaração SELECT pesquisada que é executada com uma seqüência de string vazia na cláusula WHERE não terá sucesso nessa coluna.  
  
 Uma tabela não é updatable pelo motorista do Paradoxo sob duas condições:  
  
-   Quando um índice único não é definido na tabela. Isso não é verdade para uma tabela vazia, que pode ser atualizada com uma única linha, mesmo que um índice único não seja definido na tabela. Se uma única linha for inserida em uma tabela vazia que não tenha um índice único, um aplicativo não poderá criar um índice único ou inserir dados adicionais após a inserção da linha única.  
  
-   Se o Borland Database Engine não for implementado, somente serão permitidas instruções de leitura e apêndice na tabela Paradoxo.  
  
 Quando o driver de texto é usado, os valores NULL são representados por uma seqüência de string acolchoada em branco em arquivos de comprimento fixo, mas são representados por nenhum espaço em arquivos delimitados. Por exemplo, na seguinte linha contendo três campos, o segundo campo é um valor NULL:  
  
```  
"Smith:,, 123  
```  
  
 Quando o driver texto é usado, todos os valores da coluna podem ser acolchoados com espaços de liderança. O comprimento de qualquer linha deve ser menor ou igual a 65.543 bytes.
