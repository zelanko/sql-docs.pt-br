---
title: Aumentar ou desabilitar o limite de processo bloqueado | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b392ec86b64ee41864dfa3c2067e549031b31900
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumentar ou desabilitar o limite de processo bloqueado
  Estas regras verificam se a opção de limite de processo bloqueado está definida como 0 (desabilitada) ou com um valor maior ou igual a 5 (segundos). Definir a opção de limite de processo bloqueado com um valor de 1 até 4 pode fazer o monitor de deadlock ser executado constantemente. Valores de 1 a 4 devem ser usados apenas para solução de problemas e nunca a longo prazo ou em um ambiente de produção sem a assistência do Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Para resolver este problema, defina a opção de limite de processo bloqueado com um valor de 5 (segundos) ou mais ou desabilite o limite de processo bloqueado definindo o valor como 0. Para definir o limite de processo bloqueado com um valor de `5` segundos, execute a seguinte instrução:  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opção blocked process threshold de configuração de servidor](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
