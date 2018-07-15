---
title: Provedor WMI para conceitos de gerenciamento de configuração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
caps.latest.revision: 23
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e19f7bda872dbf29c018599430f40bfd353ae42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290282"
---
# <a name="wmi-provider-for-configuration-management-concepts"></a>Provedor WMI para conceitos de gerenciamento de configuração
  O provedor WMI é uma camada publicada usada com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] snap-in Gerenciador de configuração do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Configuration Manager. Ele fornece uma forma unificada para fazer a interface com chamadas de API que gerenciam as operações do Registro solicitadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e fornece controle e manipulação aprimorados sobre os serviços selecionados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O Provedor WMI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma DLL e um arquivo MOF, que são compilados automaticamente pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor WMI contém um conjunto de classes de objeto usado para controlar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviços usando os seguintes métodos:  
  
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
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> é um objeto gerenciado do SMO que fornece acesso ao Provedor WMI para Configuration Manager. Com um programa SMO, o objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> pode ser usado para exibir e modificar serviços, configurações de rede e configurações de alias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [gerenciamento de serviços e configurações de rede usando o provedor de WMI](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>Usando o Console de Gerenciamento Microsoft ou o SQL Server Configuration Manager  
 O MMC fornece uma interface para gerenciar serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em vez de uma linguagem de script ou um programa de código gerenciado. O snap-in do MMC de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para interromper e iniciar serviços, e para alterar contas de serviço.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager também pode ser usado para gerenciar serviços, protocolos de cliente e de servidor e aliases de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o provedor WMI para gerenciamento de configuração](understanding-the-wmi-provider-for-configuration-management.md)   
 [Trabalhando com o provedor WMI para gerenciamento de configuração](working-with-the-wmi-provider-for-configuration-management.md)   
 [Usando as linguagens WQL e de scripts com o provedor WMI para gerenciamento de configuração](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
