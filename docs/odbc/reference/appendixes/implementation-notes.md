---
title: "Notas de implementação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 017c58b72d1b190d8d11f08cf7ecce5ff58f65b1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="implementation-notes"></a>Notas de implementação
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Esta seção descreve como a biblioteca de cursores ODBC é implementada. Descreve como a biblioteca de cursores mantém seu cache, executa instruções SQL e implementa funções ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cache de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Processando instruções SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funções ODBC e a biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
