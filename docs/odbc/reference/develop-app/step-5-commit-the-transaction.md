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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283346"
---
# <a name="step-5-commit-the-transaction"></a>Etapa 5: Confirmar a transação
A próxima etapa é confirmar a transação, conforme mostrado na ilustração a seguir.  
  
 ![Mostra como confirmar uma transação](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 A quinta etapa é chamar **SQLEndTran** para confirmar ou reverter a transação. O aplicativo executará essa etapa somente se ele definir o modo de confirmação da transação como confirmação manual; Se o modo de confirmação da transação for confirmação automática, que é o padrão, a transação será confirmada automaticamente quando a instrução for executada. Para obter mais informações, veja [Transações](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Para executar uma instrução em uma nova transação, o aplicativo retorna para a etapa 3. Para se desconectar da fonte de dados, o aplicativo prossegue para a etapa 6.
