---
title: CRIAR Limitações de Declaração de ÍNDICE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280877"
---
# <a name="create-index-statement-limitations"></a>Limitações da instrução CREATE INDEX
A declaração CREATE INDEX não é suportada para os drivers Microsoft Excel ou Text.  
  
 Um índice pode ser definido em um máximo de 10 colunas. Se mais de 10 colunas forem incluídas em uma declaração do CREATE INDEX, o índice não será reconhecido e a tabela será tratada como se nenhum índice fosse criado.  
  
 O driver dBASE não pode criar um índice em uma coluna LOGICAL.  
  
 Quando o driver dBASE é usado, o tempo de resposta em arquivos grandes pode ser melhorado com a construção de um índice .mdx (ou .ndx) na coluna (campo) especificado nas cláusulas WHERE de uma declaração SELECT. Os índices .mdx existentes serão automaticamente aplicados \<para =, >, >=, =< e ENTRE operadores em uma cláusula WHERE, e predicados LIKE, bem como em predicados de adesão.  
  
 Quando o driver dBASE é usado, o índice criado por uma instrução CREATE UNIQUE INDEX é realmente não único, e valores duplicados podem ser inseridos na coluna indexada. Apenas um registro de um conjunto com valores-chave idênticos pode ser adicionado ao índice.  
  
 Quando o driver Paradox é usado, um índice único deve ser definido em um subconjunto contíguo das colunas em uma tabela, incluindo a primeira coluna. Uma tabela não pode ser atualizada pelo driver Paradox se um índice único não for definido na tabela ou quando o driver Paradox for usado sem a implementação do Borland Database Engine.
