---
title: Implantando um projeto de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5d98bab3-3577-4143-b737-5196444a36ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: ec7d1aa9a432b9d54e00427deb7b47ea5fd77fbc
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543461"
---
# <a name="deploying-an-analysis-services-project"></a>Implantando um projeto do Analysis Services
  Para exibir os dados do cubo e da dimensão para os objetos do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , você deve implantar o projeto em uma instância específica do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e depois processar o cubo e suas dimensões. A *implantação* de um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] projeto cria os objetos definidos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . O*processamento* dos objetos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] copia os dados das fontes de dados subjacentes nos objetos de cubo. Para obter mais informações, consulte [Implantar projetos do Analysis Services &#40;SSDT&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md) e [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
 Nesta etapa do processo de desenvolvimento, você normalmente implanta o cubo em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em um servidor de desenvolvimento. Uma vez concluído o desenvolvimento do seu projeto do Business Intelligence, você provavelmente irá usar o Assistente para Implantação do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para implantar seu projeto de um servidor de desenvolvimento em um servidor de produção. Para obter mais informações, consulte [Implantação de solução de modelo multidimensional](multidimensional-models/multidimensional-model-solution-deployment.md) e [Implantar soluções de modelo usando o Assistente de Implantação](multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 Na tarefa a seguir, você revisará as propriedades de implantação do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e, em seguida, implantará o projeto na sua instância local do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
### <a name="to-deploy-the-analysis-services-project"></a>Para implantar o projeto do Analysis Services  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Tutorial do Analysis Services** e clique em **Propriedades**.  
  
     A caixa de diálogo **Páginas de Propriedade do Tutorial do Analysis Services** é mostrada, exibindo as propriedades da configuração Ativo(Desenvolvimento). Você pode definir várias configurações, cada uma com propriedades diferentes. Por exemplo, um desenvolvedor pode configurar o mesmo projeto para ser implantado em diferentes computadores de desenvolvimento, com propriedades de implantação distintas, como nomes de bancos de dados e propriedades de processamento. Observe o valor da propriedade **Caminho de Saída** . Essa propriedade especifica o local onde os scripts de implantação XMLA do projeto são salvos quando o projeto é compilado. Esses são os scripts usados para implantar os objetos do projeto em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
2.  No nó **Propriedades de Configuração** do painel esquerdo, clique em **Implantação**.  
  
     Revise as propriedades de implantação do projeto. Por padrão, o modelo Projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] configura um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para implantar de forma incremental todos os projeto na instância padrão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em um computador local, criar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] com o mesmo nome do projeto e processar os objetos depois da implantação usando a opção de processamento padrão. Para obter mais informações, consulte [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
    > [!NOTE]  
    >  Se você quiser implantar o projeto em uma instância nomeada do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no computador local ou em uma instância em um servidor remoto, altere a propriedade **Server** para o nome de instância apropriado, como \<*ServerName**> \\ < **InstanceName**> *.  
  
3.  Clique em **OK**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Tutorial do Analysis Services** e clique em **Implantar**. Talvez você precise esperar um pouco.  
  
    > [!NOTE]  
    >  Se você obtiver erros durante a implantação, use o SQL Server Management Studio para verificar as permissões do banco de dados. A conta especificada para a conexão da fonte de dados deve ter um logon na instância do SQL Server. Clique duas vezes no logon para exibir propriedades de Mapeamento de Usuário. A conta deve ter permissões db_datareader no banco de dados **AdventureWorksDW2012** .  
  
     [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] cria e implanta o projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na instância especificada do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usando um script de implantação. O progresso da implantação é exibido em duas janelas: a janela de **saída** e a janela do **tutorial de progresso da implantação-Analysis Services** .  
  
     Abra a janela Saída, se necessário, clicando em **Saída** no menu **Exibir** . A janela **Saída** exibe o progresso geral da implantação. A janela **progresso da implantação-Analysis Services tutorial** exibe os detalhes sobre cada etapa tomada durante a implantação. Para obter mais informações, consulte [Criar projetos do Analysis Services &#40;SSDT&#41;](multidimensional-models/build-analysis-services-projects-ssdt.md) e [Implantar projetos do Analysis Services &#40;SSDT&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
5.  Examine o conteúdo da janela **saída** e a janela **progresso da implantação – Analysis Services tutorial** para verificar se o cubo foi criado, implantado e processado sem erros.  
  
6.  Para ocultar a janela **Progresso da Implantação – Tutorial do Analysis Services** , clique no ícone **Ocultar Automaticamente** (que se parece com um pino) na barra de ferramentas da janela.  
  
7.  Para ocultar a janela **Saída** , clique no ícone **Ocultar Automaticamente** na barra de ferramentas da janela.  
  
 Você implantou com sucesso o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em sua instância local do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]e depois processou e implantou o cubo.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Navegando pelo cubo](lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar projetos de Analysis Services &#40;SSDT&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md)   
 [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
