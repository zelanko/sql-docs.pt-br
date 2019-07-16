---
title: Modo imediato | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3952ef502bf79d6704cbaea80b9a825a3c70981b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925011"
---
# <a name="immediate-mode"></a>Modo imediato
Modo imediato está em vigor quando o **LockType** estiver definida como **adLockOptimistic** ou **adLockPessimistic**. No modo imediato, alterações em um registro são propagadas para a fonte de dados assim que você declara o trabalho em uma linha completa chamando o **atualização** método.  
  
## <a name="calling-update"></a>Chamada de atualização  
 Se você mover do registro estiver adicionando ou editando antes de chamar o **atualização** método, ADO chamará automaticamente **atualização** para salvar as alterações. Você deve chamar o **CancelUpdate** método antes da navegação se você quiser cancelar todas as alterações feitas no registro atual ou descartar um registro recém-adicionado.  
  
 O registro atual permanece atual depois de chamar o **atualização** método.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Use o **CancelUpdate** método para cancelar as alterações feitas na linha atual ou para descartar uma linha recém-adicionada. Você não pode cancelar as alterações para a linha atual ou uma nova linha depois de chamar o **atualização** método, a menos que as alterações são parte de uma transação que é possível reverter com o **RollbackTrans** método ou parte dele uma atualização em lotes. No caso de uma atualização em lotes, você pode cancelar a **atualize** com o **CancelUpdate** ou **CancelBatch** método.  
  
 Se você estiver adicionando uma nova linha quando você chama o **CancelUpdate** método, a linha atual se torna a linha que foi atual antes do **AddNew** chamar.  
  
 Se você não alterou a linha atual ou adicionou uma nova linha, chamando o **CancelUpdate** método gerará um erro.
