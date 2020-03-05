---
title: Instalar Analysis Services no modo multidimensional e de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 002a4ce66108622ce5efcf33231edaed9cd1c99b
ms.sourcegitcommit: e914effe771a1ee323bb3653626cd4ba83d77308
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280833"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>Instalar o Analysis Services em modo multidimensional e de mineração de dados
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece funcionalidade de mineração de dados e OLAP (processamento analítico online) para aplicativos de business intelligence. Nesta versão, o suporte para bancos de dados OLAP e modelos de Data Mining está disponível quando você [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instala o no *modo multidimensional*. O modo multidimensional é um dos três modos do servidor em que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa. Esse é o modo padrão. Se você instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando valores padrão, obterá uma instância que executa bancos de dados multidimensionais e modelos de mineração de dados.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é um recurso com várias instâncias, o que significa que você pode instalar mais de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de instância em um único computador, ou executar uma nova instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lado a lado com uma versão anterior. O modo de servidor é específico de uma instância. Usar outros modos exige que você instale instâncias adicionais do servidor.  
  
 Você pode instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sozinho ou com outros componentes. Se você instalar apenas [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o, os seguintes recursos serão instalados quando você selecionar **Analysis Services** na página seleção de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de instalação:  
  
-   O servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para executar bancos de dados e modelos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   Provedores de dados usados para o acesso a dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em bancos de dados de origem  
  
-   SQL Server Configuration Manager  
  
## <a name="choosing-additional-features"></a>Escolhendo recursos adicionais  
 As soluções OLAP do Analysis Services e data warehouse requerem a instalação de componentes adicionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar o desenvolvimento, a implantação e a administração de bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os seguintes recursos adicionais são opções para muitos cenários de usuário típicos:  
  
-   O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], usado para criar e exibir estruturas de dados do Analysis Services e modelos de mineração de dados.  
  
-   Componentes de conectividade de ferramentas de clientes, usados na comunicação entre clientes e servidores, inclusive bibliotecas de rede para DB-Library, ODBC e OLE DB.  
  
-   
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um conjunto de objetos gráficos e programáveis para mover, copiar e transformar dados.  
  
-   Ferramentas de gerenciamento, incluindo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o Replication Monitor.  
  
## <a name="installation-tasks"></a>Tarefas de instalação  
 As tarefas de instalação incluem:  
  
|Links|Tarefas|  
|-----------|-----------|  
|[Requisitos de hardware e software para instalar o SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).|Antes de executar a Instalação, verifique os pré-requisitos para instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e determine a conta a ser usada para provisionar o servidor.|  
|[Instale o SQL Server 2014 do assistente de instalação &#40;&#41;de ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)instalação.|Execute a Instalação do SQL Server para instalar o software.|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|Ao concluir a Instalação, você deve definir as configurações de firewall para permitir conexões remotas com o servidor.|  
|[Autorizar o acesso a objetos e operações &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services)|Os usuários que acessam os bancos de dados do Analysis Services devem ter permissão de Leitura em pelo menos um banco de dados do servidor.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 O conteúdo de instalação adicional pode ser encontrado nos seguintes tópicos:  
  
 [Instalar o Analysis Services em modo Tabular](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Determinar o modo de servidor de uma instância de Analysis Services](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)  
  
 [SQL Server suplementos de mineração de dados](https://www.microsoft.com/download/details.aspx?id=35578)  
  
 Por padrão, os bancos de dados de exemplo, o código de exemplo e os suplementos de aplicativos cliente não são instalados como parte da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar bancos de dados e código de exemplo, veja o [site CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Linguagens e agrupamentos &#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
