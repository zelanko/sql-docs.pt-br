---
title: CRIAR ÍNDICE para Paradoxo | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280906"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX para Paradox
A sintaxe da declaração CREATE INDEX para o driver ODBC Paradox é:  
  
 **CRIAR** [**ÚNICO** **]** *INDEX-nome*  
  
 **ON** *nome da mesa*  
  
 **(** *identificador de colunas* **(ASC)**  
  
 [**,** *identificador de coluna* **[ASC**]...] **)**  
  
 O driver ODBC Paradox não suporta a palavra-chave **DESC** na gramática ODBC SQL para a declaração CREATE INDEX. O argumento *nome da tabela* pode especificar o caminho completo da tabela.  
  
 Se a palavra-chave **UNIQUE** for especificada, o driver ODBC Paradox criará um índice único. O primeiro índice único é criado como um índice primário. Este é um arquivo de chave primária paradoxo chamado *nome de tabela*. Px. Os índices primários estão sujeitos às seguintes restrições:  
  
-   O índice primário deve ser criado antes que quaisquer linhas sejam adicionadas à tabela.  
  
-   Um índice primário deve ser definido nas primeiras colunas "n" em uma tabela.  
  
-   Apenas um índice primário é permitido por tabela.  
  
-   Uma tabela não pode ser atualizada pelo driver Paradoxo se um índice primário não for definido na tabela. (Observe que isso não é verdade para uma tabela vazia, que pode ser atualizada mesmo que um índice único não seja definido na tabela.)  
  
-   O argumento *do nome do índice* para um índice primário deve ser o mesmo que o nome base da tabela, conforme exigido por Paradoxo.  
  
 Se a palavra-chave **UNIQUE** for omitida, o driver ODBC Paradox criará um índice não único. Isso consiste em dois arquivos de índice secundário paradoxo chamados *de nome de tabela*. X*nn* e *nome de mesa*. Y*nn*, onde *nn* é o número da coluna na tabela. Índices não únicos estão sujeitos às seguintes restrições:  
  
-   Antes que um índice não único possa ser criado para uma tabela, um índice primário deve existir para essa tabela.  
  
-   Paradoxo 3. *x*, o argumento *de nome de índice* para qualquer índice que não seja um índice primário (único ou não único) deve ser o mesmo que o nome da coluna. Paradoxo 4. *x* e 5. *x*, o nome de tal índice pode ser, mas não precisa ser, o mesmo que o nome da coluna.  
  
-   Apenas uma coluna pode ser especificada para um índice não único.  
  
 As colunas não podem ser adicionadas uma vez que um índice tenha sido definido em uma tabela. Se a primeira coluna da lista de argumentos de uma declaração CREATE TABLE criar um índice, uma segunda coluna não poderá ser incluída na lista de argumentos.  
  
 Por exemplo, para usar o número da ordem de venda e as colunas de número de linha como o índice único na tabela SO_LINES, use a declaração:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar a coluna de número de peça como um índice não único na tabela SO_LINES, use a declaração:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Observe que quando duas instruções CREATE INDEX são realizadas, a primeira instrução sempre criará um índice primário com o mesmo nome da tabela e a segunda instrução sempre criará um índice não único com o mesmo nome da coluna. Esses índices serão nomeados desta forma, mesmo que diferentes nomes sejam inseridos nas demonstrações do CREATE INDEX e mesmo se o índice for rotulado COMO ÚNICO na segunda declaração DE ÍNDICE CREATE.  
  
> [!NOTE]  
>  Quando você usa o driver Paradox sem implementar o Borland Database Engine, somente são permitidas instruções de leitura e apêndice.
