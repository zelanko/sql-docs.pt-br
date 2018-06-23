---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8aa28af9291b06607021209fd673869b34157f53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119856"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** não é recomendado no ODBC 3.0 e posterior. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte a todos os valores de *Option* definidos para **SQLFreeStmt**. Porém, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**e [SQLFreeHandle](sqlfreehandle.md) substituem ou duplicam a função do **SQLFreeStmt** e devem ser usados no lugar dela.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFreeStmt](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  