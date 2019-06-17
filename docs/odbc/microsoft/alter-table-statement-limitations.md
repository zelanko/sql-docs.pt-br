---
title: Limitações da instrução ALTER tabela | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02ce530385cdc911250a81d831dd2fdb81873f76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301982"
---
# <a name="alter-table-statement-limitations"></a>Limitações da instrução ALTER TABLE
Quando o driver do Paradox ou dBASE for usado, depois que um índice foi criado e adicionado um novo registro, a estrutura da tabela não pode ser alterada pela instrução ALTER TABLE, a menos que o índice é descartado e o conteúdo da tabela será excluído.  
  
 Não há suporte para as instruções ALTER TABLE para os drivers do Microsoft Excel ou texto.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não há suporte para as instruções ALTER TABLE; somente leitura e acrescentar instruções são permitidas.
