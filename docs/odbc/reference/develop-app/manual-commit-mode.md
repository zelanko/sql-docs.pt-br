---
title: Modo de confirmação manual | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d0e5a4cc5bbda6c8ee4414854f390694297c94e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="manual-commit-mode"></a>Modo de confirmação manual
*No modo de confirmação manual,* aplicativos explicitamente devem concluir as transações chamando **SQLEndTran** para confirmá-las ou revertê-los. Este é o modo de transação normal para a maioria dos bancos de dados relacionais.  
  
 As transações em ODBC não precisa ser explicitamente iniciada. Em vez disso, uma transação iniciada implicitamente sempre que o aplicativo inicia a operação no banco de dados. Se a fonte de dados requer a iniciação de transação explícita, o driver deve fornecer a ele sempre que o aplicativo executa uma instrução que requerem uma transação e não há nenhuma transação atual.
