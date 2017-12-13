---
title: "Procurar um modelo usando o Visualizador de regras de associação da Microsoft | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a30bdbe56a78d1bb9b09f0ff179646496bb4afdd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Procurar um modelo usando o Visualizador de Regras de Associação da Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizador de regras de associação em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe os modelos de mineração criados com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo de associação. O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de associação para ser utilizado na criação de modelos de mineração de dados que você pode usar para análise de cesta básica. Para obter mais informações sobre esse algoritmo, consulte [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md).  
  
 A seguir estão as principais razões por usar o algoritmo de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   Encontrar conjuntos de itens que descrevem itens que são localizados normalmente junto em uma transação.  
  
-   Descobrir regras que preveem a presença de outros itens em uma transação baseado em itens existentes.  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
 Para ver como criar, explorar e usar um modelo de mineração Associação, consulte [Lição 3: Criando um cenário de cesta de compras &#40;Tutorial intermediário de mineração de dados&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a).  
  
##  <a name="BKMK_ViewerTabs"></a> Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] inclui as guias a seguir:  
  
-   [Conjuntos de Itens](#BKMK_Itemsets)  
  
-   [Regras](#BKMK_Rules)  
  
-   [Rede de Dependência](#BKMK_Dependency)  
  
 Cada guia contém a caixa de seleção **Mostrar Nome Longo** , que você pode usar para mostrar ou ocultar a tabela da qual o conjunto de itens se origina na regra ou no conjunto de itens.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de Itens  
 A guia **Conjuntos de Itens** exibe a lista de conjuntos de itens que o modelo identificou como localizada normalmente junto. A guia exibe uma grade com as colunas seguintes: **Suporte**, **Tamanho**e **Conjunto de Itens**. Para obter mais informações sobre suporte, consulte [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md). A coluna **Tamanho** exibe o número de itens no conjunto de itens. A coluna **Conjunto de Itens** exibe o conjunto de itens real que o modelo descobriu. Você pode controlar o formato do conjunto de itens usando a lista **Mostrar** , que você pode definir as seguintes opções:  
  
-   **Mostrar o nome e valor de atributo**  
  
-   **Mostrar apenas o valor de atributo**  
  
-   **Mostrar apenas o nome do atributo**  
  
 Você pode filtrar o número de conjuntos de itens que são exibidos na guia utilizando **Suporte mínimo** e **Tamanho Mínimo do Conjunto de Itens**. Você pode limitar o número de conjuntos de itens exibidos cada vez mais utilizando **Filtrar Conjunto de Itens** e digitando uma característica de conjunto de itens que deve existir. Por exemplo, se você digitar "Garrafa de Água = existente", poderá limitar os conjuntos de itens à apenas aqueles que contêm uma garrafa de água. A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Regras  
 A guia **Regras** exibe as regras que o algoritmo de associação descobriu. A guia **Regras** inclui uma grade que contém as colunas **Probabilidade**, **Importância**e **Regra**. A probabilidade descreve como o resultado de uma regra será provavelmente. A importância é projetada para medir a utilidade de uma regra. Embora a probabilidade de ocorrência de uma regra possa ser alta, a utilidade da regra propriamente dita pode ser pouco importante. A coluna de importância trata disso. Por exemplo, se cada conjunto de itens contiver um estado específico de um atributo, uma regra que prevê o estado é trivial, embora a probabilidade seja muito alta. Quanto maior a importância, mais importante é a regra.  
  
 Você pode utilizar **Probabilidade Mínima** e **Importância Mínima** para filtrar as regras, semelhante à filtragem que você pode fazer na guia **Conjuntos de Itens** . Você também pode utilizar **Filtrar Regras** para filtrar uma regra baseada nos estados dos atributos que ela contém.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Rede de Dependência  
 A guia **Rede de Dependência** inclui um visualizador de rede de dependência. Cada nó no visualizador representa um item, como "estado = WA". A seta entre nós representa a associação entre itens. A direção da seta indica a associação entre os itens de acordo com as regras que o algoritmo descobriu. Por exemplo, se o visualizador contiver três itens, A, B e C, e C for  previsto por A e B, se você selecionar o nó C, duas setas apontarão para o nó C — A para C e B para C.  
  
 O controle deslizante à esquerda do visualizador funciona como um filtro vinculado à probabilidade das regras. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visualizadores do modelo de Mineração de dados](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
