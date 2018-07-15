---
title: Expiração da senha de logon do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 233df4a6c2827ede45d915d975a6d3e311e921dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251858"
---
# <a name="sql-server-login-password-expiration"></a>Vencimento da senha de logon do SQL Server
  Esta regra verifica se a "Expiração de senha" de cada logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada. Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver habilitada e a versão do sistema operacional for anterior ao [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], um invasor poderá explorar repetidamente uma senha conhecida de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que você atualize o sistema operacional para o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Se a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não for necessária em seu ambiente, use a Autenticação do Windows. Para obter mais informações, veja [Escolher um modo de autenticação](../security/choose-an-authentication-mode.md).  
  
 Habilite a "Expiração de senha" para todos os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [ALTER LOGIN](/sql/t-sql/statements/alter-login-transact-sql) para configurar a política de senha para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Política de senha](../security/password-policy.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
