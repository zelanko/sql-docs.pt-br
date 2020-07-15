---
title: Opção de configuração de servidor EKM provider enabled | Microsoft Docs
description: Saiba mais sobre a opção "EKM provider enabled". Ela controla o suporte ao dispositivo Gerenciador de Chaves Extensível no SQL Server. Veja como ativar ou desativar essa opção.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- external encryption provider
helpviewer_keywords:
- EKM provider enabled option
ms.assetid: da58ed50-3a13-4172-9065-960559d8f383
author: markingmyname
ms.author: maghan
ms.openlocfilehash: be9e074cd3d58571a0db9646648207b26b1512b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772514"
---
# <a name="ekm-provider-enabled-server-configuration-option"></a>Opção de configuração de servidor EKM provider enabled
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A opção **EKM provider enabled** controla o apoio ao dispositivo Gerenciador de Chaves Extensível em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essa opção está definida como OFF.  
  
 Para habilitar ou desabilitar o recurso, emita um dos seguintes comandos **sp_configure** :  
  
```  
/* Enable the external encryption provider option */  
sp_configure 'EKM provider enabled', 1  
/* Disable the external encryption provider option */  
sp_configure 'EKM provider enabled', 0  
```  
  
> [!NOTE]
>  Esta opção não está habilitada em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  

