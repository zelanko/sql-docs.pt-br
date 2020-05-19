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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54ec9ddb143e97aa61a47ebbf0d2094281e59964
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706371"
---
# <a name="sqlcancel"></a>SQLCancel
  O tópico [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) diz que, no ODBC 2. x, se um aplicativo chama `SQLCancel` quando nenhum processamento está sendo feito na instrução, `SQLCancel` tem o mesmo efeito que `SQLFreeStmt` com a `SQL_CLOSE` opção; esse comportamento é definido somente para fins de integridade e os aplicativos devem chamar `SQLFreeStmt` ou `SQLCloseCursor` fechar cursores. Mas mesmo que seu aplicativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente defina a versão do ODBC API para que seja 3.5.x ou posterior, a função `SQLCancel` usará o comportamento do ODBC 2.x.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
