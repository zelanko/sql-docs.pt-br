---
description: Aumentar ou desabilitar o limite de processo bloqueado
title: Aumentar ou desabilitar o limite de processo bloqueado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d3ddb1a904207960565b7d134961300b7e0ca591
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423730"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumentar ou desabilitar o limite de processo bloqueado
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
