---
title: Provedor WMI para conceitos de gerenciamento de configuração
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1058f1491dbf3b52a30f0bcc9720aab3fb056318
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659257"
---
# <a name="wmi-provider-for-configuration-management"></a>Provedor WMI para gerenciamento de configuração
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O provedor WMI é uma camada publicada que é usada com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] snap-in Configuration Manager para [!INCLUDE[msCoName](../../includes/msconame-md.md)] o console de gerenciamento (MMC) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Configuration Manager. Ele fornece uma forma unificada para fazer a interface com chamadas de API que gerenciam as operações do Registro solicitadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e fornece controle e manipulação aprimorados sobre os serviços selecionados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O Provedor WMI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma DLL e um arquivo MOF, que são compilados automaticamente pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor WMI contém um conjunto de classes de objeto usado para controlar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os serviços usando os seguintes métodos:  
  
-   Uma linguagem de script, como VBScript, [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] ou Perl, nos quais é possível inserir o WQL (Windows Query Language).  
  
-   O OBJETO <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> em um programa de código gerenciado SMO.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou MMC com o snap-in do provedor WMI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-a-script-language"></a>Usando uma linguagem de script  
 As vantagens de usar uma linguagem de script incluem o seguinte:  
  
-   Um ambiente de desenvolvimento não é necessário.  
  
-   Os arquivos que dão suporte à linguagem de script estão amplamente disponíveis.  
  
 O script também pode funcionar com outros Provedores WMI, além do Provedor WMI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um administrador de domínio pode usar um script para configurar os serviços, as configurações de rede e as configurações de alias em vários computadores em uma rede.  
  
 Esta seção trata mais detalhadamente do acesso ao Provedor WMI para Configuration Manager a partir de scripts.  
  
## <a name="using-the-smo-managedcomputer-object"></a>Usando o objeto ManagedComputer do SMO  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> é um objeto gerenciado do SMO que fornece acesso ao Provedor WMI para Configuration Manager. Com um programa SMO, o objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> pode ser usado para exibir e modificar serviços, configurações de rede e configurações de alias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Gerenciando serviços e configurações de rede usando o provedor WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>Usando o Console de Gerenciamento Microsoft ou o SQL Server Configuration Manager  
 O MMC fornece uma interface para gerenciar serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em vez de uma linguagem de script ou um programa de código gerenciado. O snap-in do MMC de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para interromper e iniciar serviços, e para alterar contas de serviço.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager também pode ser usado para gerenciar serviços, protocolos de cliente e de servidor e aliases de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/understanding-the-wmi-provider-for-configuration-management.md)   
 [Trabalhando com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Usando as linguagens WQL e de scripts com o provedor WMI para gerenciamento de configuração](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
