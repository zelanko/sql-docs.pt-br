---
title: Procurar um modelo usando o Visualizador de regras de associação da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7c3764d18d26d739023bbbb744236273e5cfd1a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086154"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Procurar um modelo usando o Visualizador de Regras de Associação da Microsoft
  O Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O algoritmo Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de associação para ser utilizado na criação de modelos de mineração de dados que você pode usar para análise de cesta básica. Para obter mais informações sobre esse algoritmo, consulte [Microsoft Association Algorithm](microsoft-association-algorithm.md).  
  
 A seguir estão as principais razões por usar o algoritmo de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   Encontrar conjuntos de itens que descrevem itens que são localizados normalmente junto em uma transação.  
  
-   Descobrir regras que preveem a presença de outros itens em uma transação baseado em itens existentes.  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Para obter uma explicação de como criar, explorar e usar um modelo de mineração de associação, consulte [lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] inclui as guias a seguir:  
  
-   [Conjuntos de Itens](#BKMK_Itemsets)  
  
-   [Regras](#BKMK_Rules)  
  
-   [Rede de Dependência](#BKMK_Dependency)  
  
 Cada guia contém a caixa de seleção **Mostrar Nome Longo** , que você pode usar para mostrar ou ocultar a tabela da qual o conjunto de itens se origina na regra ou no conjunto de itens.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de Itens  
 A guia **Conjuntos de Itens** exibe a lista de conjuntos de itens que o modelo identificou como localizada normalmente junto. A guia exibe uma grade com as seguintes colunas: **O suporte**, **tamanho**, e **conjunto de itens**. Para obter mais informações sobre suporte, consulte [Microsoft Association Algorithm](microsoft-association-algorithm.md). A coluna **Tamanho** exibe o número de itens no conjunto de itens. A coluna **Conjunto de Itens** exibe o conjunto de itens real que o modelo descobriu. Você pode controlar o formato do conjunto de itens usando a lista **Mostrar** , que você pode definir as seguintes opções:  
  
-   **Mostrar o nome e valor de atributo**  
  
-   **Mostrar apenas o valor de atributo**  
  
-   **Mostrar apenas o nome do atributo**  
  
 Você pode filtrar o número de conjuntos de itens que são exibidos na guia utilizando **Suporte mínimo** e **Tamanho Mínimo do Conjunto de Itens**. Você pode limitar o número de conjuntos de itens exibidos cada vez mais utilizando **Filtrar Conjunto de Itens** e digitando uma característica de conjunto de itens que deve existir. Por exemplo, se você digitar "Garrafa de Água = existente", poderá limitar os conjuntos de itens à apenas aqueles que contêm uma garrafa de água. A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Regras  
 A guia **Regras** exibe as regras que o algoritmo de associação descobriu. O **regras** guia inclui uma grade que contém as seguintes colunas: **Probabilidade**, **importância**, e **regra**. A probabilidade descreve como o resultado de uma regra será provavelmente. A importância é projetada para medir a utilidade de uma regra. Embora a probabilidade de ocorrência de uma regra possa ser alta, a utilidade da regra propriamente dita pode ser pouco importante. A coluna de importância trata disso. Por exemplo, se cada conjunto de itens contiver um estado específico de um atributo, uma regra que prevê o estado é trivial, embora a probabilidade seja muito alta. Quanto maior a importância, mais importante é a regra.  
  
 Você pode utilizar **Probabilidade Mínima** e **Importância Mínima** para filtrar as regras, semelhante à filtragem que você pode fazer na guia **Conjuntos de Itens** . Você também pode utilizar **Filtrar Regras** para filtrar uma regra baseada nos estados dos atributos que ela contém.  
  
 Você pode classificar as linhas na grade clicando em um título de coluna.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Rede de Dependência  
 A guia **Rede de Dependência** inclui um visualizador de rede de dependência. Cada nó no visualizador representa um item, como "estado = WA". A seta entre nós representa a associação entre itens. A direção da seta indica a associação entre os itens de acordo com as regras que o algoritmo descobriu. Por exemplo, se o visualizador contiver três itens, A, B e C e C for previsto por A e B, se você selecionar o nó C, duas setas apontarão para o nó C - A para C e B para C.  
  
 O controle deslizante à esquerda do visualizador funciona como um filtro vinculado à probabilidade das regras. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Association Algorithm](microsoft-association-algorithm.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining-model-viewers.md)  
  
  
