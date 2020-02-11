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
ms.openlocfilehash: be902866cfcf98a10af2c3741926de8b7541bb79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125603"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLRowCount** na biblioteca de cursores. Para obter informações gerais sobre **SQLRowCount**, consulte [função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada ao cursor, a biblioteca de cursores retorna o número de linhas de dados que ele recuperou do driver.  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada a uma instrução UPDATE ou DELETE posicionada, a biblioteca de cursores retorna o número de linhas afetadas pela instrução.  
  
 Quando um aplicativo chama **SQLRowCount** após uma instrução **Select** , a biblioteca de cursores retorna-1.
