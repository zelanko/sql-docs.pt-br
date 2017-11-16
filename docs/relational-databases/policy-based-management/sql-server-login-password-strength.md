---
title: "Nível de segurança da senha de logon do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9254663b1c3d06f96a8baf87af82916cf948b313
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-login-password-strength"></a>Nível de segurança da senha de logon do SQL Server
  Esta regra verifica se “Impor política de senha” de cada logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitado. Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver habilitada e a versão do sistema operacional for anterior ao [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], um invasor poderá explorar repetidamente uma senha conhecida de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que você atualize o sistema operacional para o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não for necessária em seu ambiente, use a Autenticação do Windows.  
  
 Habilite “Impor política de senha” para todos os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para configurar a política de senha para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Política de senha](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
