---
title: Tempos de vida da transação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 290d4c43767ba7e1c6f784c84473e9a05503af54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213036"
---
# <a name="transaction-lifetimes"></a>Vidas úteis de transação
  Há uma diferença importante entre as transações iniciadas nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] e aquelas iniciadas no código gerenciado: o código CLR (common language runtime) não pode desequilibrar o estado da transação na entrada ou saída de uma invocação CLR. Esteja ciente das seguintes implicações dessa diferença:  
  
-   Uma transação iniciada em um quadro CLR precisa ser confirmada ou revertida ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro quando o quadro for fechado.  
  
-   Uma transação externa não pode ser confirmada ou revertida no código CLR.  
  
-   Uma tentativa de confirmar uma transação não iniciada no mesmo procedimento causa um erro em tempo de execução.  
  
-   Uma tentativa de reverter uma transação não iniciada no mesmo procedimento causa a paralisação da transação (impedindo a ocorrência de qualquer outra operação como efeito colateral). A transação é descontinuada até que o código CLR saia do escopo. Observe que isso pode ser útil quando você detecta um erro em seu procedimento e deseja verificar se a transação inteira é finalizada.  
  
## <a name="see-also"></a>Consulte também  
 [Integração CLR e transações](../native-client-ole-db-transactions/transactions.md)  
  
  
