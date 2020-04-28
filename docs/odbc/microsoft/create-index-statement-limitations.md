---
title: Limitações da instrução CREATE INDEX | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280877"
---
# <a name="create-index-statement-limitations"></a>Limitações da instrução CREATE INDEX
Não há suporte para a instrução CREATE INDEX para os drivers de texto ou do Microsoft Excel.  
  
 Um índice pode ser definido em um máximo de 10 colunas. Se mais de 10 colunas forem incluídas em uma instrução CREATE INDEX, o índice não será reconhecido e a tabela será tratada como embora nenhum índice tenha sido criado.  
  
 O driver do dBASE não pode criar um índice em uma coluna lógica.  
  
 Quando o driver do dBASE é usado, o tempo de resposta em arquivos grandes pode ser melhorado com a criação de um índice. MDX (ou. ndx) na coluna (campo) especificada nas cláusulas WHERE de uma instrução SELECT. Os índices. MDX existentes serão aplicados automaticamente para os operadores =, \<>,, >=, =< e between em uma cláusula WHERE e como predicados, bem como em predicados de junção.  
  
 Quando o driver do dBASE é usado, o índice criado por uma instrução CREATE UNIQUE INDEX é, na verdade, não exclusivo, e valores duplicados podem ser inseridos na coluna indexada. Somente um registro de um conjunto com valores de chave idênticos pode ser adicionado ao índice.  
  
 Quando o driver do Paradox é usado, um índice exclusivo deve ser definido em um subconjunto contíguo das colunas em uma tabela, incluindo a primeira coluna. Uma tabela não poderá ser atualizada pelo driver do Paradox se um índice exclusivo não estiver definido na tabela ou quando o driver do Paradox for usado sem a implementação do Mecanismo de Banco de Dados Borland.
