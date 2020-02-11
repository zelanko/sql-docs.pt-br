---
title: Explorando o modelo de clustering (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63280428"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Explorando o modelo de clustering (Tutorial de mineração de dados básico)
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clustering agrupa casos em clusters que contêm características semelhantes. Esses agrupamentos são úteis para explorar dados, identificando anomalias nos dados e criar previsões.  
  
 O Visualizador de Cluster da [!INCLUDE[msCoName](../includes/msconame-md.md)] fornece as seguintes guias para serem usadas na exploração de modelos de mineração de cluster:  
  

  
##  <a name="ClusterDiagramTab"></a>Guia diagrama de cluster  
 A guia Diagrama de Cluster exibe todos os clusters existentes em um modelo de mineração. As linhas entre os clusters representam "proximidade" e estão sombreadas com base no grau de semelhança que os clusters têm. A cor real de cada cluster representa a frequência da variável e o estado no cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Para explorar o modelo na guia Diagrama de Cluster  
  
1.  Use a lista **modelo de mineração** na parte superior da guia Visualizador do modelo de **mineração** para alternar `TM_Clustering` para o modelo.  
  
2.  Na lista **Visualizador** , selecione **Visualizador de cluster da Microsoft**.  
  
3.  Na caixa **variável de sombreamento** , selecione **comprador de bicicleta**.  
  
     A variável padrão é **população**, mas você pode alterá-la para qualquer atributo no modelo, para descobrir quais clusters contêm membros que têm os atributos desejados.  
  
4.  Selecione **1** na caixa **estado** para explorar os casos em que uma bicicleta foi comprada.  
  
     A legenda de **densidade** descreve a densidade do par de estado de atributo selecionado na variável de sombreamento e o estado. Neste exemplo, ele nos informa que a clusterwith do sombreamento mais escuro tem o percentual mais alto de compradores de bicicletas.  
  
5.  Coloque o seu mouse sobre o cluster com o sombreamento mais escuro.  
  
     Uma dica de ferramenta exibe a porcentagem de casos que têm o atributo `Bike Buyer = 1`.  
  
6.  Selecione o cluster que tem a densidade mais alta, clique com o botão direito do mouse no cluster, selecione **renomear cluster** e tipo **compradores de bicicletas alto** para identificação posterior. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Localize o cluster com o sombreamento mais claro (e a menor densidade). Clique com o botão direito do mouse no cluster, selecione **renomear cluster** e tipo de **compradores de bicicleta baixo**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Clique no cluster de **compradores de bicicletas alto** e arraste-o para uma área do painel que lhe dará uma visão clara de suas conexões com os outros clusters.  
  
     Quando você seleciona um cluster, as linhas que conectam esse cluster a outros são realçadas para que você possa facilmente ver todas as relações desse cluster. Quando o cluster não estiver selecionado, você poderá dizer pela escuridão das linhas o grau de importância das relações entre todos os clusters do diagrama. Um sombreamento claro ou a ausência dele indica que os clusters não são muito parecidos.  
  
9. Use o controle deslizante à esquerda da rede para filtrar os links menos importantes e encontrar os clusters com relações mais próximas. O departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] pode querer combinar clusters similares na determinação do melhor método de entrega da mala direta.  
  

  
##  <a name="ClusterProfilesTab"></a>Guia perfis de cluster  
 A guia **perfis de cluster** fornece uma visão geral do `TM_Clustering` modelo. A guia **perfis de cluster** contém uma coluna para cada cluster no modelo. A primeira coluna listas os atributos associados a pelo menos um cluster. O resto do visualizador contém a distribuição dos estados de um atributo para cada cluster. A distribuição de uma variável discreta é mostrada como uma barra colorida com o número máximo de barras exibidas na lista de **barras de histograma** . São exibidos atributos contínuos com um gráfico de diamante que representa o desvio médio e padrão em cada cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Para explorar o modelo na guia Perfis de Cluster  
  
1.  Defina as barras de **histograma** como **5**.  
  
     Em nosso modelo, 5 é o número máximo de estados para qualquer variável.  
  
2.  Se a **legenda de mineração** bloquear a exibição dos **perfis de atributo**, mova-o para fora do caminho.  
  
3.  Selecione a coluna **alto dos compradores de bicicleta** e arraste-a para a direita da coluna de **população** .  
  
4.  Selecione a coluna de **compradores de bicicletas de baixa** e arraste-a para a direita da coluna alto dos compradores de **bicicletas** .  
  
5.  Clique na coluna **alto dos compradores de bicicletas** .  
  
     A coluna **Variables** é classificada em ordem de importância para esse cluster. Navegue pela coluna e examine as características do cluster Altos Compradores de Bicicleta. Por exemplo, é mais provável que eles tenham um caminho curto para o trabalho.  
  
6.  Clique duas vezes na célula **age** na coluna **alta dos compradores de bicicletas** .  
  
     A **legenda de mineração** exibe uma exibição mais detalhada e você pode ver a faixa etária desses clientes, bem como a idade média.  
  
7.  Clique com o botão direito do mouse na coluna de **compradores de bicicletas baixo** e selecione **Ocultar coluna**.  
  

  
##  <a name="ClusterCharacteristicsTab"></a>Guia características do cluster  
 Com a guia **características do cluster** , você pode examinar mais detalhadamente as características que compõem um cluster. Em vez de comparar as características de todos os clusters (como na guia Perfis de Cluster), você pode explorar um cluster por vez. Por exemplo, se você selecionar **compradores de bicicleta alto** na lista de **clusters** , poderá ver as características dos clientes neste cluster. Embora a exibição seja diferente do visualizador Perfis de Cluster, as informações são as mesmas.  
  
> [!NOTE]  
>  A menos que você defina um valor inicial para **HoldoutSeed**, os resultados variarão cada vez que você processar o modelo. Para obter mais informações, consulte [elemento HoldoutSeed](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="ClusterDiscriminationTab"></a>Guia discriminação de cluster  
 Com a guia **discriminação de cluster** , você pode explorar as características que distinguem um cluster de outro. Depois de selecionar dois clusters, um da lista **cluster 1** e outro na lista **cluster 2** , o visualizador calcula as diferenças entre os clusters e exibe uma lista dos atributos que distinguem os clusters.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Para explorar o modelo na guia Distinção de Cluster  
  
1.  Na caixa **cluster 1** , selecione **compradores de bicicleta alto**.  
  
2.  Na caixa **cluster 2** , selecione **compradores de bicicleta baixo**.  
  
3.  Clique em **variáveis** para classificar em ordem alfabética.  
  
     Algumas das diferenças mais substanciais entre os clientes nos **compradores de bicicletas baixos** e os **compradores de bicicletas altos** são os clusters com idade, Propriedade do carro, número de filhos e região.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte os tópicos a seguir para explorar os outros modelos de mineração.  
  
-   [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o Naive Bayes do modelo de mineração de dados &#40;Basic&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando o Naive Bayes do modelo de mineração de dados &#40;Basic&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Procurar um modelo usando o Visualizador de cluster da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Guia discriminação de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Guia perfis de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Guia características do cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Guia diagrama de cluster &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
