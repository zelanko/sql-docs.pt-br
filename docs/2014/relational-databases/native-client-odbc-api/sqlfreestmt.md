---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16add1df2294e990a5774392b191949b2a8088ff
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425415"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** não é recomendado no ODBC 3.0 e posterior. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte a todos os valores de *Option* definidos para **SQLFreeStmt**. Porém, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**e [SQLFreeHandle](sqlfreehandle.md) substituem ou duplicam a função do **SQLFreeStmt** e devem ser usados no lugar dela.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFreeStmt](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
