---
title: SQLCancel | Microsoft Docs
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
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6aff7aea0040e2fd7f86a3ad668b4e4438148497
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121267"
---
# <a name="sqlcancel"></a>SQLCancel
  O [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) tópico diz que, no ODBC 2. x, se um aplicativo chamar `SQLCancel` quando nenhum processamentos estiver sendo feito na instrução, `SQLCancel` tem o mesmo efeito que `SQLFreeStmt` com o `SQL_CLOSE` opção; isso o comportamento é definido apenas para fins de integridade e os aplicativos devem chamar `SQLFreeStmt` ou `SQLCloseCursor` para fechar cursores. Mas mesmo que seu aplicativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente defina a versão do ODBC API para que seja 3.5.x ou posterior, a função `SQLCancel` usará o comportamento do ODBC 2.x.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  