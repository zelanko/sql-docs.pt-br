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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307617"
---
# <a name="update-statement-limitations"></a>Limitações da instrução UPDATE
Para que o driver do Paradox atualize uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o Borland Mecanismo de Banco de Dados, não é possível atualizar uma tabela do Paradox.  
  
 Não há suporte para o driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é considerada oficialmente suportada pelo driver do Microsoft Excel. Somente a instrução INSERT é considerada suportada.
