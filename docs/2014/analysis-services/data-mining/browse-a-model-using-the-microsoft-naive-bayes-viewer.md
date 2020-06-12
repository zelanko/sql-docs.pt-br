---
title: Procurar um modelo usando o Microsoft Naive Bayes Viewer | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: 83ba32e732a590881803d87c73d9853ee6c20abf
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525338"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Procurar um modelo usando o Visualizador do Microsoft Naive Bayes
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador do Naive Bayes no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo Naive Bayes. O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de classificação altamente adaptável para tarefas de modelagem com previsão. Para obter mais informações sobre esse algoritmo, consulte [Referência técnica do algoritmo Naive Bayes da Microsoft](microsoft-naive-bayes-algorithm.md).  
  
 Como um dos principais objetivos de um modelo Naive Bayes é fornecer uma maneira de explorar rapidamente os dados em um conjunto de dados, o Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece vários métodos para exibir a interação entre atributos previsíveis e os atributos de entrada.  
  
> [!NOTE]  
>  Se desejar exibir informações detalhadas sobre as equações usadas no modelo e os padrões descobertos, você poderá alternar para o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece as seguintes guias para explorar dados:  
  
-   [Rede de Dependências](#BKMK_Dependency)  
  
-   [Perfis de atributo](#BKMK_Profiles)  
  
-   [Características do atributo](#BKMK_Characteristics)  
  
-   [Discriminação de atributo](#BKMK_Discrimination)  
  
##  <a name="dependency-network"></a><a name="BKMK_Dependency"></a>Rede de dependências  
 A guia **Rede de Dependências** exibe as dependências entre os atributos de entrada e os atributos previsíveis em um modelo. O controle deslizante à esquerda do visualizador funciona como um filtro vinculado aos pontos fortes das dependências. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 Quando você selecionar um nó, o visualizador destacará as dependências específicas ao nó. Por exemplo, se você escolher um nó previsível, o visualizador também realçará cada nó que ajuda a prever o nó previsível.  
  
 A legenda na parte inferior do visualizador vincula os nós de cores ao tipo de dependência no gráfico. Por exemplo, quando você seleciona um nó previsível, ele fica sombreado na cor turquesa e os nós que preveem o nó selecionado são sombreados em laranja.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
##  <a name="attribute-profiles"></a><a name="BKMK_Profiles"></a> Perfis de Atributo  
 A guia **Perfis de Atributos** exibe histogramas em uma grade. Você pode usar essa grade para comparar o atributo previsível selecionado na caixa **Previsível** com todos os outros atributos que estão no modelo. Cada coluna na guia representa um estado do atributo previsível. Se o atributo previsível tiver muitos estados, você poderá alterar o número de estados exibidos no histograma ajustando as **Barras de histograma**. Se o número que você escolher for menor do que o número total de estados no atributo, os estados estarão listados na ordem de suporte, com os outros estados coletados em um único recipiente cinza.  
  
 Para exibir uma Legenda de Mineração que relaciona as cores do histograma aos estados de um atributo, clique na caixa de seleção **Mostrar Legenda** . A Legenda de Mineração também exibe a distribuição de casos para cada par atributo-valor selecionado.  
  
 Para copiar o conteúdo da grade para a Área de Transferência como uma tabela HTML, clique com o botão direito do mouse na guia **Perfis de Atributo** e selecione **Copiar**.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
##  <a name="attribute-characteristics"></a><a name="BKMK_Characteristics"></a> Características do Atributo  
 Para usar a guia **Características do Atributo** , selecione um atributo previsível na lista **Atributo** e selecione um estado do atributo selecionado na lista **Valor** . Quando você define essas variáveis, a guia **Características do Atributo** exibe os estados dos atributos associados ao caso selecionado do atributo selecionado. Os atributos são classificados por importância.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
##  <a name="attribute-discrimination"></a><a name="BKMK_Discrimination"></a> Distinção de Atributo  
 Para usar a guia **Discriminação de Atributo** , selecione um atributo previsível e dois de seus estados nas listas **Atributo**, **Valor 1**e **Valor 2** . A grade da guia **Discriminação de Atributo** exibe as seguintes informações nas colunas:  
  
 **Atributo**  
 Lista outros atributos do conjunto de dados que contêm um estado que altamente favorece um estado do atributo previsível.  
  
 **Valores**  
 Mostra o valor do atributo na coluna **Atributo**.  
  
 **Enfatiza\<value 1>**  
 Mostra uma barra colorida que indica como o valor do atributo favorece significativamente o valor do atributo previsível mostrado em **Valor 1**.  
  
 **Enfatiza\<value 2>**  
 Mostra uma barra colorida que indica como o valor do atributo favorece significativamente o valor do atributo previsível mostrado em **Valor 2**.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo do Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)   
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining-model-viewers.md)  
  
  
