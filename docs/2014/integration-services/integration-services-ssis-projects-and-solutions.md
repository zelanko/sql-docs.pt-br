---
title: Projetos do Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26ab429a5f2abeda9a811e85dc5113121380e999
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62892470"
---
# <a name="integration-services-ssis-projects"></a>Projetos do Integration Services (SSIS)
  
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para o desenvolvimento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Ao implantar pacotes em um [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] banco de dados ou [!INCLUDE[ssIS](../includes/ssis-md.md)] no armazenamento de pacotes, você [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa o serviço para gerenciar os pacotes. O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está disponível apenas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre o serviço, consulte [Serviço Integration Services &#40;Serviço SSIS&#41;](service/integration-services-service-ssis-service.md). Para obter mais informações sobre a implantação de pacotes, consulte [implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md).  
  
 Quando você implantar projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], usa as exibições de Transact-SQL e procedimentos armazenados no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar os projetos. Para obter mais informações sobre a implantação de projetos, consulte [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre o servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consulte [Servidor do Integration Services &#40;SSIS&#41;](catalog/integration-services-ssis-server-and-catalog.md).  
  
 Para obter uma visão geral do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [Ambientes do Integration Services &#40;SSIS&#41; e do Studio](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="understanding-integration-services-projects"></a>Entendendo os projetos do Integration Services  
 Um projeto é um contêiner no qual você desenvolve pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] armazena e agrupa os arquivos que são relacionados ao pacote. Por exemplo, um projeto inclui os arquivos necessários para criar uma solução de ETL (extração, transferência e carregamento) específica.  
  
 Antes de você criar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , familiarize-se com o conteúdo básico deste tipo de projeto. Depois de entender o que um projeto contém, você pode começar a criar e trabalhar com um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
### <a name="folders-in-integration-services-projects"></a>Pastas nos projetos do Integration Services  
 O diagrama a seguir mostra as pastas em um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 ![Pastas em um projeto do Integration Services](media/solutionexplorer.gif "Pastas em um projeto do Integration Services")  
  
 A tabela a seguir descreve as pastas que aparecem em um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Pasta|DESCRIÇÃO|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)]Compacta|Contém pacotes. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Pacotes](../../2014/integration-services/integration-services-ssis-packages.md).|  
|Diversos|Contém arquivos diferentes de arquivos de pacotes.|  
  
### <a name="files-in-integration-services-projects"></a>Arquivos em projetos do Integration Services  
 Ao adicionar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] novo ou existente a uma solução, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] cria arquivos de projeto que têm extensões .dtproj e .dtproj.user e .database.  
  
-   O arquivo *.dtproj contém informações sobre configurações de projeto e itens como pacotes.  
  
-   O arquivo * .dtproj.user contém informações sobre suas preferências para trabalhar com o projeto  
  
-   O arquivo * .database contém informações que o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] exige abrir o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="understanding-solutions"></a>Compreendendo soluções  
 Uma solução é um contêiner que agrupa e gerencia os projetos que você usa quando desenvolve soluções empresariais completas. Uma solução permite que você manipule vários projetos como uma unidade e una um ou mais projetos relacionados que contribuam para uma solução empresarial.  
  
 Soluções podem incluir diferentes tipos de projetos. Se você quiser usar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para criar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , trabalhe em um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em uma solução fornecida por [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria uma nova solução, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] adiciona uma pasta Solução ao Gerenciador de Soluções e cria arquivos que têm extensões .sln e .suo.  
  
-   O arquivo * .sln contém informações sobre as configurações da solução e lista os projetos na solução.  
  
-   O arquivo *.suo contém informações sobre suas preferências para trabalhar com a solução.  
  
 Embora o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crie automaticamente uma solução quando um novo projeto é criado, você também pode criar uma solução em branco e então adicionar projetos depois.  
  
> [!NOTE]  
>  Por padrão, quando você cria um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], a solução não é mostrada no painel **Explorador de Projeto** . Para alterar este comportamento padrão, no menu **Ferramentas** , clique em **Opções**. Na caixa de diálogo **Opções** , expanda **Projetos e Soluções**e clique em **Geral**. Na página **Geral** , selecione **Sempre mostrar solução**.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar ou remover um projeto do Integration Services em uma solução](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
 [Criar um novo projeto de Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
 [Adicionar um item a um projeto do Integration Services](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
 [Copiar itens do projeto](../../2014/integration-services/copy-project-items.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Implantação de um projeto do Integration Services](../../2014/integration-services/development-of-an-integration-services-project.md)  
  
  
