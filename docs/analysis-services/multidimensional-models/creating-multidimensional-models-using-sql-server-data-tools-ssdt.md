---
title: Criar Multidimensional modelos usando o SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
caps.latest.revision: "63"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e841871a7be5dd1d787854bc5fbedc86eed264f4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>Criando modelos multidimensionais usando o SSDT (Ferramentas de Dados do SQL Server)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece dois ambientes diferentes para compilar, implantar e gerenciar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] soluções: [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ambos os ambientes implementam um sistema de projeto. Para obter mais informações sobre projetos do Visual Studio, consulte [Projetos como contêineres](http://go.microsoft.com/fwlink/?LinkId=63960) na Biblioteca MSDN.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é um ambiente de desenvolvimento, baseado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010, usado para criar e modificar soluções de business intelligence. Com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], é possível criar projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contendo definições de objetos (cubos, dimensões e assim por diante) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , que são armazenados em arquivos XML que contêm elementos da linguagem de script do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL). Esses projetos são mantidos em soluções que também podem conter projetos de outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode desenvolver projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como parte de uma solução que seja independente de qualquer instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Pode implantar os objetos em uma instância de um servidor de teste durante o desenvolvimento e, em seguida, usar o mesmo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar os objetos em instâncias de um ou mais servidores de preparação ou de produção. Os projetos e itens de uma solução que inclui o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser integrados com um controle de código-fonte, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe. Para obter mais informações sobre como criar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md). Você também pode usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para se conectar diretamente a uma instância existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar e modificar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , sem trabalhar com um projeto e sem armazenar as definições de objetos em arquivos XML. Para obter mais informações, consulte [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)e o [Conectar em Modo Online a um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é um ambiente de gerenciamento e administração, usado basicamente para administrar instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode gerenciar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (executar backups, processamento e assim por diante) e também pode criar novos objetos diretamente em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente usando scripts XMLA. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um projeto de Scripts do Analysis Server no qual é possível desenvolver e salvar scripts gravados em MDX, extensões DMX e XMLA. Normalmente, os projetos de Scripts do Analysis Server são utilizados na realização de tarefas de gerenciamento ou para recriar objetos, como bancos de dados e cubos, em instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esses projetos podem ser salvos como parte de uma solução e integrados ao controle do código-fonte. Para obter mais informações sobre como criar um projeto de Scripts do Analysis Server no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Projeto de scripts do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="introducing-solutions-projects-and-items"></a>Introdução a soluções, projetos e itens  
 Tanto o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornecem projetos que são organizados em soluções. Uma solução pode conter vários projetos e um projeto, geralmente, contém diversos itens. Sempre que você cria um novo projeto, uma nova solução é gerada automaticamente, sendo possível ainda adicionar projetos a uma solução existente. Os objetos de projeto variam de acordo com o tipo do projeto. Os itens de cada contêiner do projeto são salvos como arquivos em pastas de projeto do sistema de arquivos.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] contém os seguintes projetos com o tipo Projetos de Business Intelligence.  
  
|Projeto|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projeto|Contém as definições de objeto para um único banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações sobre como criar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md).|  
|Importar o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008|Fornece um assistente que você pode usar para criar um novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] importando as definições de objetos de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Projeto|Contém as definições de objeto para um conjunto de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).|  
|Assistente de Projeto de Relatório|Fornece um assistente que orienta você durante o processo de criação de um projeto de relatório usando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Projeto de Modelo de Relatório|Contém as definições de objeto para um modelo de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Projeto do Servidor de Relatório|Contém as definições de objeto para um ou mais relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] também contém vários tipos de projetos que enfatizam várias consultas ou scripts, conforme mostrado na tabela a seguir.  
  
|Projeto|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripts|Contém scripts DMX, MDX e XMLA para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], bem como conexões para instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nas quais esses scripts podem ser executados. Para obter mais informações, consulte [Projeto de Scripts do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).|  
|Scripts do SQL Server Compact|Contém scripts SQL para o SQL Server Compact, bem como conexões para instâncias do SQL Server Compact nas quais esses scripts podem ser executados.|  
|Scripts do SQL Server|Contém scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e XQuery para a instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , bem como conexões para instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nas quais esses scripts podem ser executados. Para obter mais informações, consulte [SQL Server Database Engine](../../database-engine/configure-windows/sql-server-database-engine.md).|  
  
 Para obter mais informações sobre soluções e projetos, consulte "Gerenciando soluções, projetos e arquivos" na documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET ou na Biblioteca MSDN.  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>Optando entre o SQL Server Management Studio e Ferramentas de Dados do SQL Server  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se destina a administrar e configurar objetos existentes no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é criado para desenvolver soluções de business intelligence que incluem funcionalidade de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 A seguir estão algumas diferenças entre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um ambiente integrado para conexão com instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] to configure, managee o administer objects within an instance of [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Usando esses scripts, você também pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar ou modificar os próprios objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , mas o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não dispõe de uma interface gráfica para criação e definição de objetos.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece um ambiente de desenvolvimento integrado para desenvolver soluções de business intelligence. É possível usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no modo de projeto, que utiliza definições baseadas em XML de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contidos em projetos e soluções. Usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto significa que as alterações feitas em objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] serão feitas nas definições desses objetos baseados em XML mas não serão aplicadas diretamente a um objeto de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] até que a solução seja implantada. Você também pode usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online, ou seja, conectar-se diretamente a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e trabalhar com os objetos de um banco de dados existente.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] melhora o desenvolvimento de aplicativos de business intelligence, pois você pode trabalhar em projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um ambiente multiusuário com fontes controladas, sem a necessidade de uma conexão ativa a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece acesso direto a objetos existentes para consulta e teste, e pode ser usado para implementar mais rapidamente bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com script gerado previamente. No entanto, após a implantação do projeto no ambiente de produção, será necessário ter cuidado ao trabalhar com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e seus objetos com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Isso ocorre para evitar alterações de substituição feitas a objetos diretamente em um banco de dados existente e alterações feitas ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que originalmente gerou a solução de implantação. Para obter mais informações, consulte [Trabalhando com projetos e bancos de dados do Analysis Services durante a fase de desenvolvimento](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md), e [Trabalhando com projetos e bancos de dados do Analysis Services em um ambiente de produção](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-production.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
-   [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
-   [Criar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
-   [Implantar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
-   [Trabalhando com projetos e bancos de dados do Analysis Services durante a fase de desenvolvimento](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [Trabalhando com projetos e bancos de dados do Analysis Services em um ambiente de produção](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Projeto de Scripts do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
