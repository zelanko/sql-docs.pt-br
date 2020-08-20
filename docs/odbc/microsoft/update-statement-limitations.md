---
description: Limitações da instrução UPDATE
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
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471395"
---
# <a name="update-statement-limitations"></a>Limitações da instrução UPDATE
Para que o driver do Paradox atualize uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox). Quando você usa o driver do Paradox sem implementar o Borland Mecanismo de Banco de Dados, não é possível atualizar uma tabela do Paradox.  
  
 Não há suporte para o driver de texto.  
  
 Quando o driver do Microsoft Excel é usado, é possível atualizar valores, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel. Como resultado, a instrução UPDATE não é considerada oficialmente suportada pelo driver do Microsoft Excel. Somente a instrução INSERT é considerada suportada.
