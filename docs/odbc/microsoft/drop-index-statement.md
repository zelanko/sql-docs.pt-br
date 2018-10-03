---
title: Instrução de índice DROP | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b00f15f6a660025930ac401278a571f5cb617697
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636744"
---
# <a name="drop-index-statement"></a>Instrução DROP INDEX
Quando o driver do Paradox, dBASE ou Microsoft Access for usado, a sintaxe da instrução DROP INDEX é "DROP INDEX a em b" onde "a" é o nome do índice e "b" é o nome da tabela (não DROP INDEX *nome do índice*).  
  
 Quando o driver do Paradox é usado, a instrução DROP INDEX exclui arquivos de índice secundário Paradox.  
  
 A instrução DROP INDEX não há suporte para os drivers do Microsoft Excel ou texto.
