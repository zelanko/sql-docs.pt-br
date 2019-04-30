---
title: SQLRowCount (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b3dcd9c348d83dad1e295e253cb37768fbb0abb
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473049"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLRowCount** função na biblioteca de cursor. Para obter informações gerais sobre **SQLRowCount**, consulte [função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada com o cursor, a biblioteca de cursores retorna o número de linhas de dados que ela foi recuperada do driver.  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada a uma instrução de exclusão ou atualização posicionada, a biblioteca de cursores retorna o número de linhas afetadas pela instrução.  
  
 Quando um aplicativo chama **SQLRowCount** depois que um **selecione** instrução, a biblioteca de cursores retornará -1.
