---
title: Bit confiável | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c63c98eda9ef0827919bfe36f3a2b14ef717f648
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021502"
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
  
  
