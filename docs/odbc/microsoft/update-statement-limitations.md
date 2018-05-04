---
title: Limitações de instrução de atualização | Microsoft Docs
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
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbb1e6cbf0660f7b016391d5881b77d7e89e1f81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>Limitações de instrução de atualização
Para o driver Paradox atualizar uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não é possível atualizar uma tabela Paradox.  
  
 Não tem suporte pelo driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar os valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é oficialmente suportado pelo driver do Microsoft Excel. A instrução de inserção é considerada com suporte.
