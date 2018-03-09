---
title: "Expiração da senha de logon do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c6955ced9de05755a1846d69b5811c86efa26e76
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-login-password-expiration"></a>Vencimento da senha de logon do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta regra verifica se a "Expiração de senha" de cada logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada. Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver habilitada e a versão do sistema operacional for anterior ao [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], um invasor poderá explorar repetidamente uma senha conhecida de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que você atualize o sistema operacional para o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não for necessária em seu ambiente, use a Autenticação do Windows. Para obter mais informações, veja [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Habilite a "Expiração de senha" para todos os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para configurar a política de senha para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Política de senha](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
