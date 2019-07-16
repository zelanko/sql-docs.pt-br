---
title: Limitações da instrução UPDATE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088200"
---
# <a name="update-statement-limitations"></a>Limitações da instrução UPDATE
Para o driver do Paradox atualizar uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não é possível atualizar uma tabela Paradox.  
  
 Não tem suporte pelo driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar os valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é considerada oficialmente com suporte pelo driver do Microsoft Excel. Somente a instrução INSERT é considerada com suporte.
