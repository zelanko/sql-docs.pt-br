---
title: Instalação do SQL Server 2014 de início rápido | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- data-quality-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
caps.latest.revision: 48
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7567675dffc0395da5152a98700f8fd19a1b3e12
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118202"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>Instalação de início rápido do SQL Server 2014
    
## <a name="introduction"></a>Introdução  
 O Assistente de Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é baseado no Windows Installer. Ele fornece uma única árvore de recursos para a instalação dos seguintes componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   Ferramentas de gerenciamento  
  
-   Componentes de conectividade  
  
 Você pode instalar cada componente individualmente ou selecionar uma combinação dos componentes listados acima. Para fazer a melhor escolha entre as edições e componentes disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [edições e componentes do SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponível em edições de 32 e 64 bits. A Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte às seguintes opções de instalação:  
  
-   **Assistente de Instalação**  
  
     Consulte [instalar o SQL Server 2014 do Assistente de instalação &#40;instalação&#41; ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) para obter informações conceituais sobre como instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o Assistente de instalação.  
  
-   **Prompt de comando**  
  
     Consulte [instalar o SQL Server 2014 do Prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) para exemplo sintaxe e parâmetros de instalação para instalação autônoma.  
  
-   **Arquivo de configuração**  
  
     Consulte [instalar o SQL Server 2014 usando um arquivo de configuração](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md) de exemplo sintaxe e parâmetros de instalação para executar a instalação por meio de um arquivo de configuração.  
  
-   **SysPrep**  
  
     Consulte [instalar o SQL Server 2014 usando SysPrep](../database-engine/install-windows/install-sql-server-using-sysprep.md) para obter informações conceituais sobre como instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o SysPrep.  
  
-   **Instalação do Server Core**  
  
     Consulte [instalar o SQL Server 2014 no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md) para obter informações conceituais sobre como instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Windows Server Core.  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Instalação do recurso de BI**  
  
     Consulte [instalar a recursos de BI do SQL Server 2014](../sql-server/install/install-sql-server-business-intelligence-features.md) para obter informações sobre como instalar os recursos que fazem parte da plataforma Microsoft BI, que incluem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e várias aplicativos cliente usados para criação ou funcionamento com dados analíticos.  
  
-   **Instalação do cluster de failover**  
  
     Consulte [instalação de Cluster de Failover do SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md) para obter informações conceituais sobre como instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cluster de failover.  
  
 Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para instalar bancos de dados de exemplo e código de exemplo de edições não Express do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte o [site do CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843). Para ler sobre o suporte para bancos de dados de exemplo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e código de exemplo para [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], consulte [Databases and Samples Overview](http://go.microsoft.com/fwlink/?LinkId=110391) (Visão geral dos exemplos e bancos de dados).  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Instalação  
 Independentemente de você usar o Assistente de Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou o prompt de comando para instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a instalação envolve uma ou mais das seguintes etapas:  
  
-   Examine os requisitos de instalação, as verificações de configuração do sistema e as considerações sobre segurança da instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  Para obter mais informações, consulte [Planejando uma instalação do SQL Server](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall).  
  
-   Execute a Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para atualizar uma versão existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações, consulte [atualização para o SQL Server 2014](#BKMK_Upgrading).  
  
-   Execute a Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para instalar uma nova instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações, consulte [instalando o SQL Server 2014](#BKMK_Install).  
  
-   Depois de concluir a instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a próxima etapa principal é configurar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e seus componentes. Use os utilitários do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para configurar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configurando o SQL Server 2014](#BKMK_Configure).  
  
 Você pode localizar explicações detalhadas sobre essas tarefas na próxima seção.  
  
## <a name="related-tasks"></a>Related Tasks  
  
###  <a name="BKMK_BeforeYouInstall"></a> Planejando um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalação  
 Antes de instalar o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], deve revisar os requisitos de hardware e de software, as considerações sobre rede e Internet e sobre segurança para instalar e executar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Planejando uma instalação do SQL Server](../../2014/sql-server/install/planning-a-sql-server-installation.md) e também os seguintes tópicos:  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Revise os requisitos de hardware e software, o suporte do sistema operacional, as considerações sobre rede e Internet e os requisitos de espaço em disco rígido.|[Pré-requisitos de instalação](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|Revisar as considerações de segurança para uma instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Considerações sobre segurança](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|Revise os detalhes dos recursos que têm suporte na diferentes edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Recursos e edições](features-supported-by-the-editions-of-sql-server-2014.md)|  
|Determine a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Edições e componentes do SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|Revise a configuração de hardware e aprenda a preparar-se para a instalação do cluster de failover do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Antes de instalar o cluster de failover](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a> Atualizando para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Você pode atualizar instâncias existentes do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações, consulte [atualizar para SQL Server 2014](../database-engine/install-windows/upgrade-sql-server.md). Antes de executar a Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para atualizar para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], revise os tópicos a seguir sobre o processo de atualização:  
  
|Description|Tópico|  
|-----------------|-----------|  
|Documenta os caminhos de atualização com suporte para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Atualizações com suporte](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|Descreve o Supervisor de Atualização, uma ferramenta que analisa instâncias do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para identificar problemas de atualização conhecidos.|[Usar o Supervisor de Atualização para preparar para atualizações](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|Descreve o Distributed Replay Utility, uma ferramenta que pode usar vários computadores para reproduzir dados de rastreamento com uma simulação de uma carga de trabalho de missão crítica. Ao executar uma reprodução em um servidor de teste antes e depois de uma atualização do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você pode medir diferenças de desempenho e procurar alguma incompatibilidade que seu aplicativo possa ter com a atualização.|[Usar o Distributed Replay Utility para preparar para atualizações](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|Lista as alterações significativas que podem afetar seus aplicativos depois da atualização para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Compatibilidade com versões anteriores](backward-compatibility.md)|  
|O tópico de procedimento para atualizar uma instância autônoma de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Atualizar para o SQL Server 2014 usando o Assistente de instalação &#40;instalação&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|O tópico de procedimento para atualizar uma edição do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para outra edição. Para obter informações sobre os caminhos de atualização de edição com suporte, consulte [Atualizações de versão e edição com suporte](../database-engine/install-windows/supported-version-and-edition-upgrades.md).|[Atualizar para outra edição do SQL Server 2014 &#40;instalação&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte à atualização do [!INCLUDE[ssDE](../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de clusters de failover do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] separadamente em todos os nós de cluster de failover. Revise este tópico para obter mais informações.|[Atualizar um cluster de failover do SQL Server](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a> Instalar o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Revise os tópicos a seguir para obter informações sobre os vários cenários de instalação do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
|Description|Tópico|  
|-----------------|-----------|  
|Fornece links para tópicos sobre a instalação de vários componentes do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e tópicos de procedimentos para a instalação do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Instalar o SQL Server 2014](../database-engine/install-windows/install-sql-server.md)|  
|Revise este tópico para instalar o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] no Windows Server Core.|[Instalar o SQL Server 2014 no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|Revise este tópico para adicionar recursos individuais a uma instância existente do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Adicionar recursos a uma instância do SQL Server 2014 &#40;instalação&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|Revise este tópico para criar uma nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Use este tópico para gerenciar nós em uma instância de cluster de failover existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Use este tópico para instalar ferramentas cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um cluster de failover.|[Instalar as ferramentas de cliente em um cluster de failover do SQL Server](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|Analise o uso do relatório de Descoberta SQL para verificar a versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalados no computador.|[Validar uma instalação do SQL Server](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|Fornece links para tópicos de procedimentos para instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] do assistente de instalação, no prompt de comando, usando arquivos de configuração e o SysPrep.|[Tópicos de instruções sobre a instalação](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Esta seção fornece informações sobre como configurar e desinstalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_Configure"></a> Configurando [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Depois de instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você pode configurar adicionalmente o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando utilitários gráficos e de prompt de comando. Consulte os tópicos a seguir para configurar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pela primeira vez:  
  
|Description|Tópico|  
|-----------------|-----------|  
|Use as informações deste tópico para determinar se você precisa desbloquear portas em um firewall para permitir o acesso ao [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou ao PowerPivot para SharePoint. Você pode seguir as etapas fornecidas neste tópico para definir as configurações de porta e firewall.|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|Este tópico apresenta uma visão geral da configuração do firewall e resume informações de interesse de um administrador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|Este tópico descreve como configurar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um ambiente multihomed.|[Configurar um computador multihomed para acesso ao SQL Server](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a> Desinstalando o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Os tópicos a seguir descrevem como desinstalar manualmente uma instância autônoma e uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
|Description|Tópico|  
|-----------------|-----------|  
|Este tópico descreve como desinstalar manualmente uma instância autônoma do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Desinstalar o SQL Server 2014](../sql-server/install/uninstall-sql-server.md)|  
|Este tópico descreve como desinstalar uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Remover uma Instância de Cluster de Failover do SQL Server &#40;Instalação&#41;](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|Este tópico fornece informações sobre como remover manualmente objetos [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) após desinstalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou apenas o servidor DQS.|[Remover objetos do Servidor de Qualidade de Dados](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Especificações do produto SQL Server 2014](sql-server-2014-product-specifications.md)   
 [Introdução à documentação de produto do SQL Server](../2014-toc/books-online-for-sql-server-2014.md) [compatibilidade com versões anteriores](backward-compatibility.md)  
  
  
