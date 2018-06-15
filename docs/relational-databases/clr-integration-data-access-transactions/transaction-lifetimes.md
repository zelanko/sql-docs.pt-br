---
title: Vidas úteis de transação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2c78887d28fdc202da63f58167b4fb414e905f58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917891"
---
# <a name="transaction-lifetimes"></a>Vidas úteis de transação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Há uma diferença importante entre as transações iniciadas nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] e aquelas iniciadas no código gerenciado: o código CLR (common language runtime) não pode desequilibrar o estado da transação na entrada ou saída de uma invocação CLR. Esteja ciente das seguintes implicações dessa diferença:  
  
-   Uma transação iniciada em um quadro CLR precisa ser confirmada ou revertida ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro quando o quadro for fechado.  
  
-   Uma transação externa não pode ser confirmada ou revertida no código CLR.  
  
-   Uma tentativa de confirmar uma transação não iniciada no mesmo procedimento causa um erro em tempo de execução.  
  
-   Uma tentativa de reverter uma transação não iniciada no mesmo procedimento causa a paralisação da transação (impedindo a ocorrência de qualquer outra operação como efeito colateral). A transação é descontinuada até que o código CLR saia do escopo. Observe que isso pode ser útil quando você detecta um erro em seu procedimento e deseja verificar se a transação inteira é finalizada.  
  
## <a name="see-also"></a>Consulte também  
 [Integração CLR e transações](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
