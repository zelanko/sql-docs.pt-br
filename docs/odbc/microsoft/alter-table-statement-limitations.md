---
title: LIMITAÇÕES DA DECLARAÇÃO DA TABELA ALTER | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304695"
---
# <a name="alter-table-statement-limitations"></a>Limitações da instrução ALTER TABLE
Quando o driver dBASE ou Paradox é usado, uma vez que um índice foi criado e um novo registro adicionado, a estrutura da tabela não pode ser alterada pela declaração ALTER TABLE, a menos que o índice seja descartado e o conteúdo da tabela seja excluído.  
  
 As instruções ALTER TABLE não são suportadas para os drivers Microsoft Excel ou Text.  
  
> [!NOTE]  
>  Quando você usa o driver Paradox sem implementar o Borland Database Engine, as instruções ALTER TABLE não são suportadas; apenas declarações de leitura e apêndice são permitidas.
