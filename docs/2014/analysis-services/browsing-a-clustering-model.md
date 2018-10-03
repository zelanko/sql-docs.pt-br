---
title: Procurando um modelo de Clustering | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- clustering [data mining]
- mining model, clustering
ms.assetid: 7f3f0949-d791-403a-88e2-54cb1a803dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c994b43bda37981d7073d0ee16f32369677e244e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060406"
---
# <a name="browsing-a-clustering-model"></a>Procurando um modelo de clustering
  Quando você abre um modelo de clustering usando **navegue**, o modelo é exibido em um visualizador interativo, semelhante ao Visualizador de clustering no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O visualizador ajuda a explorar os clusters que foram criados e compreender características do cluster. Você também pode comparar e contrastar segmentos individuais com outros segmentos ou com a população.  
  
##  <a name="BKMK_Tabs"></a> Explorar o modelo  
 O **procurar** janela inclui as seguintes ferramentas para ajudá-lo a entender o modelo de clustering e explorar os atributos dos grupos de dados subjacente:  
  
-   [Diagrama de cluster](#BKMK_ClusterDiagram)  
  
-   [Perfis de cluster](#BKMK_ClusterProfiles)  
  
-   [Características do cluster](#BKMK_ClusterCharacteristics)  
  
-   [Discriminação do cluster](#BKMK_ClusterDiscrimination)  
  
 Para fazer experiências com um modelo de clustering, você pode usar os dados de exemplo na guia treinamento da pasta de trabalho de dados de exemplo e criar um modelo de clustering usando [Assistente de Cluster &#40;Data Mining Add-ins para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) e todos os padrões .  
  
###  <a name="BKMK_ClusterDiagram"></a> Diagrama de cluster  
 O **diagrama de Cluster** guia exibe todos os clusters que estão em um modelo de mineração. Aqui você pode ver quantos agrupamentos diferentes foram encontrados no conjunto de dados e a distância entre eles.  
  
##### <a name="explore-the-cluster-diagram"></a>Explorar o diagrama de cluster  
  
1.  Clique no cluster 1 no diagrama.  
  
     Observe como as linhas cinza que conectam todos os clusters mudam de modo que as linhas que vão até o cluster selecionado são destacadas em azul brilhante.  
  
     ![Introdução ao diagrama de cluster](media/dm13-cluster-diagram-intro.gif "Introdução ao diagrama de cluster")  
  
     A intensidade da linha que conecta um cluster a outro expressa o grau de semelhança entre os clusters. Um sombreamento claro ou a ausência dele indica que os clusters não são muito parecidos. Quanto mais escura a linha, mais forte a semelhança entre os dois clusters.  
  
2.  Clique e arraste o controle deslizante para a esquerda do diagrama de cluster para ajustar o número de linhas exibido no visualizador.  
  
     Quando você arrasta o controle deslizante para baixo, apenas os links mais importantes entre os clusters são mostrados. Isso ajuda a se concentrar nos grupos relacionados.  
  
3.  Observe que o **variável de sombreamento** controle no canto superior direito da **diagrama de Cluster** janela.  
  
     Por padrão, ele é definido como **população**. O que isso significa é que os clusters mais escuros têm o maior suporte.  
  
4.  Pause sobre qualquer cluster com o cursor.  
  
     Uma dica de ferramenta é exibida que contém a população daquele cluster.  
  
5.  Agora, clique o **variável de sombreamento** dropdown lista e escolha o **idade** variável. Conforme você faz isso, é exibida uma lista de valores na **estado** caixa de texto.  
  
     A coluna Idade usada como entrada para este modelo contém valores numéricos contínuos, mas, para a finalidade de clustering, o algoritmo sempre discretiza números. Aqui você pode ver os compartimentos ou grupos que o algoritmo criou, como "muito baixo (\<= 27)" e "muito alto (> = 63)".  
  
6.  Dos **estado** listas suspensas, selecione **muito alta** e veja como o diagrama muda.  
  
     Ao alterar a variável de sombreamento, você pode ter uma noção de quais clusters contêm mais dessa faixa etária de destino e quais clusters contêm muito poucos clientes nessa faixa etária.  
  
     ![Modificar o diagrama de cluster para mostrar a idade](media/dm13-cluster-diagramshadebyage.gif "modificar o diagrama de cluster para mostrar a idade")  
  
     Quanto mais escuro o sombreamento, maior a proporção do atributo de destino e a distribuição de valor desse cluster  
  
7.  Localize o cluster que está sombreado mais escuro quando a **variável de sombreamento** estiver definida como idade > 65.  
  
     Passe o mouse sobre o cluster.  
  
     O valor exibido na dica de ferramenta mostra a população de clientes neste cluster que tenha mais de 65.  
  
8.  O cluster com o botão direito e selecione **renomear Cluster**. Digite um novo nome descritivo, como **mais de 65**. O novo nome será salvo com o modelo no servidor e poderá ser usado para identificar o cluster nas outras exibições de clustering.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterProfiles"></a> Perfis de cluster  
 O **perfis de Cluster** guia permite que você compare a composição de todos os clusters em um relance. Este é um bom local para iniciar quando você estiver se familiarizado com o modelo. Esta exibição também será útil posteriormente, se você explorou um cluster específico e decidir que precisa localizar os relacionados.  
  
 **Perfis de cluster** também lhe dá uma boa visão geral de como os clusters são diferentes uns dos outros. Consequentemente, pode ser conveniente usar essa exibição para dar a cada cluster um nome descritivo.  
  
##### <a name="explore-the-cluster-profiles"></a>Explorar os perfis de cluster  
  
1.  Clique na célula para ocupações, na **estados** coluna, para ver a lista de todos os valores para ocupação.  
  
2.  Agora mova o cursor sobre Ocupação nos perfis de cluster.  
  
     A dica de ferramenta mostra a distribuição das ocupações nesse cluster.  
  
     ![Exibir os valores detalhados em dicas de ferramenta ou na legenda](media/dm13-cluster-profile-age-tooltip.gif "exibir os valores detalhados em dicas de ferramenta ou na legenda")  
  
     Observe que, em alguns clusters (como aquele no gráfico), a lista de ocupações não está completa e algumas ocupações são substituídas com o rótulo **outros**.  
  
     Isso é proposital, pois pode ser difícil saber a diferença entre muitas barras pequenas em um histograma. Por padrão somente as barras de maior importância serão retidas e as barras restantes serão agrupadas em um cinza **outros** bucket.  
  
     Para alterar o número de barras visíveis em qualquer histograma, use a opção **barras de histograma**.  
  
3.  Observe que o **idade** coluna tem uma aparência diferente dos outros. Clique no losango no gráfico usado para representar a idade.  
  
     A coluna Idade originalmente continha somente números contínuos. O algoritmo de clustering exige valores discretos e, portanto, agrupava os valores numéricos na coluna Idade em um número limitado de grupos de idade, com base na distribuição de valores.  
  
4.  Clique em um dos gráficos de losangos em um perfil de cluster.  
  
     Esses gráficos de losangos são exibidos somente quando os dados de origem usam valores numéricos contínuos. Os gráficos de losango fornecem algumas estatísticas descritivas úteis, inclusive o desvio médio e o padrão para esse valor em cada cluster:  
  
    -   A linha no gráfico de losangos representa o intervalo de valores para o atributo. Os valores também são mostrados na **estados** coluna à esquerda do **perfis** gráfico.  
  
    -   O centro do losango está posicionado na média para o nó.  
  
    -   A largura do losango representa a variação do atributo nesse nó. Portanto, um losango mais estreito indica que o nó pode criar uma previsão mais precisa.  
  
5.  Para ter mais espaço no gráfico, clique com botão direito um cluster que você não precisa exibir imediatamente e, em seguida, selecione **Ocultar coluna**. Isso não a exclui do modelo, apenas recolhe a coluna temporariamente.  
  
     Para exibir clusters que você ocultou, você pode clique e arraste a borda da coluna ou selecione o nome do cluster na lista, **mais clusters**.  
  
6.  Percorra a lista de atributos até localizar o comprador de bicicletas (Bike Buyer) e localize o cluster com a maior porcentagem de valores Sim.  
  
     Clique com botão direito no cabeçalho da coluna para o cluster que você deseja renomear, selecione **renomear cluster**e digite **compradores de bicicleta**.  
  
     O novo nome do cluster é persistido em todas as exibições e no servidor, até que você reprocesse o modelo.  
  
     ![Renomear clusters para facilitar o uso do gráfico](media/dm13-cluster-rename.gif "renomear clusters para facilitar o uso do gráfico")  
  
 **Dicas**  
  
-   Clique em um cabeçalho de coluna para classificar os atributos em ordem de importância para aquele cluster.  
  
-   Arraste as colunas para reordená-las no visualizador.  
  
-   Clique em qualquer célula no gráfico de perfis para exibir as estatísticas detalhadas na **legenda de mineração**.  
  
-   Clique em qualquer célula e selecione **colunas do modelo de detalhamento** para gerar os dados subjacentes em uma nova planilha no Excel.  
  
-   Clique com botão direito da coluna do cluster título e selecione **detalhamento para estruturar dados** para obter informações detalhadas sobre os membros do cluster que não estavam incluídas no modelo.  
  
     Por exemplo, se você estiver criando perfis de clientes, poderá deixar as informações de contato nos dados subjacentes (a estrutura de mineração), mas não a incluir no modelo, pois não é útil para a análise. Entretanto, depois que os clientes foram atribuídos aos clusters, você poderá exibir os dados detalhados usando o detalhamento.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterCharacteristics"></a> Características do cluster  
 A exibição Características do Cluster permite que você realmente explore um único cluster, para localizar os atributos que caracterizam mais fortemente esse grupo de dados.  
  
##### <a name="explore-the-cluster-characteristics"></a>Explorar as características do cluster  
  
1.  Selecione o **mais de 65** cluster a partir de **Cluster** lista.  
  
     Depois de selecionado um cluster, é possível ver em detalhes as características particulares daquele cluster específico.  
  
     Os atributos contidos no cluster são listados nas colunas **Variáveis** , e o estado do atributo listado é relacionado na coluna **Valores** .  
  
     Estados de atributo são listados em ordem de importância, acompanhada pela probabilidade nesse cluster, representado como uma barra colorida na **probabilidade** coluna.  
  
     ![Características de um modelo de clustering](media/dm13-cluster-characteristics.gif "características de um modelo de clustering")  
  
2.  Clique o **variáveis** coluna para classificar por atributo.  
  
     Ao alterar a variável de classificação, você poderá ver mais facilmente como os valores das variáveis como renda ou propriedade de carros são distribuídos no grupo.  
  
3.  Clique em **copiar para Excel**.  
  
     Uma nova planilha é adicionada à pasta de trabalho que contém as características do cluster selecionado.  
  
4.  Agora, escolha um cluster diferente na lista, **compradores de bicicleta**.  
  
5.  Clique em **copiar para Excel**.  
  
     Observe que o gráfico das características do novo cluster é adicionado em sua própria planilha. Você pode movê-lo para a mesma planilha que o outro perfil para facilitar a comparação entre eles, o que você fará na próxima etapa.  
  
 **Dicas**  
  
-   Observe que a característica principal do cliente no cluster Mais de 65 é que ele não compra seu produto! Se você quiser saber por que isso acontece, poderá procurar clusters e comparar grupos ou poderá criar um modelo relacionado usando um algoritmo que é bom em explorar causas e resultados, como, por exemplo, um modelo de árvore de decisão ou um modelo Naïve Bayes.  
  
-   Se você quiser obter uma lista completa de atributos e probabilidades para este cluster (ou todos os clusters) poderá criar uma consulta. Para obter exemplos de consultas em modelos de clustering, consulte [exemplos de consulta de modelo de Clustering](data-mining/clustering-model-query-examples.md).  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterDiscrimination"></a> Discriminação do cluster  
 Você usa o **discriminação do Cluster** guia para comparar atributos entre dois clusters ou entre um cluster e todos os outros casos no conjunto de dados.  
  
 Para realçar os recursos deste visualizador, vamos compará-lo para as tabelas de lado a lado no Excel que você criou com base nas **características do Cluster** modo de exibição.  
  
##### <a name="explore-cluster-discrimination"></a>Explorar distinção de cluster  
  
1.  Use as listas **Cluster 1** e **Cluster 2** para selecionar os clusters a serem comparados.  
  
    -   Para o cluster 1, selecione Mais de 65.  
  
    -   Para o cluster 2, selecione Bike Buyers.  
  
     A comparação deve ter aparência semelhante ao gráfico a seguir.  
  
     ![Comparando clusters em um modelo](media/dm13-cluster-compareclusters.gif "comparar clusters em um modelo")  
  
     Observe que, nos bastidores, o **discriminação do Cluster** visualizador envia consultas complexas para o servidor de mineração de dados, para extrair os atributos que são mais importantes na distinção entre os dois grupos, tornando mais fácil comparar dois conjuntos de clientes.  
  
2.  Clique em qualquer uma da **favorece...** colunas.  
  
     A barra à direita do atributo e da lista de valores mostra quais recursos ou valores são mais importantes como uma característica do cluster selecionado.  
  
3.  Agora compare as listas no Excel.  
  
     ![Gráfico de rede de dependência para um modelo de associação](media/dm13-comparing-profiles-in-excel.gif "grafo de rede de dependência para um modelo de associação")  
  
     Como as estatísticas subjacentes que foram usadas para criar a imagem no visualizador são salvas no Excel como tabelas, você pode filtrar e classificar, e exibir os valores reais de probabilidade.  
  
     Além de usar o Excel, recomendamos que você tente o visualizador de cluster para o Visio, que também permite que você exiba não apenas pontos de dados, mas também extensivamente modifique e aprimore o gráfico. Para obter mais informações, consulte [passo a passo de diagrama de Cluster &#40;Data Mining Add-ins&#41;](cluster-diagram-walkthrough-data-mining-add-ins.md).  
  
 **Dicas**  
  
 Depois de obter visões sobre grupos de clientes, tente usar o [cenário de teste de hipóteses &#40;ferramentas de análise de tabela para Excel&#41; ](what-if-scenario-table-analysis-tools-for-excel.md) ou [cenário de atingir meta &#40;ferramentas de análise de tabela para Excel&#41; ](goal-seek-scenario-table-analysis-tools-for-excel.md) ferramentas para explorar fatores no modelo que pode ser alterado para afetar o resultado.  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)   
 [Assistente de cluster &#40;Data Mining Add-ins para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
  
