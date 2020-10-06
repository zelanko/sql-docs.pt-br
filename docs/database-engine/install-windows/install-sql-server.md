---
title: Guia de instalação do SQL Server
description: Um índice de conteúdo que ajuda a instalar o SQL Server e os componentes associados usando opções como o assistente de instalação, o prompt de comando ou o sysprep.
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c981154462ec6b544d8dd877d1b6a41a6fa0ac2c
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670584"
---
# <a name="sql-server-installation-guide"></a>Guia de instalação do SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

Este artigo é um índice de conteúdo que fornece diretrizes para a instalação do SQL Server no Windows.

Para ver outros cenários de implantação, confira:

- [Linux](../../linux/sql-server-linux-setup.md)
- [Contêineres do Docker](../../linux/sql-server-linux-docker-container-deployment.md)
- [Kubernetes – Clusters de Big Data](../../big-data-cluster/deploy-get-started.md)

A partir do [!INCLUDE[sssql15](../../includes/sssql15-md.md)], o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] só está disponível como um aplicativo de 64 bits. Aqui estão os detalhes importantes sobre como obter o SQL Server e como instalá-lo.

## <a name="getting-started"></a>Introdução
  
* **Edições e recursos**: Examine os recursos compatíveis com as diferentes edições e versões do SQL Server para determinar qual é a mais adequada às suas necessidades de negócios. 
    - [[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)]](~/sql-server/editions-and-components-of-sql-server-version-15.md).  
    - [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
    - [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
    - [[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://docs.microsoft.com/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014)

*  **Requisitos**: Examine os requisitos de instalação de hardware e software para [SQL Server 2016 e 2017](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), [SQL Server 2019](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) ou [SQL Server em Linux](../../linux/sql-server-linux-setup.md), bem como verificações de configuração do sistema e considerações de segurança no [Planejando de uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 


  
* **Exemplos de bancos de dados e exemplo de código**: 
    * Eles não são instalados como parte da instalação do SQL Server por padrão, mas podem ser encontrados 
    * Para instalá-los em edições não Express do SQL Server, confira [Onde estão as amostras](../../samples/sql-samples-where-are.md)
    

## <a name="installation-media"></a>Mídia de instalação

O local de download para [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] depende da edição:

* **SQL Server Enterprise, Standard, e Express Editions** são licenciadas para uso em produção. Para as Edições Enterprise e Standard, entre em contato com seu fornecedor de software para obter a mídia de instalação. Encontre informações de compra e um diretório de parceiros da Microsoft na [página de licenciamento da Microsoft](https://www.microsoft.com/licensing/product-licensing/sql-server).
* [Versão gratuita: mais recente](https://www.microsoft.com/sql-server/sql-server-downloads)
* [Versão gratuita: outras](https://www.microsoft.com/evalcenter/evaluate-sql-server)


Outros componentes do SQL Server podem ser encontrados aqui: 

* [Todas as atualizações cumulativas](https://sqlserverbuilds.blogspot.com/)
* [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122). 
* [SQL Server Management Studio](https://aka.ms/ssmsfullsetup)
* [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)


## <a name="considerations"></a>Considerações

-   A instalação falhará se você iniciar a instalação por meio da Conexão de Área de Trabalho Remota com a mídia em um recurso local no cliente RDC. Para instalar remotamente, a mídia deve estar em um compartilhamento de rede ou local para a máquina virtual ou física. A mídia de instalação[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode estar em um compartilhamento de rede, uma unidade mapeada, uma unidade local ou ser apresentada como um arquivo ISO em uma máquina virtual.  
  
  
-   A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala os seguintes componentes de software necessários ao produto:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arquivos de suporte à instalação  

## <a name="sql-server-installation"></a>Instalação do SQL Server


|Artigo|Descrição|  
|-----------|-----------------|  
|[Assistente de Instalação](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Instale o SQL Server usando a GUI do Assistente de Instalação iniciada na mídia de instalação do setup.exe. |  
|[Prompt de comando](./install-sql-server-from-the-command-prompt.md)|Sintaxe de exemplo e parâmetros de instalação para executar uma instalação do SQL Server por meio do prompt de comando. | 
|[Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Instale o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] no Windows Server Core.|  
|[Verificar parâmetros do Verificador de Configuração do Sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Discute a função do Verificador de Configuração do Sistema (SCC).|   
|[Arquivo de configuração](./install-sql-server-using-a-configuration-file.md)|Sintaxe de exemplo e parâmetros de instalação para executar a Instalação por meio de um arquivo de configuração.|  
|[SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Sintaxe de exemplo e parâmetros de instalação para executar a Instalação por meio do SysPrep.|
|[Adicionar recursos a uma instância](./add-features-to-an-instance-of-sql-server-setup.md)|Atualize os componentes de uma instância existente do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)| Instale uma instância de cluster de failover do SQL Server.  | 
|[Reparar uma instalação com falha do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Repare uma instalação corrompida do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Renomear um computador com o SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Atualize os metadados do sistema armazenados em sys.servers depois que o nome do host de um computador que hospeda uma instância autônoma do SQL Server for renomeado. |  
|[Instalar as atualizações de manutenção do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Instale as atualizações do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Arquivos de log da instalação](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)| Veja e leia os erros nos arquivos de log da instalação do SQL Server. |  
|[Validar uma instalação](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Analise o uso do relatório de Descoberta SQL para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador.|  
  
  
## <a name="individual-component-installation"></a>Instalação de componente individual 
  
|Artigo|Descrição|  
|-----------|-----------------|  
|[Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Instale e configure o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Replicação do SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Instale e configure a Replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|Lista os artigos para instalar o recurso Distributed Replay.|  
|[Ferramentas de Gerenciamento do SQL Server com o SSMS](../../ssms/download-sql-server-management-studio-ssms.md)|Instale e configure as Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Considerações sobre a instalação de componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="sql-server-configuration"></a>Configuração do SQL Server 
  
|Artigo|Descrição|  
|-----------|-----------------|  
|[Configurar o Firewall do Windows (SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Visão geral da configuração do firewall e de como configurar o Firewall do Windows para permitir acesso ao SQL Server.|  
|[Configurar o Firewall do Windows (SSAS)](/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|Defina as configurações de porta e firewall para permitir acesso ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SharePoint.|  
|[Configurar um computador multihomed](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente multihomed.|  

 
## <a name="see-also"></a>Confira também  

[Atualizar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
[Desinstalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
[Instalar o SSRS (SQL Server Reporting Services)](../../reporting-services/install-windows/install-reporting-services.md)   
[Instalar o SSAS (SQL Server Analysis Services)](/analysis-services/instances/install-windows/install-analysis-services)   
[Instalar Recursos de Business Intelligence do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
[Soluções de alta disponibilidade &#40;SQL Server&#41;](../sql-server-business-continuity-dr.md)