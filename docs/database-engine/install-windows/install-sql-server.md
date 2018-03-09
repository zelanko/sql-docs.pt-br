---
title: Instalar o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccbcbc7c58b940a5438cf5ff2c42d8da8da89ec5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="install-sql-server"></a>Instalar o SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 > Para ver o conteúdo relacionado a versões anteriores do SQL Server, consulte [Instalar o SQL Server 2014](https://msdn.microsoft.com/library/bb500395(SQL.120).aspx).

 A partir do [!INCLUDE[sssql15](../../includes/sssql15-md.md)], o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] só está disponível como um aplicativo de 64 bits. Aqui estão os detalhes importantes sobre como obter o SQL Server e como instalá-lo.

## <a name="installation-details"></a>Detalhes da instalação
  
*  **Opções**: instale pelo Assistente de Instalação, em um prompt de comando ou por meio do sysprep
 
*  **Requisitos**: antes de instalar, separe algum tempo para examinar os requisitos de instalação, as verificações de configuração do sistema e as considerações sobre segurança em [Planejamento de uma Instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Processo**: consulte [Instalação para SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) para obter instruções completas sobre o processo de instalação

* **Exemplos de bancos de dados e exemplo de código**: 
    * Eles não são instalados como parte da instalação do SQL Server por padrão 
    * Para instalá-los em edições não Express do SQL Server, acesse o [GitHub](http://github.com/Microsoft/sql-server-samples)
    

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>Como instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Title|Description|  
|-----------|-----------------|  
|[Instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] no Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Examine este artigo para instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] no Windows Server Core.|  
|[Verificar parâmetros do Verificador de Configuração do Sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Discute a função do Verificador de Configuração do Sistema (SCC).|  
|[Instale o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Artigo de procedimento para uma instalação típica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Assistente de Instalação.|  
|[Instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] por meio do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Artigo de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para Instalação autônoma.|  
|[Instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Artigo de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para execução da Instalação por meio de um arquivo de configuração.|  
|[Instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] usando o SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Artigo de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para execução da Instalação por meio do SysPrep.|  
|[Adicionar recursos a uma instância do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] &#40;Instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Artigo de procedimento para atualização de componentes de uma instância existente do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Reparar uma instalação com falha do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Artigo de procedimento para reparar uma instalação corrompida do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Artigo de procedimento para atualizar metadados do sistema armazenados no sys.servers.|  
|[Instalar as atualizações de manutenção do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Artigo de procedimento para instalação de atualizações do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Artigo de procedimento para verificar erros em arquivos de log da instalação.|  
|[Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Analise o uso do relatório de Descoberta SQL para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador.|  
  
  
## <a name="how-to-install-individual-components"></a>Como instalar os componentes individuais  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Descreve como instalar e configurar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar a Replicação do SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Descreve como instalar e configurar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar o Distributed Replay – Visão geral](../../tools/distributed-replay/install-distributed-replay-overview.md)|Lista os artigos para instalar o recurso Distributed Replay.|  
|[Instalar as Ferramentas de Gerenciamento do SQL Server com SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Descreve como instalar e configurar as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar o PowerShell do SQL Server](../../database-engine/install-windows/install-sql-server-powershell.md)|Descreve as considerações de instalação de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="how-to-configure-sql-server"></a>Como configurar o SQL Server  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Este artigo apresenta uma visão geral da configuração do firewall e de como configurar o Firewall do Windows.|  
|[Configurar um computador multihomed para acesso ao SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Este artigo descreve como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente multihomed.|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Você pode seguir as etapas fornecidas neste artigo para definir as configurações de porta e firewall de modo a permitir o acesso ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Edições e recursos com suporte do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Instalar recursos de business intelligence do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Consulte também  

[Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Fazer upgrade para o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Desinstalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
