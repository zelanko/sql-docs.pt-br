---
title: Bit confiável | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c887b1e8f2243e89d9390bbdd043a5d2483856b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="trustworthy-bit"></a>Bit confiável
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra determina se a função dbo para um banco de dados é atribuída à função de servidor fixa sysadmin e se o banco de dados tem o bit confiável definido como ON.  
  
 Se essas condições forem atendidas, um usuário de banco de dados privilegiado poderá elevar privilégios para a função sysadmin. Nessa função, o usuário pode criar e executar assemblies não seguros que comprometem o sistema.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Desativar o bit confiável ou revogar permissões sysadmin da função de banco de dados dbo.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
