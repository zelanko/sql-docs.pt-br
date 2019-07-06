---
title: Projeto de serviços de implantação de uma análise | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e73a5b2d7924d67f7c8bc2e41414e158aa0ff6b
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597508"
---
# <a name="lesson-2-5---deploying-an-analysis-services-project"></a>Lição 2-5: Implantando um projeto do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Para exibir os dados do cubo e da dimensão para os objetos do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você deve implantar o projeto em uma instância específica do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e depois processar o cubo e suas dimensões. *Implantar* um projeto  do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria os objetos definidos em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O*processamento* dos objetos em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] copia os dados das fontes de dados subjacentes nos objetos de cubo. Para obter mais informações, consulte [Implantar projetos do Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md) e [Configurar propriedades de projeto do Analysis Services &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
Nesta etapa do processo de desenvolvimento, você normalmente implanta o cubo em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um servidor de desenvolvimento. Uma vez concluído o desenvolvimento do seu projeto do Business Intelligence, você provavelmente irá usar o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar seu projeto de um servidor de desenvolvimento em um servidor de produção. Para obter mais informações, consulte [Implantação de solução de modelo multidimensional](../multidimensional-models/multidimensional-model-solution-deployment.md) e [Implantar soluções de modelo usando o Assistente de Implantação](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
Na tarefa a seguir, você revisará as propriedades de implantação do projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, implantará o projeto na sua instância local do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="to-deploy-the-analysis-services-project"></a>Para implantar o projeto do Analysis Services  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Tutorial do Analysis Services** e clique em **Propriedades**.  
  
    A caixa de diálogo **Páginas de Propriedade do Tutorial do Analysis Services** é mostrada, exibindo as propriedades da configuração Ativo(Desenvolvimento). Você pode definir várias configurações, cada uma com propriedades diferentes. Por exemplo, um desenvolvedor pode configurar o mesmo projeto para ser implantado em diferentes computadores de desenvolvimento, com propriedades de implantação distintas, como nomes de bancos de dados e propriedades de processamento. Observe o valor da propriedade **Caminho de Saída** . Essa propriedade especifica o local onde os scripts de implantação XMLA do projeto são salvos quando o projeto é compilado. Esses são os scripts usados para implantar os objetos do projeto em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  No nó **Propriedades de Configuração** do painel esquerdo, clique em **Implantação**.  
  
    Revise as propriedades de implantação do projeto. Por padrão, o modelo Projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configura um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar de forma incremental todos os projeto na instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um computador local, criar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com o mesmo nome do projeto e processar os objetos depois da implantação usando a opção de processamento padrão. Para obter mais informações, consulte [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
    > [!NOTE]  
    > Se você deseja implantar o projeto em uma instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no computador local, ou a uma instância em um servidor remoto, altere o **Server** nome de propriedade para a instância apropriada, como \<  **ServerName**>\\\<**InstanceName**>.  
  
3.  Clique em **OK**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Tutorial do Analysis Services** e clique em **Implantar**. Talvez você precise esperar um pouco.  
  
    > [!NOTE]  
    > Se você obtiver erros durante a implantação, use o SQL Server Management Studio para verificar as permissões do banco de dados. A conta especificada para a conexão da fonte de dados deve ter um logon na instância do SQL Server. Clique duas vezes no logon para exibir propriedades de Mapeamento de Usuário. A conta deve ter permissões db_datareader no banco de dados **AdventureWorksDW2012** .  
  
    [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria e implanta o projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na instância especificada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando um script de implantação. O progresso da implantação é exibido em duas janelas: o **saída** janela e o **progresso da implantação – Tutorial do Analysis Services** janela.  
  
    Abra a janela Saída, se necessário, clicando em **Saída** no menu **Exibir** . A janela **Saída** exibe o progresso geral da implantação. O **progresso da implantação – Tutorial do Analysis Services** janela exibe os detalhes sobre cada etapa realizada durante a implantação. Para obter mais informações, consulte [Criar projetos do Analysis Services &#40;SSDT&#41;](../multidimensional-models/build-analysis-services-projects-ssdt.md) e [Implantar projetos do Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
5.  Revisar o conteúdo do **saída** janela e o **progresso da implantação – Tutorial do Analysis Services** para verificar se o cubo foi criado, implantado e processado sem erros.  
  
6.  Para ocultar a janela **Progresso da Implantação – Tutorial do Analysis Services** , clique no ícone **Ocultar Automaticamente** (que se parece com um pino) na barra de ferramentas da janela.  
  
7.  Para ocultar a janela **Saída** , clique no ícone **Ocultar Automaticamente** na barra de ferramentas da janela.  
  
Você implantou com sucesso o cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em sua instância local do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e depois processou e implantou o cubo.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Navegando pelo cubo](lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>Consulte também  
[Implantar projetos do Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
[Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
  
