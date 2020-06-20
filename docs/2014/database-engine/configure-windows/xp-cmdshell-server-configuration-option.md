---
title: Opção de configuração de servidor xp_cmdshell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a7feec1765cf6ffaa3e46a300a5155ae73fb13db
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934687"
---
# <a name="xp_cmdshell-server-configuration-option"></a>Opção de configuração de servidor xp_cmdshell
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
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
