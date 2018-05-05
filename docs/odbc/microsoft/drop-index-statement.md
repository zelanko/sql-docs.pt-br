---
title: Instrução de índice DROP | Microsoft Docs
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
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aef4e44ff71a000345dff42a01d5e5e75a13bdd1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="drop-index-statement"></a>Remova a instrução de índice
Quando o driver do Microsoft Access, dBASE ou Paradox é usado, a sintaxe da instrução DROP INDEX é "DROP INDEX a b na" onde "a" é o nome do índice e "b" é o nome da tabela (DROP INDEX não *nome do índice*).  
  
 Quando o driver do Paradox for usado, a instrução DROP INDEX exclui arquivos de índice secundário Paradox.  
  
 Não há suporte para a instrução DROP INDEX para os drivers de texto ou do Microsoft Excel.
