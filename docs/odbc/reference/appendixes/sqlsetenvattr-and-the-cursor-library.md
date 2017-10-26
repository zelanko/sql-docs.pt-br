---
title: SQLSetEnvAttr e a biblioteca de cursores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c08fab3b713e1f1a57d7a81f53ed29b1678893cd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e a biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetEnvAttr** função com a biblioteca de cursores. Para obter informações gerais sobre **SQLSetEnvAttr**, consulte [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 A biblioteca de cursores é afetada pela configuração do atributo ambiente SQL_ATTR_ODBC_VERSION, independentemente da versão do aplicativo ou driver.

