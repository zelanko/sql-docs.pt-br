---
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
ms.openlocfilehash: 638bae6491c020519a0123ff56fe31e9a9ca1cf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303427"
---
# <a name="drop-index-statement"></a>Instrução DROP INDEX
Quando o driver do Microsoft Access, dBASE ou Paradox é usado, a sintaxe da instrução DROP INDEX é "DROP INDEX a em b", em que "a" é o nome do índice e "b" é o nome da tabela (não DROP INDEX *índice-Name*).  
  
 Quando o driver do Paradox é usado, a instrução DROP INDEX exclui arquivos de índice secundários do Paradox.  
  
 Não há suporte para a instrução DROP INDEX para os drivers de texto ou do Microsoft Excel.
