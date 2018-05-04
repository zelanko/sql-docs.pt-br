---
title: Criar índice para Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b0f8cb298dd62faee4c562943477ea0bd022a45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-for-paradox"></a>Criar índice para Paradox
A sintaxe da instrução CREATE INDEX para o driver ODBC Paradox é:  
  
 **CRIAR** [**UNIQUE**] **índice** *nome do índice*  
  
 **ON** *nome de tabela*  
  
 **(** *identificador de coluna* [**ASC**]  
  
 [**,** *identificador de coluna* [**ASC**]...] **)**  
  
 O driver ODBC Paradox não dá suporte a **DESC** palavra-chave na gramática do ODBC SQL para a instrução CREATE INDEX. O *nome de tabela* argumento pode especificar o caminho completo da tabela.  
  
 Se a palavra-chave **UNIQUE** for especificado, o driver ODBC Paradox criará um índice exclusivo. O primeiro índice exclusivo é criado como um índice primário. Este é um arquivo de chave primário da Paradox denominado *nome de tabela*. PX. Índices primários estão sujeitas às seguintes restrições:  
  
-   O índice principal deve ser criado antes que as linhas são adicionadas à tabela.  
  
-   Um índice primário deve ser definido após as primeiras colunas "n" em uma tabela.  
  
-   Somente um índice primário é permitido por tabela.  
  
-   Uma tabela não pode ser atualizada pelo driver Paradox se um índice primário não está definido na tabela. (Observe que isso não é válido para uma tabela vazia, o que pode ser atualizada, mesmo se um índice exclusivo não está definido na tabela).  
  
-   O *nome do índice* argumento para um índice primário deve ser igual ao nome de base da tabela, conforme exigido pelo Paradox.  
  
 Se a palavra-chave **UNIQUE** for omitido, o driver ODBC Paradox criará um índice não exclusivo. Isso consiste em dois arquivos de índice secundário Paradox denominados *nome de tabela*. X*nn* e *nome de tabela*. Y*nn*, onde *nn* é o número da coluna na tabela. Índices não exclusivos estão sujeitas às seguintes restrições:  
  
-   Antes de um índice não exclusivo pode ser criado para uma tabela, um índice primário deve existir para essa tabela.  
  
-   Para o Paradox 3. *x*, o *nome do índice* argumento para qualquer índice que não seja um índice primário (exclusivo ou não exclusivo) deve ser o mesmo que o nome da coluna. Para o Paradox 4. *x* e 5. *x*, o nome de um índice pode ser, mas não precisa ser o mesmo que o nome da coluna.  
  
-   Somente uma coluna pode ser especificada para um índice não exclusivo.  
  
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
  
 Observe que, quando são executadas duas instruções CREATE INDEX, a primeira instrução sempre criará um índice primário com o mesmo nome que a tabela e a segunda instrução sempre criará um índice não exclusivo com o mesmo nome de coluna. Esses índices serão nomeados dessa forma, mesmo se nomes diferentes são inseridos nas instruções CREATE INDEX e mesmo se o índice é rotulado como UNIQUE na segunda instrução CREATE INDEX.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, somente leitura e acrescente as instruções são permitidas.
