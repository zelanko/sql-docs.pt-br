---
title: Procurar um modelo usando o visualizador Microsoft Naive Bayes | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec5fa6be2358366b181b0608025d3d3a4b94a321
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Procurar um modelo usando o Visualizador do Microsoft Naive Bayes
  O Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de classificação altamente adaptável para tarefas de modelagem com previsão. Para obter mais informações sobre esse algoritmo, consulte [Referência técnica do algoritmo Naive Bayes da Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md).  
  
 Como um dos principais objetivos de um modelo Naive Bayes é fornecer uma maneira de explorar rapidamente os dados em um conjunto de dados, o Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece vários métodos para exibir a interação entre atributos previsíveis e os atributos de entrada.  
  
> [!NOTE]  
>  Se desejar exibir informações detalhadas sobre as equações usadas no modelo e os padrões descobertos, você poderá alternar para o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece as seguintes guias para explorar dados:  
  
-   [Rede de Dependências](#BKMK_Dependency)  
  
-   [Perfis de Atributo](#BKMK_Profiles)  
  
-   [Características do Atributo](#BKMK_Characteristics)  
  
-   [Distinção de Atributo](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> Rede de Dependências  
 A guia **Rede de Dependências** exibe as dependências entre os atributos de entrada e os atributos previsíveis em um modelo. O controle deslizante à esquerda do visualizador funciona como um filtro vinculado aos pontos fortes das dependências. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 Quando você selecionar um nó, o visualizador destacará as dependências específicas ao nó. Por exemplo, se você escolher um nó previsível, o visualizador também realçará cada nó que ajuda a prever o nó previsível.  
  
 A legenda na parte inferior do visualizador vincula os nós de cores ao tipo de dependência no gráfico. Por exemplo, quando você seleciona um nó previsível, ele fica sombreado na cor turquesa e os nós que preveem o nó selecionado são sombreados em laranja.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> Perfis de Atributo  
 A guia **Perfis de Atributos** exibe histogramas em uma grade. Você pode usar essa grade para comparar o atributo previsível selecionado na caixa **Previsível** com todos os outros atributos que estão no modelo. Cada coluna na guia representa um estado do atributo previsível. Se o atributo previsível tiver muitos estados, você poderá alterar o número de estados exibidos no histograma ajustando as **Barras de histograma**. Se o número que você escolher for menor do que o número total de estados no atributo, os estados estarão listados na ordem de suporte, com os outros estados coletados em um único recipiente cinza.  
  
 Para exibir uma Legenda de Mineração que relaciona as cores do histograma aos estados de um atributo, clique na caixa de seleção **Mostrar Legenda** . A Legenda de Mineração também exibe a distribuição de casos para cada par atributo-valor selecionado.  
  
 Para copiar o conteúdo da grade para a Área de Transferência como uma tabela HTML, clique com o botão direito do mouse na guia **Perfis de Atributo** e selecione **Copiar**.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> Características do Atributo  
 Para usar a guia **Características do Atributo** , selecione um atributo previsível na lista **Atributo** e selecione um estado do atributo selecionado na lista **Valor** . Quando você define essas variáveis, a guia **Características do Atributo** exibe os estados dos atributos associados ao caso selecionado do atributo selecionado. Os atributos são classificados por importância.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> Distinção de Atributo  
 Para usar a guia **Discriminação de Atributo** , selecione um atributo previsível e dois de seus estados nas listas **Atributo**, **Valor 1**e **Valor 2** . A grade da guia **Discriminação de Atributo** exibe as seguintes informações nas colunas:  
  
 **Atributo**  
 Lista outros atributos do conjunto de dados que contêm um estado que altamente favorece um estado do atributo previsível.  
  
 **Valores**  
 Mostra o valor do atributo na coluna **Atributo** .  
  
 **Favorece \<valor 1 >**  
 Mostra uma barra colorida que indica como o valor do atributo favorece significativamente o valor do atributo previsível mostrado em **Valor 1**.  
  
 **Favorece \<valor 2 >**  
 Mostra uma barra colorida que indica como o valor do atributo favorece significativamente o valor do atributo previsível mostrado em **Valor 2**.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica do algoritmo Naive Bayes da Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visualizadores do Modelo de Mineração de Dados](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  

