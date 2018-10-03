---
title: CREATE INDEX para Paradox | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e16fb311bf3c9acb2823772247e0fc16eabeef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649044"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX para Paradox
A sintaxe da instrução CREATE INDEX para o driver do Paradox ODBC é:  
  
 **Crie** [**UNIQUE**] **índice** *nome do índice*  
  
 **Diante** *nome de tabela*  
  
 **(** *identificador de coluna* [**ASC**]  
  
 [**,** *identificador de coluna* [**ASC**]...] **)**  
  
 O driver do Paradox ODBC não oferece suporte a **DESC** palavra-chave na gramática SQL ODBC para a instrução CREATE INDEX. O *nome da tabela* argumento pode especificar o caminho completo da tabela.  
  
 Se a palavra-chave **UNIQUE** for especificado, o driver do Paradox ODBC criará um índice exclusivo. O primeiro índice exclusivo é criado como um índice primário. Este é um arquivo de chave primário da Paradox denominado *nome da tabela*. PX. Índices primários estão sujeitos às seguintes restrições:  
  
-   O índice primário deve ser criado antes de todas as linhas são adicionadas à tabela.  
  
-   Um índice primário deve ser definido após as primeiras colunas "n" em uma tabela.  
  
-   Somente um índice primário é permitido por tabela.  
  
-   Uma tabela não pode ser atualizada pelo driver do Paradox se um índice primário não está definido na tabela. (Observe que isso não é verdadeiro para uma tabela vazia, o que pode ser atualizada, mesmo se um índice exclusivo não está definido na tabela.)  
  
-   O *nome do índice* argumento para um índice primário deve ser o mesmo que o nome de base da tabela, conforme exigido pelo Paradox.  
  
 Se a palavra-chave **UNIQUE** é omitido, o driver do Paradox ODBC criará um índice não exclusivo. Isso consiste em dois arquivos de índice secundário Paradox denominados *nome da tabela*. X*nn* e *nome da tabela*. Y*nn*, onde *nn* é o número da coluna na tabela. Índices não exclusivos estão sujeitos às seguintes restrições:  
  
-   Antes de um índice não exclusivo pode ser criado para uma tabela, um índice primário deve existir para essa tabela.  
  
-   Para Paradox 3. *x*, o *nome do índice* argumento para qualquer índice que não seja um índice primário (exclusivo ou não exclusivo) deve ser o mesmo que o nome da coluna. Para Paradox 4. *x* e 5. *x*, o nome de tal índice pode ser, mas não precisa ser o mesmo que o nome da coluna.  
  
-   Apenas uma coluna pode ser especificada para um índice não exclusivo.  
  
 Não não possível adicionar colunas depois que um índice foi definido em uma tabela. Se a primeira coluna da lista de argumentos de uma instrução CREATE TABLE cria um índice, uma segunda coluna não pode ser incluída na lista de argumentos.  
  
 Por exemplo, para usar o número de ordem de venda e colunas de número de linha como o índice exclusivo na tabela SO_LINES, use a instrução:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar a coluna de número de parte como um índice não exclusivo na tabela SO_LINES, use a instrução:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Observe que, quando são executadas duas instruções CREATE INDEX, a primeira instrução sempre criará um índice primário com o mesmo nome que a tabela e a segunda instrução sempre criará um índice não exclusivo com o mesmo nome que a coluna. Esses índices serão nomeados dessa forma, mesmo se nomes diferentes são inseridos nas instruções CREATE INDEX e mesmo se o índice é rotulado como UNIQUE na segunda instrução CREATE INDEX.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, somente leitura e acréscimo instruções são permitidas.
