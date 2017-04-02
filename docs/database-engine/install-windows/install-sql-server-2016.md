---
title: "Instalar o SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "banco de dados de exemplo AdventureWorks"
  - "instalando o SQL Server, preparando para instalar"
  - "instalação [SQL Server]"
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
ms.author: "mikeray"
manager: "jhubbard"
---
# Instalar o SQL Server 2016
  SQL Server 2016 é um aplicativo de 64 bits. Aqui estão os detalhes importantes sobre como obter o SQL Server e como instalá-lo.

## <a name="installation-details"></a>Detalhes da instalação
  
*  **Opções**: instale pelo Assistente de Instalação, em um prompt de comando ou por meio do sysprep
 
*  **Requisitos**: antes de instalar, separe algum tempo para examinar os requisitos de instalação, as verificações de configuração do sistema e as considerações sobre segurança em [Planejamento de uma Instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Processo**: consulte [Instalação para SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) para obter instruções completas sobre o processo de instalação

* **Exemplos de bancos de dados e exemplo de código**: 
    * Eles não são instalados como parte da instalação do SQL Server por padrão 
    * Para instalá-las para edições não Express do SQL Server, consulte o [site da CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843)
    * Para ler sobre o suporte aos bancos de dados de exemplo do SQL Server e o código de exemplo do SQL Server Express, consulte [Visão Geral de Bancos de Dados e Exemplos](http://go.microsoft.com/fwlink/?LinkId=110391)
    

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

O local de download para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depende da edição:

- **SQL Server Enterprise, Standard, e Express Editions** são licenciadas para uso em produção. Para Enterprise e Standard Editions, entre em contato com seu fornecedor de software para obter a mídia de instalação. Você pode encontrar informações de compra e um diretório de parceiros da Microsoft no [site de compras da Microsoft](https://www.microsoft.com/en-us/server-cloud/products/sql-server/overview.aspx). 

- **Edições grátis** estão disponíveis nestes links:

| Edição | Description
|---------|--------
|[Developer Edition](http://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?q=SQL%20Server%20Developer) | Conjunto gratuito e completo do software SQL Server 2016 Enterprise Edition que permite que os desenvolvedores compilem, testem e demonstrem aplicativos em um ambiente que não seja de produção. 
|[Express Edition](http://www.microsoft.com/download/details.aspx?id=52679)|  Banco de dados básico gratuito que é ideal para a implantação de bancos de dados pequenos em ambientes de produção. Compile aplicativos orientados a dados de desktops e pequenos servidores até 10 GB de tamanho de disco. 
| [Evaluation Edition](http://technet.microsoft.com/evalcenter/mt130694) | Conjunto completo de recursos de software do SQL Server Enterprise Edition que fornece um período de avaliação de 180 dias.
   
 
  

## <a name="how-to-install-sql-server"></a>Como instalar o SQL Server
 
|Título|Description|  
|-----------|-----------------|  
|[Instalar o SQL Server 2016 no Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)|Revise este tópico para instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Windows Server Core.|  
|[Verificar parâmetros do Verificador de Configuração do Sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Discute a função do Verificador de Configuração do Sistema (SCC).|  
|[Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)|Tópico de procedimento para uma instalação típica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Assistente de Instalação.|  
|[Instalar o SQL Server 2016 do Prompt de Comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Tópico de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para Instalação autônoma.|  
|[Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Tópico de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para execução da Instalação por meio de um arquivo de configuração.|  
|[Instalar o SQL Server 2016 usando SysPrep](../../database-engine/install-windows/install-sql-server-2016-using-sysprep.md)|Tópico de procedimento que fornece sintaxe de exemplo e parâmetros de instalação para execução da Instalação por meio do SysPrep.|  
|[Adicionar recursos a uma instância do SQL Server 2016 &#40;Instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Tópico de procedimento para atualização de componentes de uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Reparar uma instalação com falha do SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)|Tópico de procedimento para reparar uma instalação corrompida do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Tópico de procedimento para atualizar metadados do sistema armazenados no sys.servers.|  
|[Instalar atualizações de serviço do SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-servicing-updates.md)|Tópico de procedimento para instalar atualizações para o SQL Server 2016.|  
|[Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Tópico de procedimento para verificar erros em arquivos de log da instalação.|  
|[Validar uma instalação do SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Analise o uso do relatório de Descoberta SQL para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador.|  
  
  
## <a name="how-to-install-individual-components"></a>Como instalar os componentes individuais  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Descreve como instalar e configurar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar a Replicação do SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Descreve como instalar e configurar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Instalar o Distributed Replay – Visão geral](../../tools/distributed-replay/install-distributed-replay-overview.md)|Lista os tópicos para instalar o recurso Distributed Replay.|  
|[Instalar as Ferramentas de Gerenciamento do SQL Server com SSMS](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md)|Descreve como instalar e configurar as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Instalar o PowerShell do SQL Server](../../database-engine/install-windows/install-sql-server-powershell.md)|Descreve as considerações de instalação de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="how-to-configure-sql-server"></a>Como configurar o SQL Server  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Este tópico apresenta uma visão geral da configuração do firewall e de como configurar o firewall do Windows.|  
|[Configurar um computador multihomed para acesso ao SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Este tópico descreve como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente multihomed.|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Você pode seguir as etapas fornecidas neste tópico para definir as configurações de porta e firewall de modo a permitir o acesso ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Recursos com suporte na Edição do SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
[Instalar os recursos do Business Intelligence do SQL Server 2016](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
  [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Consulte também  

[Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Atualizar para o SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Desinstalar o SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  