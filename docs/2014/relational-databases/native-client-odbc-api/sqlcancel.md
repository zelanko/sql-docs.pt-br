---
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bad2cc35a30f5c6f5855292ff73635cef6072b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067831"
---
# <a name="sqlcancel"></a>SQLCancel
  O [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) tópico diz que, no ODBC 2.x, se um aplicativo chamar `SQLCancel` quando nenhum processamentos estiver sendo feito na instrução, `SQLCancel` tem o mesmo efeito que `SQLFreeStmt` com o `SQL_CLOSE` opção; isso comportamento é definido apenas para fins de integridade e os aplicativos devem chamar `SQLFreeStmt` ou `SQLCloseCursor` para fechar cursores. Mas mesmo que seu aplicativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente defina a versão do ODBC API para que seja 3.5.x ou posterior, a função `SQLCancel` usará o comportamento do ODBC 2.x.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
