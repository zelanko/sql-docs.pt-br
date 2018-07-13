---
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed3bdb4cc5c2508435bff011545b5b9113d7aeac
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424385"
---
# <a name="sqlcancel"></a>SQLCancel
  O [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) tópico diz que, no ODBC 2.x, se um aplicativo chamar `SQLCancel` quando nenhum processamentos estiver sendo feito na instrução, `SQLCancel` tem o mesmo efeito que `SQLFreeStmt` com o `SQL_CLOSE` opção; isso comportamento é definido apenas para fins de integridade e os aplicativos devem chamar `SQLFreeStmt` ou `SQLCloseCursor` para fechar cursores. Mas mesmo que seu aplicativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente defina a versão do ODBC API para que seja 3.5.x ou posterior, a função `SQLCancel` usará o comportamento do ODBC 2.x.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
