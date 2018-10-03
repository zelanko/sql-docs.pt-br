---
title: Criando uma solução e a fonte de dados (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ad99c202d858bbdf5de47a21fe26070328e2de2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119626"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>Criando uma solução e uma fonte de dados (tutorial de mineração de dados intermediário)
  Para trabalhar com mineração de dados, você deve primeiro criar um projeto no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] usando o modelo **Multidimensional do Analysis Services e projeto de mineração de dados**. Quando você abre o modelo, ele carrega no designer todos os esquemas que você pode precisar na mineração de dados: fontes de dados, estruturas de mineração e modelos de mineração, e até mesmo cubos, quando sua estrutura de mineração usa dados multidimensionais.  
  
 Quando você cria o projeto, sua solução é armazenada como um arquivo local até ser implantada. Quando você implanta a solução [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procurará o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server especificado nas propriedades do projeto e cria um novo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados com o mesmo nome que o projeto. Por padrão, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa o **localhost** instância para novos projetos. Se estiver usando uma instância nomeada ou se especificou um nome de servidor diferente para a instância padrão, você deverá alterar a propriedade do banco de dados de implantação do projeto para o local onde deseja criar os objetos de mineração de dados.  
  
 Para obter mais informações sobre [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] projetos, consulte [criar um projeto do Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md).  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>Para criar um novo projeto do Analysis Services para este tutorial  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Selecione **Projeto Multidimensional e de Mineração de Dados do Analysis Services** no painel **Modelos Instalados** .  
  
4.  Na caixa **Nome** , nomeie o novo projeto como **DM Intermediate**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>Para alterar a instância em que os objetos de mineração de dados estão armazenados (opcional)  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]diante a **Project** menu, clique em **propriedades**.  
  
2.  No lado esquerdo do painel **Páginas de Propriedades** , clique em **Implantação**.  
  
3.  Verifique se o nome do **Servidor** é **localhost**. Se você estiver usando uma instância diferente, digite o nome dessa instância. Se você estiver usando uma instância nomeada do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], digite o nome do computador e, em seguida, o nome da instância. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>Para alterar as propriedades de implantação de um projeto (opcional)  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e, em seguida, selecione **Propriedades**.  
  
     – ou –  
  
     Na [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]diante a **Project** menu, selecione **propriedades**.  
  
2.  No lado esquerdo do painel **Páginas de Propriedades** , clique em **Implantação**.  
  
     No painel **Opções** , selecione **Modo de Implantação**e defina as opções para **Implantar Tudo** como substituir ou **Implantar Apenas Alterações** como atualizar objetos ou adicionar objetos.  
  
## <a name="creating-a-data-source"></a>Criando uma fonte de dados  
 O Tutorial de mineração de dados básico, você criou uma *fonte de dados* que armazena informações de conexão para o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados. Siga as mesmas etapas para criar a fonte de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] nessa solução.  
  
#### <a name="to-create-a-data-source"></a>Para criar uma fonte de dados  
  
-   [Criando uma fonte de dados &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 Uma única fonte de dados pode dar suporte a várias exibições de fonte de dados, e cada uma dessas exibições pode ter várias tabelas. No entanto, porque a fonte de dados e fonte de dados de exibição são implantadas em sua [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] junto com os modelos de mineração de dados criado por você, como uma prática recomendada, você deve incluir em cada exibição da fonte de dados apenas as tabelas do banco de dados que são necessários para cada modelo de mineração de dados ou grupo de modelos.  
  
 Nas próximas lições, você adicionará exibições de fonte de dados para oferecer suporte a cada um dos novos cenários. Apenas as lições de cesta básica e de clustering de sequência usam a mesma exibição de fonte de dados; caso contrário, cada cenário usa uma exibição de fonte de dados diferente. Portanto, as lições são independentes entre si e podem ser concluídas separadamente.  
  
|Cenário|Dados incluídos na exibição de fonte de dados|  
|--------------|-------------------------------------------|  
|[Lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|Relatórios de vendas mensais para modelos de bicicleta em regiões diferentes, coletados como uma única exibição.|  
|[Lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|Uma tabela que contém uma lista de pedidos de clientes e uma tabela aninhada que mostra as compras individuais de cada cliente.|  
|[Lição 4: Criando um cenário de Clustering de sequências &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|Os mesmos dados que são usados para a análise da cesta de compras, com a adição de um identificador que mostra a ordem na qual itens foram comprados.|  
|[Lição 5: Criando a rede Neural e modelos de regressão logística &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|Uma única tabela contendo alguns dados de rastreamento de desempenho preliminar de um call center.|  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Projetos de mineração de dados](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [Exibições de fontes de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
