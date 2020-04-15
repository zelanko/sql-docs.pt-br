---
title: 'Passo 5: Comprometa a Transação | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283346"
---
# <a name="step-5-commit-the-transaction"></a>Etapa 5: Confirmar a transação
O próximo passo é cometer a transação, como mostra a ilustração a seguir.  
  
 ![Mostra como confirmar uma transação](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 O quinto passo é chamar o **SQLEndTran** para cometer ou reverter a transação. O aplicativo só executa essa etapa se definir o modo de confirmação da transação como manual; se o modo de confirmação da transação for o compromisso automático, que é o padrão, a transação é automaticamente cometida quando a declaração é executada. Para obter mais informações, veja [Transações](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Para executar uma declaração em uma nova transação, o aplicativo retorna à etapa 3. Para desconectar-se da fonte de dados, o aplicativo segue para a etapa 6.
