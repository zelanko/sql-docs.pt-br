---
title: Opção de configuração de servidor xp_cmdshell | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d403205c3fc3ef57fcfa7e566f0913f00604862
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="xpcmdshell-server-configuration-option"></a>Opção de configuração de servidor xp_cmdshell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A opção **xp_cmdshell** é uma opção de configuração de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite aos administradores de sistema controlar se o procedimento armazenado estendido **xp_cmdshell** pode ser executado em um sistema. Por padrão, a opção **xp_cmdshell** é desabilitada em novas instalações. Antes de habilitar essa opção, é importante considerar as possíveis implicações de segurança associadas ao seu uso. Código desenvolvido recentemente não deve usar essa opção, pois de modo geral ela deve ser deixada desabilitada. Alguns aplicativos herdados requerem que ela seja habilitada e, se não é possível modificá-los para evitar o uso da opção, ela pode ser habilitada usando o Gerenciamento baseado em políticas ou executando o procedimento armazenado do sistema **sp_configure**, conforme mostrado no exemplo de código a seguir:  
  
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
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
