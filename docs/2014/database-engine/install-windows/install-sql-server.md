---
title: Instalar o SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50869ae6b834bd0d9ee1780879d674d22ddf38b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143816"
---
# <a name="install-sql-server-2014"></a>Instalar o SQL Server 2014
## <a name="-download-sql-server-2014-express-httpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[ Baixe o SQL Server 2014 Express ](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Agradecemos aos [Scott Hanselman](http://www.hanselman.com/) para coletar todos os links do pacote do instalador em um único lugar!**
  
 Este tópico fornece uma visão geral de opções de instalação diferentes que temos para instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações sobre os vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes que podem ser instalados e o processo de instalação, consulte [instalação do SQL Server 2014](installation-for-sql-server.md).  
> **Observação:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível nas edições de 32 bits e 64 bits. As edições de 64 e 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são instaladas pelo Assistente de Instalação ou em um prompt de comando. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes, consulte [edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [recursos compatíveis com as edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar bancos de dados de exemplo e código de exemplo de edições não Express do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte o [site do CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843). Para ler sobre o suporte para bancos de dados de exemplo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e código de exemplo para [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], consulte [Databases and Samples Overview](http://go.microsoft.com/fwlink/?LinkId=110391) (Visão geral dos exemplos e bancos de dados).  
  
 Antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine os requisitos de instalação, as verificações de configuração do sistema e as considerações sobre segurança. Para obter mais informações, consulte [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md). Revise os tópicos na próxima seção para obter informações sobre vários cenários de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>Instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] componentes  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Sobre o Mecanismo de Banco de Dados do SQL Server](../sql-server-database-engine-overview.md)|Descreve como instalar e configurar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar a Replicação do SQL Server](install-sql-server-replication.md)|Descreve como instalar e configurar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar o Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|Lista os tópicos para instalar o recurso Distributed Replay.|  
|[Instalar Ferramentas de Gerenciamento do SQL Server](../../sql-server/install/install-sql-server-management-tools.md)|Descreve como instalar e configurar as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar o PowerShell do SQL Server](install-sql-server-powershell.md)|Descreve as considerações de instalação de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>Como instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|Title|Description|  
|-----------|-----------------|  
|[Tópicos de instruções sobre a instalação](../../sql-server/install/installation-how-to-topics.md)|Fornece links para tópicos de procedimentos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do assistente de instalação, no prompt de comando, usando arquivos de configuração e o SysPrep.|  
|[Instalar o SQL Server 2014 no Server Core](install-sql-server-on-server-core.md)|Revise este tópico para instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Windows Server Core.|  
|[Validar uma instalação do SQL Server](validate-a-sql-server-installation.md)|Analise o uso do relatório de Descoberta SQL para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador.|  
|[Verificar parâmetros do Verificador de Configuração do Sistema](check-parameters-for-the-system-configuration-checker.md)|Discute a função do Verificador de Configuração do Sistema (SCC).|  
  
## <a name="configuration"></a>Configuração  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Este tópico apresenta uma visão geral da configuração do firewall e de como configurar o firewall do Windows.|  
|[Configurar um computador multihomed para acesso ao SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Este tópico descreve como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente multihomed.|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Você pode seguir as etapas fornecidas neste tópico para definir as configurações de porta e firewall de modo a permitir o acesso ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou ao PowerPivot para SharePoint.|  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Instalar os recursos de BI do SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 Recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são parte da plataforma [!INCLUDE[msCoName](../../includes/msconame-md.md)] BI e que incluem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] e vários aplicativos cliente usados para criação ou funcionamento com dados analíticos. Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar e configurar o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)   
 [Desinstalar o SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
