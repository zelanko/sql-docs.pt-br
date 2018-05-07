---
title: Limitações de instrução de atualização | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 006d0f9644c9f62a6b50e2d327384ec3a9c954c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>Limitações de instrução de atualização
Para o driver Paradox atualizar uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não é possível atualizar uma tabela Paradox.  
  
 Não tem suporte pelo driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar os valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é oficialmente suportado pelo driver do Microsoft Excel. A instrução de inserção é considerada com suporte.
