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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088200"
---
# <a name="update-statement-limitations"></a>Limitações da instrução UPDATE
Para que o driver do Paradox atualize uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o Borland Mecanismo de Banco de Dados, não é possível atualizar uma tabela do Paradox.  
  
 Não há suporte para o driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é considerada oficialmente suportada pelo driver do Microsoft Excel. Somente a instrução INSERT é considerada suportada.
