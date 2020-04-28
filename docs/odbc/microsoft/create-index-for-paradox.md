---
title: CRIAR índice para o Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280906"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX para Paradox
A sintaxe da instrução CREATE INDEX para o driver ODBC Paradox é:  
  
 **Criar** índice de **índice** [**exclusivo**] *-nome*  
  
 **Em nome da** *tabela*  
  
 **(** *identificador de coluna* [**ASC**]  
  
 [**,** *identificador de coluna* [**ASC**]...] **)**  
  
 O driver ODBC do Paradox não oferece suporte à palavra-chave **desc** na gramática do SQL ODBC para a instrução CREATE index. O argumento *table-name* pode especificar o caminho completo da tabela.  
  
 Se a palavra-chave **Unique** for especificada, o driver ODBC do Paradox criará um índice exclusivo. O primeiro índice exclusivo é criado como um índice primário. Este é um arquivo de chave primária do Paradox chamado *table-name*. PX. Os índices primários estão sujeitos às seguintes restrições:  
  
-   O índice primário deve ser criado antes de qualquer linha ser adicionada à tabela.  
  
-   Um índice primário deve ser definido nas primeiras colunas "n" em uma tabela.  
  
-   Somente um índice primário é permitido por tabela.  
  
-   Uma tabela não poderá ser atualizada pelo driver do Paradox se um índice primário não estiver definido na tabela. (Observe que isso não é verdadeiro para uma tabela vazia, que pode ser atualizada mesmo que um índice exclusivo não esteja definido na tabela.)  
  
-   O argumento de *nome de índice* para um índice primário deve ser o mesmo que o nome base da tabela, conforme exigido pelo Paradox.  
  
 Se a palavra-chave **Unique** for omitida, o driver ODBC do Paradox criará um índice não exclusivo. Isso consiste em dois arquivos de índice secundários do Paradox nomeados *table-name*. X*NN* e *nome da tabela*. Y*NN*, em que *NN* é o número da coluna na tabela. Os índices não exclusivos estão sujeitos às seguintes restrições:  
  
-   Antes que um índice não exclusivo possa ser criado para uma tabela, deve existir um índice primário para essa tabela.  
  
-   Para o Paradox 3. *x*, o argumento de *nome de índice* para qualquer índice que não seja um índice primário (exclusivo ou não exclusivo) deve ser igual ao nome da coluna. Para o Paradox 4. *x* e 5. *x*, o nome desse índice pode ser, mas não precisa ser, o mesmo que o nome da coluna.  
  
-   Somente uma coluna pode ser especificada para um índice não exclusivo.  
  
 Não é possível adicionar colunas depois que um índice tiver sido definido em uma tabela. Se a primeira coluna da lista de argumentos de uma instrução CREATE TABLE criar um índice, uma segunda coluna não poderá ser incluída na lista de argumentos.  
  
 Por exemplo, para usar as colunas número da ordem de venda e número da linha como o índice exclusivo na tabela SO_LINES, use a instrução:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar a coluna de número de peça como um índice não exclusivo na tabela SO_LINES, use a instrução:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Observe que, quando duas instruções CREATE INDEX são executadas, a primeira instrução sempre criará um índice primário com o mesmo nome que a tabela e a segunda instrução sempre criará um índice não exclusivo com o mesmo nome que a coluna. Esses índices serão nomeados dessa forma, mesmo se nomes diferentes forem inseridos nas instruções CREATE INDEX e mesmo se o índice for rotulado exclusivo na segunda instrução CREATE INDEX.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o Borland Mecanismo de Banco de Dados, somente instruções Read e Append são permitidas.
