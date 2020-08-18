---
description: Instrução DROP INDEX
title: Instrução de DROP INDEX | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01b0c51d3fff15184b4542299c97423fbed15aa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412672"
---
# <a name="drop-index-statement"></a>Instrução DROP INDEX
Quando o driver do Microsoft Access, dBASE ou Paradox é usado, a sintaxe da instrução DROP INDEX é "DROP INDEX a em b", em que "a" é o nome do índice e "b" é o nome da tabela (não DROP INDEX *índice-Name*).  
  
 Quando o driver do Paradox é usado, a instrução DROP INDEX exclui arquivos de índice secundários do Paradox.  
  
 Não há suporte para a instrução DROP INDEX para os drivers de texto ou do Microsoft Excel.
