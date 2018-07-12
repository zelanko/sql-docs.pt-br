---
title: Explorando o modelo de Clustering (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35cbe12526fbd8ead78132f8560368b62e50aa61
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153377"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Explorando o modelo de clustering (Tutorial de mineração de dados básico)
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Clustering agrupa casos em clusters que contenham características semelhantes. Esses agrupamentos são úteis para explorar dados, identificando anomalias nos dados e criar previsões.  
  
 O Visualizador de Cluster da [!INCLUDE[msCoName](../includes/msconame-md.md)] fornece as seguintes guias para serem usadas na exploração de modelos de mineração de cluster:  
  

  
##  <a name="ClusterDiagramTab"></a> Guia diagrama de cluster  
 A guia Diagrama de Cluster exibe todos os clusters existentes em um modelo de mineração. As linhas entre os clusters representam "proximidade" e estão sombreadas com base no grau de semelhança que os clusters têm. A cor real de cada cluster representa a frequência da variável e o estado no cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Para explorar o modelo na guia Diagrama de Cluster  
  
1.  Use o **modelo de mineração** lista na parte superior das **Visualizador do modelo de mineração** tab para alternar para o `TM_Clustering` modelo.  
  
2.  No **Viewer** lista, selecione **Visualizador de Cluster da Microsoft**.  
  
3.  No **variável de sombreamento** caixa, selecione **comprador de bicicleta**.  
  
     A variável padrão é **população**, mas você pode alterar isso para qualquer atributo no modelo, para descobrir quais clusters contêm membros que têm os atributos desejados.  
  
4.  Selecione **1** na **estado** caixa para explorar os casos em que uma bicicleta foi comprada.  
  
     O **densidade** legenda descreve a densidade do par de estado de atributo selecionado na variável de sombreamento e o estado. Neste exemplo ele nos informa que o clusterwith o sombreamento mais escuro tem a maior porcentagem de compradores de bicicleta.  
  
5.  Coloque o seu mouse sobre o cluster com o sombreamento mais escuro.  
  
     Uma dica de ferramenta exibe a porcentagem de casos que têm o atributo `Bike Buyer = 1`.  
  
6.  Selecione o cluster com a densidade mais alta, clique com botão direito no cluster, selecione **renomear Cluster** e digite **altos compradores de bicicleta** para identificação posterior. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Localize o cluster com o sombreamento mais claro (e a menor densidade). Clique com botão direito no cluster, selecione **renomear Cluster** e digite **baixos compradores de bicicleta**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Clique o **altos compradores de bicicleta** do cluster e arraste-o para uma área do painel que lhe dará uma visão clara de suas conexões com outros clusters.  
  
     Quando você seleciona um cluster, as linhas que conectam esse cluster a outros são realçadas para que você possa facilmente ver todas as relações desse cluster. Quando o cluster não estiver selecionado, você poderá dizer pela escuridão das linhas o grau de importância das relações entre todos os clusters do diagrama. Um sombreamento claro ou a ausência dele indica que os clusters não são muito parecidos.  
  
9. Use o controle deslizante à esquerda da rede para filtrar os links menos importantes e encontrar os clusters com relações mais próximas. O departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] pode querer combinar clusters similares na determinação do melhor método de entrega da mala direta.  
  

  
##  <a name="ClusterProfilesTab"></a> Guia Perfis de cluster  
 O **perfis de Cluster** guia fornece uma visão geral do `TM_Clustering` modelo. O **perfis de Cluster** guia contém uma coluna para cada cluster no modelo. A primeira coluna listas os atributos associados a pelo menos um cluster. O resto do visualizador contém a distribuição dos estados de um atributo para cada cluster. A distribuição de uma variável discreta é mostrada como uma barra colorida com o número máximo de barras exibidas na **barras de histograma** lista. São exibidos atributos contínuos com um gráfico de diamante que representa o desvio médio e padrão em cada cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Para explorar o modelo na guia Perfis de Cluster  
  
1.  Definir **histograma** as barras **5**.  
  
     Em nosso modelo, 5 é o número máximo de estados para qualquer variável.  
  
2.  Se o **legenda de mineração** bloquear a exibição da **perfis de atributo**, movê-lo fora do caminho.  
  
3.  Selecione o **altos compradores de bicicleta** coluna e arraste-o à direita do **população** coluna.  
  
4.  Selecione o **baixos compradores de bicicleta** coluna e arraste-o à direita do **altos compradores de bicicleta** coluna.  
  
5.  Clique o **altos compradores de bicicleta** coluna.  
  
     O **variáveis** coluna é classificada em ordem de importância para esse cluster. Navegue pela coluna e examine as características do cluster Altos Compradores de Bicicleta. Por exemplo, é mais provável que eles tenham um caminho curto para o trabalho.  
  
6.  Clique duas vezes o **idade** célula a **altos compradores de bicicleta** coluna.  
  
     O **legenda de mineração** exibe mais detalhada exibição e você pode ver o intervalo de idade desses clientes, bem como a idade média.  
  
7.  Clique com botão direito do **baixos compradores de bicicleta** coluna e selecione **Ocultar coluna**.  
  

  
##  <a name="ClusterCharacteristicsTab"></a> Guia características do cluster  
 Com o **características do Cluster** guia, você pode examinar mais detalhadamente as características que compõem um cluster. Em vez de comparar as características de todos os clusters (como na guia Perfis de Cluster), você pode explorar um cluster por vez. Por exemplo, se você selecionar **altos compradores de bicicleta** da **Cluster** lista, você pode ver as características dos clientes neste cluster. Embora a exibição seja diferente do visualizador Perfis de Cluster, as informações são as mesmas.  
  
> [!NOTE]  
>  A menos que você defina um valor inicial para **holdoutseed**, os resultados irão variar sempre que você processar o modelo. Para obter mais informações, consulte [elemento HoldoutSeed](../analysis-services/scripting/properties/holdoutseed-element.md)  
  

  
##  <a name="ClusterDiscriminationTab"></a> Guia discriminação de cluster  
 Com o **discriminação do Cluster** guia, você pode explorar as características que distinguem um cluster de outro. Depois de selecionar dois clusters, um do **Cluster 1** lista e uma da **Cluster 2** lista, o visualizador calculará as diferenças entre os clusters e exibe uma lista dos atributos que distinguem os clusters.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Para explorar o modelo na guia Distinção de Cluster  
  
1.  No **Cluster 1** caixa, selecione **altos compradores de bicicleta**.  
  
2.  No **Cluster 2** caixa, selecione **baixos compradores de bicicleta**.  
  
3.  Clique em **variáveis** para classificar em ordem alfabética.  
  
     Algumas das diferenças mais significativas entre os clientes nos **baixos compradores de bicicleta** e **altos compradores de bicicleta** clusters incluem idade, propriedade de carros, número de filhos e região.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte os tópicos a seguir para explorar os outros modelos de mineração.  
  
-   [Explorando o modelo de árvore de decisão &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o modelo Naive Bayes &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando o modelo Naive Bayes &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Explorando o modelo de árvore de decisão &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Procurar um modelo usando o Visualizador de Cluster da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Guia discriminação de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Guia Perfis de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Guia características do cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Guia diagrama de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
