---
title: 'Etapa 5: confirmar a transação | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bde493edbc6d677b27ef72a24736b504959a7b59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114125"
---
# <a name="step-5-commit-the-transaction"></a>Etapa 5: Confirmar a transação
A próxima etapa é confirmar a transação, conforme mostrado na ilustração a seguir.  
  
 ![Mostra como confirmar uma transação](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 A quinta etapa é chamar **SQLEndTran** para confirmar ou reverter a transação. O aplicativo executará essa etapa somente se ele definir o modo de confirmação da transação como confirmação manual; Se o modo de confirmação da transação for confirmação automática, que é o padrão, a transação será confirmada automaticamente quando a instrução for executada. Para obter mais informações, consulte [Transações](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Para executar uma instrução em uma nova transação, o aplicativo retorna para a etapa 3. Para se desconectar da fonte de dados, o aplicativo prossegue para a etapa 6.
