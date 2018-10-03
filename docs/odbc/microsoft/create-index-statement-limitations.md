---
title: Limitações da instrução de índice CREATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec6ba27197f7a6021aff90d30884129128cb3614
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837034"
---
# <a name="create-index-statement-limitations"></a>Limitações da instrução CREATE INDEX
Não há suporte para a instrução CREATE INDEX para os drivers do Microsoft Excel ou texto.  
  
 Um índice pode ser definido em um máximo de 10 colunas. Se mais de 10 colunas são incluídas em uma instrução CREATE INDEX, o índice não será reconhecido e a tabela será tratada como se nenhum índice foi criado.  
  
 O driver do dBASE não é possível criar um índice em uma coluna de lógica.  
  
 Quando o driver do dBASE é usado, o tempo de resposta em arquivos grandes pode ser melhorado pela criação de um índice. MDX (ou ndx) na coluna (campo) especificados nas cláusulas WHERE de uma instrução SELECT. Os índices existentes. MDX serão aplicados automaticamente para =, >, \<, > =, = < e entre os operadores em uma cláusula WHERE e predicados LIKE, bem como em predicados de junção.  
  
 Quando o driver do dBASE é usado, o índice criado por uma instrução CREATE UNIQUE INDEX é, na verdade, não exclusiva, e valores duplicados podem ser inseridos na coluna indexada. Apenas um registro de um conjunto de valores de chave idênticos pode ser adicionado ao índice.  
  
 Quando o driver do Paradox é usado, um índice exclusivo deve ser definido em um subconjunto contíguo das colunas em uma tabela, incluindo a primeira coluna. Uma tabela não pode ser atualizada pelo driver do Paradox se um índice exclusivo não está definido na tabela ou quando o driver do Paradox for usado sem a implementação do mecanismo de banco de dados Borland.
