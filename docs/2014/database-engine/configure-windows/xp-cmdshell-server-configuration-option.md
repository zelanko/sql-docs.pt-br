---
title: Opção de configuração de servidor xp_cmdshell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f59953bff75a352770c3df3d0910eeaa0b97c38e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208686"
---
# <a name="xpcmdshell-server-configuration-option"></a>Opção de configuração de servidor xp_cmdshell
  A opção **xp_cmdshell** é uma opção de configuração de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite aos administradores de sistema controlar se o procedimento armazenado estendido **xp_cmdshell** pode ser executado em um sistema. Por padrão, a opção **xp_cmdshell** está desabilitada em novas instalações. Para habilitá-la, use o Gerenciamento Baseado em Políticas ou execute o procedimento armazenado do sistema **sp_configure** , como mostra o seguinte exemplo de código:  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
