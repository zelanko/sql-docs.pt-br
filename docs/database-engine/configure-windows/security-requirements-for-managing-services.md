---
title: Requisitos de segurança para gerenciar serviços | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ede737abf7d158e4d8dee66885ced018f03a375e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68025632"
---
# <a name="security-requirements-for-managing-services"></a>Requisitos de segurança para gerenciar serviços
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para gerenciar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Services, use o SQL Server Configuration Manager ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Gerencie os serviços em servidores agrupados com o Administrador Clusterizado.  
  
 Para gerenciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e definir as opções de configuração de servidor, você deve ser um membro da função de servidor fixa **serveradmin** ou **sysadmin** . Membros do grupo **Administradores** do Windows podem iniciar e interromper serviços e configurar as opções de servidor que o Windows fornece.  
  
> [!NOTE]  
>  Para operar corretamente, as contas usadas para os serviços devem ser configuradas com o domínio, sistema de arquivo e permissões de registro corretos. Para obter informações sobre as permissões necessárias, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="windows-management-instrumentation"></a>Instrumentação de Gerenciamento do Windows  
 O SQL Server Configuration Manager e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usam Instrumentação de Gerenciamento do Windows (WMI) para exibir e modificar algumas das propriedades de servidor. Para administrar serviços e obter o status dos serviços, o usuário deve ter direitos para acessar o objeto WMI. Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], as seguintes páginas de propriedades de servidor usam o WMI:  
  
-   Iniciar serviços automaticamente  
  
-   Parâmetros de inicialização  
  
-   Segurança  
  
-   Diversas configurações de servidor  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Provedor WMI para conceitos de gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
