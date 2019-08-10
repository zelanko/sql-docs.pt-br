---
title: Criando uma solução e uma fonte de dados (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21bedc825f5890e3eb6551818dc5dc10724d2bf8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891433"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>Criando uma solução e uma fonte de dados (tutorial de mineração de dados intermediário)
  Para trabalhar com a mineração de dados, primeiro crie um projeto primeiro no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] usando o modelo, **Projeto Multidimensional e de Mineração de Dados do Analysis Services**. Quando você abre o modelo, ele carrega no designer todos os esquemas que você pode precisar na mineração de dados: fontes de dados, estruturas de mineração e modelos de mineração, e até mesmo cubos, quando sua estrutura de mineração usa dados multidimensionais.  
  
 Quando você cria o projeto, sua solução é armazenada como um arquivo local até ser implantada. Quando você implantar a solução, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procurará o servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificado nas propriedades de projeto e criará um novo banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] com o mesmo nome que o projeto. Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa a instância **localhost** para novos projetos. Se estiver usando uma instância nomeada ou se especificou um nome de servidor diferente para a instância padrão, você deverá alterar a propriedade do banco de dados de implantação do projeto para o local onde deseja criar os objetos de mineração de dados.  
  
 Para obter mais informações [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sobre projetos, consulte [criar um Analysis Services &#40;projeto&#41;SSDT](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt).  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>Para criar um novo projeto do Analysis Services para este tutorial  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  Selecione **Projeto Multidimensional e de Mineração de Dados do Analysis Services** no painel **Modelos Instalados** .  
  
4.  Na caixa **Nome** , nomeie o novo projeto como **DM Intermediate**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>Para alterar a instância em que os objetos de mineração de dados estão armazenados (opcional)  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Projeto** , clique em **Propriedades**.  
  
2.  No lado esquerdo do painel **Páginas de Propriedades** , clique em **Implantação**.  
  
3.  Verifique se o nome do **Servidor** é **localhost**. Se você estiver usando uma instância diferente, digite o nome dessa instância. Se você estiver usando uma instância nomeada do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], digite o nome do computador e, depois, o nome da instância. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>Para alterar as propriedades de implantação de um projeto (opcional)  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e, em seguida, selecione **Propriedades**.  
  
     – ou –  
  
     No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Projeto** , selecione **Propriedades**.  
  
2.  No lado esquerdo do painel **Páginas de Propriedades** , clique em **Implantação**.  
  
     No painel **Opções** , selecione **Modo de Implantação**e defina as opções para **Implantar Tudo** como substituir ou **Implantar Apenas Alterações** como atualizar objetos ou adicionar objetos.  
  
## <a name="creating-a-data-source"></a>Criando uma fonte de dados  
 No tutorial de data mining básico, você criou uma *fonte de dados* que armazena informações de conexão do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] . Siga as mesmas etapas para criar a fonte de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] nessa solução.  
  
#### <a name="to-create-a-data-source"></a>Para criar uma fonte de dados  
  
-   [Criando um tutorial de &#40;mineração de dados básico de fonte de dados&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 Uma única fonte de dados pode dar suporte a várias exibições de fonte de dados, e cada uma dessas exibições pode ter várias tabelas. No entanto, como a fonte de dados e sua exibição são implantadas no banco de dados [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] com os modelos de mineração de dados criados por você, como prática recomendada, inclua em cada exibição da fonte de dados apenas as tabelas obrigatórias para cada modelo de mineração de dados ou grupo de modelos.  
  
 Nas próximas lições, você adicionará exibições de fonte de dados para oferecer suporte a cada um dos novos cenários. Apenas as lições de cesta básica e de clustering de sequência usam a mesma exibição de fonte de dados; caso contrário, cada cenário usa uma exibição de fonte de dados diferente. Portanto, as lições são independentes entre si e podem ser concluídas separadamente.  
  
|Cenário|Dados incluídos na exibição de fonte de dados|  
|--------------|-------------------------------------------|  
|[Lição 2: Criando um tutorial de mineração &#40;de dados intermediário de cenário de previsão&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|Relatórios de vendas mensais para modelos de bicicleta em regiões diferentes, coletados como uma única exibição.|  
|[Lição 3: Tutorial sobre a criação de &#40;um cenário de mineração de dados intermediário do setor de cesta&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|Uma tabela que contém uma lista de pedidos de clientes e uma tabela aninhada que mostra as compras individuais de cada cliente.|  
|[Lição 4: Tutorial sobre a criação de um &#40;cenário de clustering de dados intermediário de agrupamento de sequências&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|Os mesmos dados que são usados para a análise da cesta de compras, com a adição de um identificador que mostra a ordem na qual itens foram comprados.|  
|[Lição 5: Criando um tutorial de mineração de dados intermediário &#40;de modelos de regressão logística e rede neural&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|Uma única tabela contendo alguns dados de rastreamento de desempenho preliminar de um call center.|  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando um tutorial de mineração &#40;de dados intermediário de cenário de previsão&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Projetos de mineração de dados](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [Exibições de fontes de dados em modelos multidimensionais](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
