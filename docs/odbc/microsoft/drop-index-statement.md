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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23823e53e516324832c79706e6171b48a9c5297c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071859"
---
# <a name="drop-index-statement"></a>Instrução DROP INDEX
Quando o driver do Microsoft Access, dBASE ou Paradox é usado, a sintaxe da instrução DROP INDEX é "DROP INDEX a em b", em que "a" é o nome do índice e "b" é o nome da tabela (não DROP INDEX *índice-Name*).  
  
 Quando o driver do Paradox é usado, a instrução DROP INDEX exclui arquivos de índice secundários do Paradox.  
  
 Não há suporte para a instrução DROP INDEX para os drivers de texto ou do Microsoft Excel.
