---
title: LIMITAÇÕES DE DECLARAÇÃO DE ATUALIZAÇÃO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307617"
---
# <a name="update-statement-limitations"></a>Limitações da instrução UPDATE
Para que o driver Paradox atualize uma tabela, a tabela deve ter um índice único (chave primária paradoxo). Quando você usa o driver Paradox sem implementar o Borland Database Engine, não é possível atualizar uma tabela Paradox.  
  
 Não suportado pelo driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a declaração UPDATE não é considerada oficialmente suportada pelo driver do Microsoft Excel. Apenas a instrução INSERT é considerada suportada.
