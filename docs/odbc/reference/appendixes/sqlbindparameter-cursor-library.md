---
title: SQLBindParameter (biblioteca de Cursor) | Microsoft Docs
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
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45b3a0355edb0c9fbd37f7047aa0a1e6ff9a1fe8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLBindParameter** função na biblioteca de cursor. Para obter informações gerais sobre **SQLBindParameter**, consulte [função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Um aplicativo pode chamar **SQLBindParameter** para reassociar os parâmetros, como o tipo de dados C, tamanho da coluna e casas decimais da coluna associada permanecem os mesmos.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar os deslocamentos de ligação. (**SQLBindParameter** não precisa ser chamado para essa nova associação ocorra.)  
  
 A biblioteca de cursores suporta associação de parâmetros de dados em execução.

