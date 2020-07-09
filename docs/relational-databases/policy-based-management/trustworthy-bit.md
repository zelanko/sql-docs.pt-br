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
ms.openlocfilehash: 7c0fe0b7b8890b3ef9ee2671b4926c8be99cc679
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727289"
---
# <a name="trustworthy-bit"></a>Bit confiável
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra determina se a função dbo para um banco de dados é atribuída à função de servidor fixa sysadmin e se o banco de dados tem o bit confiável definido como ON.  
  
 Se essas condições forem atendidas, um usuário de banco de dados privilegiado poderá elevar privilégios para a função sysadmin. Nessa função, o usuário pode criar e executar assemblies não seguros que comprometem o sistema.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Desativar o bit confiável ou revogar permissões sysadmin da função de banco de dados dbo.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
