---
title: Instalar o Analysis Services in Multidimensional e o modo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: 100bac6834825af1e22658279d26be02c30f3f39
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349260"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>Instalar o Analysis Services em modo multidimensional e de mineração de dados
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece funcionalidade de mineração de dados e OLAP (processamento analítico online) para aplicativos de business intelligence. Nesta versão, suporte para bancos de dados OLAP e modelos de mineração de dados está disponível quando você instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na *modo Multidimensional*. O modo multidimensional é um dos três modos do servidor em que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa. Esse é o modo padrão. Se você instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando valores padrão, obterá uma instância que executa bancos de dados multidimensionais e modelos de mineração de dados.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é um recurso com várias instâncias, o que significa que você pode instalar mais de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de instância em um único computador, ou executar uma nova instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lado a lado com uma versão anterior. O modo de servidor é específico de uma instância. Usar outros modos exige que você instale instâncias adicionais do servidor.  
  
 Você pode instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sozinho ou com outros componentes. Se você instalar apenas [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os seguintes recursos são instalados quando você seleciona **Analysis Services** na página seleção de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação:  
  
-   O servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para executar bancos de dados e modelos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   Provedores de dados usados para o acesso a dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em bancos de dados de origem  
  
-   SQL Server Configuration Manager  
  
## <a name="choosing-additional-features"></a>Escolhendo recursos adicionais  
 As soluções OLAP do Analysis Services e data warehouse requerem a instalação de componentes adicionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar o desenvolvimento, a implantação e a administração de bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os seguintes recursos adicionais são opções para muitos cenários de usuário típicos:  
  
-   O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], usado para criar e exibir estruturas de dados do Analysis Services e modelos de mineração de dados.  
  
-   Componentes de conectividade de ferramentas de cliente, usado para comunicação entre clientes e servidores, incluindo bibliotecas de rede para DB-Library, ODBC e OLE DB.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um conjunto de objetos gráficos e programáveis para mover, copiar e transformar dados.  
  
-   Ferramentas de gerenciamento, incluindo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o Replication Monitor.  
  
## <a name="installation-tasks"></a>Tarefas de instalação  
 As tarefas de instalação incluem:  
  
|Links|Tarefas|  
|-----------|-----------|  
|[Requisitos de hardware e Software para instalação do SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md) e [configurar contas de serviço do Windows e as permissões](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).|Antes de executar a Instalação, verifique os pré-requisitos para instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e determine a conta a ser usada para provisionar o servidor.|  
|[Instalar o SQL Server 2014 do Assistente de instalação &#40;instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).|Execute a Instalação do SQL Server para instalar o software.|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Ao concluir a Instalação, você deve definir as configurações de firewall para permitir conexões remotas com o servidor.|  
|[Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|Os usuários que acessam os bancos de dados do Analysis Services devem ter permissão de Leitura em pelo menos um banco de dados do servidor.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 O conteúdo de instalação adicional pode ser encontrado nos seguintes tópicos:  
  
 [Instalar o Analysis Services em modo Tabular](../../analysis-services/instances/install-windows/install-analysis-services.md)  
  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
 [Suplementos de mineração de dados do SQL Server](https://go.microsoft.com/fwlink/?LinkId=197091)  
  
 Por padrão, os bancos de dados de exemplo, o código de exemplo e os suplementos de aplicativos cliente não são instalados como parte da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar bancos de dados e código de exemplo, veja o [site CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Idiomas e ordenações &amp;#40;Analysis Services&amp;#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
