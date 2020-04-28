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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925011"
---
# <a name="immediate-mode"></a>Modo imediato
O modo imediato está em vigor quando a propriedade **LockType** é definida como **adLockOptimistic** ou **adLockPessimistic**. No modo imediato, as alterações em um registro são propagadas para a fonte de dados assim que você declara o trabalho em uma linha concluída chamando o método **Update** .  
  
## <a name="calling-update"></a>Chamando atualização  
 Se você mover do registro que está adicionando ou editando antes de chamar o método **Update** , o ADO automaticamente chamará **Update** para salvar as alterações. Você deve chamar o método **CancelUpdate** antes da navegação se quiser cancelar as alterações feitas no registro atual ou descartar um registro recém-adicionado.  
  
 O registro atual permanece atual depois que você chama o método **Update** .  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Use o método **CancelUpdate** para cancelar as alterações feitas na linha atual ou para descartar uma linha recém-adicionada. Você não pode cancelar alterações na linha atual ou em uma nova linha depois de chamar o método **Update** , a menos que as alterações façam parte de uma transação que você possa reverter com o método **RollbackTrans** ou parte de uma atualização do lote. No caso de uma atualização em lotes, você pode cancelar a **atualização** com o método **CancelUpdate** ou **CancelBatch** .  
  
 Se você estiver adicionando uma nova linha ao chamar o método **CancelUpdate** , a linha atual se tornará a linha que era atual antes da chamada **AddNew** .  
  
 Se você não alterou a linha atual ou adicionou uma nova linha, chamar o método **CancelUpdate** gera um erro.
