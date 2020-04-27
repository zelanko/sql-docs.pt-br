---
title: Explorando o modelo de clustering de sequências (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e0904239933361b80727700c94b03e379751251f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63164058"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Explorando o modelo de clustering de sequências (Tutorial de mineração de dados intermediário)
  Agora que você criou o **clustering de sequência com** o modelo de região, você pode explorá- [!INCLUDE[msCoName](../includes/msconame-md.md)] lo usando o Visualizador de clustering de sequência na guia **Visualizador do modelo de mineração** do designer de mineração de dados. O [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de cluster de sequência contém cinco guias: **diagrama de cluster**, **perfis**de cluster, **características de cluster**, **ClusterDiscrimination**e **transições de estado**. Para obter mais informações sobre como usar esse visualizador, consulte [procurar um modelo usando o Visualizador de cluster de sequência da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
-   [Guia diagrama de cluster](#bkmk_CDiagram)  
  
-   [Guia perfis de cluster](#bkmk_CProfiles)  
  
-   [Guia características do cluster](#bkmk_CChars)  
  
-   [Guia discriminação de cluster](#bkmk_CDiscrim2)  
  
-   [Guia Transições de Estado](#bkmk_StateTran)  
  
-   [Visualizador de Conteúdo Genérico](#bkmk_Generic)  
  
##  <a name="cluster-diagram-tab"></a><a name="bkmk_CDiagram"></a>Guia diagrama de cluster  
 A guia **diagrama de cluster** exibe graficamente os clusters que o algoritmo descobriu no banco de dados. O layout do diagrama representa as relações dos clusters, com clusters semelhantes agrupados juntos. Por padrão, a sombra de cada nó nó representa a densidade de todos os casos no cluster: quanto mais escuro o sombreamento do nó, mais casos ele conterá. Você pode alterar o significado do sombreamento dos nós para que ele represente suporte, em cada cluster, a um atributo e a um estado.  
  
 Você também pode renomear os clusters para facilitar a identificação e o trabalho com os clusters de destino. Para este tutorial, você renomeará o cluster com a maior porcentagem de clientes da região do Pacífico e o cluster com mais casos.  
  
> [!NOTE]  
>  Os casos atribuídos a clusters específicos podem mudar quando você reprocessar o modelo, dependendo dos dados e dos parâmetros do modelo. Além disso, se você renomear clusters, os nomes serão perdidos no reprocessamento do modelo de mineração.  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>Para alterar o atributo usado para realçar clusters  
  
1.  Na lista **variável de sombreamento** , selecione **modelo**.  
  
2.  Selecione **limite de ciclo** na lista **estado** .  
  
     O diagrama é atualizado para mostrar a concentração do produto selecionado em cada um dos clusters. O cluster no diagrama com o sombreamento mais escuro contém a densidade mais alta de capacetes para ciclismo. Você pode alterar a variável de sombreamento para usar qualquer estado de qualquer coluna de entrada.  
  
3.  Na lista **variável de sombreamento** , selecione **população**.  
  
     Quando você altera a variável de sombreamento para população, o diagrama é atualizado para comparar os clusters por tamanho. O cluster no diagrama com o sombreamento mais escuro contém mais casos do que os outros clusters.  
  
#### <a name="to-rename-nodes-in-the-model"></a>Para renomear nós no modelo  
  
1.  Altere a **variável de sombreamento** para `Region`e defina o **estado** para o **Pacífico**.  
  
2.  Realce o nó mais escuro no gráfico.  
  
3.  Clique com o botão direito do mouse nesse cluster e selecione **renomear cluster.**  
  
4.  Digite o nome**cluster do Pacífico.**  
  
5.  Altere o valor da **variável de sombreamento** para **população**.  
  
6.  No gráfico atualizado, localize o cluster mais escuro, que deverá ser o maior. Se você não conseguir saber, pelo sombreamento, que cluster é o maior, coloque o mouse sobre cada cluster e exiba a Dica de Ferramenta e escolha o cluster que contém mais casos.  
  
7.  Clique com o botão direito do mouse nesse cluster e selecione **renomear cluster**. Digite o novo nome, `Largest Cluster`.  
  
 Você pode detalhar o nó que representa o cluster para exibir detalhes dos casos de cada cluster. Isso pode ser útil caso você queira executar uma ação sobre os resultados da sua análise, como o envio de um email ao cliente. Você também pode navegar por outros atributos dos casos incluídos na estrutura mas que não foram usados no modelo, como Região e IncomeGroup. Para obter mais informações sobre como fazer drill-through de modelos de mineração para os casos subjacentes, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>Para detalhar o diagrama Cluster  
  
1.  Clique `Pacific Cluster`com o botão direito do mouse, selecione **detalhar**e, em seguida, selecione **colunas de modelo e estrutura**.  
  
     A caixa de diálogo **Drill-through** é aberta. As colunas que não são usadas no modelo, mas que estão disponíveis para consulta, são prefixadas com **estrutura**.  
  
     Você pode ver que esse cluster contém como maioria clientes da região do Pacífico, com somente alguns poucos clientes de outras regiões.  
  
2.  Clique no sinal de mais na coluna aninhada v Assoc Seq Line Items para exibir a sequência de itens em uma determinada ordem de clientes.  
  
3.  Feche a caixa de diálogo **Drill-through** .  
  
    > [!NOTE]  
    >  O botão **Play** permite que você repita a consulta dos dados; no entanto, a reconsulta não altera os dados que são exibidos, a menos que o modelo tenha sido atualizado dinamicamente em segundo plano por algum outro processo.  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
##  <a name="cluster-profiles-tab"></a><a name="bkmk_CProfiles"></a>Guia perfis de cluster  
 A guia **perfis de cluster** exibe as sequências que estão em cada cluster. Os clusters são listados em colunas individuais à direita da coluna **Estados** .  
  
 No visualizador, a linha de **modelo** descreve a distribuição geral de itens em um cluster e a linha **Model. Samples** contém sequências dos itens. Cada linha das sequências de cores em cada célula da linha **Model. Samples** representa o comportamento de um usuário selecionado aleatoriamente no cluster.  
  
 Cada cor em um histograma de sequência individual representa um modelo de produto. A Legenda de Mineração mostra as sequências de produtos usando a codificação de cores e os nomes de modelos do produto. Se você adicionou outras colunas ao modelo de clustering, como Região ou IncomeGroup, o visualizador conterá uma linha adicional para cada coluna, mostrando a distribuição desses valores em cada cluster.  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>Para exibir as sequências mais comuns em um cluster  
  
1.  Clique com o botão direito do mouse na linha **modelo** na coluna `Largest Cluster`do cluster e selecione **Mostrar Legenda**.  
  
     A coluna **Color** contém uma barra sombreada que indica a frequência dos itens encontrados em sequências. Cada item é representado por uma cor diferente. A coluna **significado** lista os nomes de modelo de produto para cada cor. A coluna de **distribuição** informa a porcentagem de casos que continham esse item em uma sequência.  
  
2.  Feche a **legenda de mineração**.  
  
3.  Clique com o botão direito do mouse na linha **Model. Samples** na coluna com o título, **população** e selecione **Mostrar Legenda**.  
  
4.  Examinar a lista de sequências no modelo geral`.`  
  
     A Legenda de Mineração lista as sequências mais comuns primeiro, para que você possa ver que o Tubo de Pneu para Mountain Bike é o primeiro item de muitas sequências. Isso significa que um cliente muito provavelmente coloca o Tubo de Pneu pra Mountain Bike primeiro na cesta de compras.  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>Para detalhar casos a partir do visualizador de clusters  
  
1.  Role para baixo no painel atributo até encontrar a linha do `Region` atributo.  
  
     A linha contém um histograma para cada cluster no modelo, mais um histograma adicional para **população**, o que significa o conjunto inteiro de casos usados no modelo. Um histograma é uma barra com cores diferentes, onde cada cor representa um atributo e o tamanho da seção colorida desse atributo representa a sua porcentagem de casos.  
  
2.  Compare os histogramas para os clusters que você renomeou `Pacific Cluster` e `Largest Cluster`. Cada cluster aparece em uma coluna diferente.  
  
     Ambos têm cores sólidas, mas as cores são diferentes.  
  
3.  Na `Region` linha, pause o mouse sobre o histograma colorido para `Largest Cluster`.  
  
     A Dica de Ferramenta exibirá valores que mostram as porcentagens reais de casos de cada região.  
  
4.  Clique com o botão direito do mouse no `Region` histograma colorido `Pacific Cluster`na linha para, selecione **detalhar**e selecione **apenas colunas de modelo**.  
  
5.  Mova a barra de rolagem para revisar todos os clientes desse cluster.  
  
     Novamente, a partir do detalhamento, é possível ver que o cluster contém, em grande parte, pedidos da região do Pacífico, mas também alguns das regiões da América do Norte e da Europa.  
  
6.  Feche a caixa de diálogo **Drill-through** .  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
##  <a name="cluster-characteristics-tab"></a><a name="bkmk_CChars"></a>Guia características do cluster  
 A guia **características do cluster** resume as transições entre os Estados em um cluster exibindo barras que representam visualmente a importância do valor do atributo para o cluster selecionado. A coluna **variáveis** informa o que o modelo encontrou para ser importante para o cluster ou população selecionado: um valor específico ou a relação entre valores, conhecida como *transição*. A coluna **valores** fornece mais detalhes sobre o valor ou a transição, e a coluna **probabilidade** representa visualmente o peso desse atributo ou da transição.  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>Para exibir os atributos importantes para um cluster  
  
1.  Na lista suspensa **cluster** , selecione `Pacific Cluster`.  
  
     A lista é atualizada para mostrar as características do cluster que você renomeou `Pacific Cluster`. Nesse cluster, a característica mais importante é `Region`.  
  
2.  Pause o mouse sobre a barra sombreada na linha para `Region`.  
  
     A probabilidade do valor ser Pacífico é muito alta. Para obter mais informações sobre como interpretar esses valores, consulte [referência técnica do algoritmo Microsoft Sequence clustering](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
3.  Examine a lista de características do cluster até localizar a primeira linha de transição.  
  
4.  Uma linha de transição contém a transição de texto na coluna **variáveis** e uma combinação de valores de atributo sequenciais na coluna **valor** . A sequência também pode conter pontos iniciais e valores ausentes.  
  
     Por exemplo, suponha que a transição tenha o valor [início]-> tubo de aro de estrada. Isso significa que clientes deste cluster colocam com frequência o Tubo de Pneu de Estrada em sua cesta de compras. Isso poderia significar que o produto é um item popular e procurado primeiro por clientes, ou pode simplesmente indicar que o produto é fácil de localizar no site de compras.  
  
5.  Percorra a lista até encontrar a primeira transição que não tem **[start]** ou **ausente** nela.  
  
     Por exemplo, suponha que você encontre a transição, **aro de passeio, tubo de aro de passeio**. Isso significa que clientes deste cluster com frequência compraram esses itens juntos, exatamente nessa ordem.  
  
6.  Coloque o mouse sobre a barra sombreada para essa transição.  
  
     A probabilidade dessa transição é exibida como uma porcentagem.  
  
7.  Na lista suspensa **cluster** , selecione **população (tudo)**.  
  
     A lista de atributos é atualizada para mostrar as características de todas as ordens usadas na criação do modelo. Nesse modelo de mineração, a característica mais importante para distinguir entre clusters é `Region`, com um valor de **América do Norte**.  
  
 Depois de revisar essas tarefas, você percebe duas coisas. A primeira é que precisa de muitos dados para obter um número significativo de combinações. Por exemplo, as sequências com as probabilidades mais altas provavelmente incluirão um estado **[início]** ou **ausente** .  
  
 O segundo é que há um forte efeito de clustering nos atributos para `Region`, o que dificulta a visualização dos grupos de sequências. Dessa forma, você decide criar outro modelo que use somente sequências e que não inclua as colunas para região ou renda.  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
##  <a name="cluster-discrimination-tab"></a><a name="bkmk_CDiscrim2"></a>Guia discriminação de cluster  
 A guia **discriminação de cluster** ajuda a comparar dois clusters, para determinar quais atributos distinguem um cluster específico de outro cluster. A guia contém quatro colunas: **variáveis**, **valores**, **cluster 1**e **cluster 2**.  Você pode escolher qualquer cluster para usar como **cluster 1** e **cluster 2**.  
  
 A coluna **variáveis** informa o nome do atributo, que pode ser um nome de coluna ou uma combinação de nome de coluna e a palavra **transição**. A coluna **valores** mostra o valor exato do atributo ou a transição. As barras sombreadas nas colunas do **cluster 1** e do **cluster 2** indicam a força do atributo nos clusters que você está comparando. Quanto mais longa for a barra, mais será provável que o cluster inclua casos com esse atributo.  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>Para comparar dois clusters usando a guia Distinção de Cluster  
  
1.  Na guia **discriminação de cluster** , para **cluster 1**, selecione `Pacific Cluster`.  
  
     Por padrão, a seleção de **cluster 2** muda para o **complemento do cluster do Pacífico**.  
  
     O atributo superior que se distingue `Pacific Cluster` de todos os outros casos é a região. A região é um atributo tão forte para o clustering que obscurece outros atributos. Para impedir esse efeito, tente comparar vários clusters menores uns aos outros. Quando você fizer isso, a lista de atributos mudará e poderá incluir mais transições entre modelos.  
  
2.  Localize uma linha de transição e coloque o mouse sobre a barra sombreada.  
  
     Os itens na coluna **valores** podem incluir Estados e transições. O sombreamento de cada item indica a contagem de distinção. Para saber mais sobre o significado de pontuações diferentes, confira [conteúdo do modelo de mineração para modelos de clustering de sequência &#40;&#41;de mineração de dados Analysis Services ](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
##  <a name="state-transitions-tab"></a><a name="bkmk_StateTran"></a>Guia transições de estado  
 Na guia **transições de estado** , você pode selecionar um cluster e navegar pelas transições de estado. Se você selecionar **população (tudo)** na lista suspensa cluster, o diagrama mostrará a distribuição de Estados para todo o modelo de mineração.  
  
 Cada nó do gráfico representa um estado, ou um valor possível das sequências que você está tentando analisar. A cor de fundo dos nós representa a frequência do estado. As linhas conectam alguns estados, indicando uma transição entre eles. Você pode mover o controle deslizante para cima ou para baixo para alterar o limite de probabilidade para as transições. Os números são associados a alguns nós, indicando a probabilidade do estado.  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>Para explorar os relacionamentos na guia Transição de Estado  
  
1.  Na guia **transições de estado** do Visualizador do modelo de mineração, `Pacific Cluster` selecione na lista de clusters. Verifique se a opção **Mostrar rótulos de borda** está selecionada.  
  
     O gráfico é atualizado para mostrar as transições mais comuns desse cluster.  
  
2.  Clique em qualquer nó conectado por uma linha a outro nó.  
  
     O gráfico é atualizado e realça os nós relacionados. O valor numérico ao lado da linha indica a probabilidade da transição.  
  
3.  Gere o controle deslizante até **todos os links**para aumentar o número de transições incluídas no grafo.  
  
4.  Selecione **população (tudo)** do **cluster**.  
  
     Observe que quando você carrega um cluster diferente, o gráfico volta a ter as configurações de exibição padrão e, portanto, o controle deslizante é redefinido para a posição intermediária.  
  
5.  Clique no nó mais escuro no grafo, que deve ser **esporte-100**.  
  
     Observe que não há linhas conectando esse produto a outros.  
  
6.  Suba o controle deslizante uma etapa para aumentar o número de transições incluídas no gráfico. Não vá até **todos os links** ainda.  
  
     O gráfico será atualizado pela adição de várias outras transições, mas nenhuma que inclua o modelo Sport-100.  
  
7.  Mova o controle deslizante até todos os **links**. Clique no nó Sport-100 caso ele ainda não esteja selecionado.  
  
     O gráfico é atualizado para mostrar muitas transições que incluem o produto Sport-100. A direção da seta na linha de conexão mostra se o item Sport-100 foi selecionado como o primeiro ou o segundo item do par.  
  
8.  Clique no nó de Pneu de Passeio e mova o controle deslizante de volta à posição intermediária.  
  
     A princípio, há muitas linhas de transição conectando o aro de passeio a outros produtos, mas quando você aumenta o limite de probabilidade, as transições menos prováveis são eliminadas do grafo, deixando apenas a transição, o aro de passeio > tubo de aro de passeio. Essa transição significa que se um cliente colocar um Pneu de Passeio na cesta de compras, há uma grande probabilidade de que o cliente colocará em seguida um Tubo de Pneu de Passeio na cesta.  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
##  <a name="generic-content-tree-viewer"></a><a name="bkmk_Generic"></a>Visualizador de árvore de conteúdo genérica  
 Esse visualizador pode ser usado em todos os modelos, independentemente do algoritmo ou do tipo de modelo. O **Visualizador de árvore de conteúdo MicrosoftGeneric** está disponível na lista suspensa **Visualizador** .  
  
 Uma árvore de conteúdo é uma representação de qualquer modelo de mineração como uma série de nós, em que cada nó representa conhecimento adquirido sobre alguns dados de treinamento. O nó pode conter um padrão, um conjunto de regras, um cluster ou a definição de um intervalo de datas que compartilham alguns atributos. O conteúdo exato do nó difere dependendo do algoritmo e do tipo do atributo previsível; no entanto, a representação geral do conteúdo é a mesma.  
  
 É possível expandir os nós para consultar um maior número de detalhes, assim como copiar o conteúdo de qualquer um deles para a Área de Transferência. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>Para exibir detalhes de um modelo de clustering de sequências usando o Visualizador de Árvore de Conteúdo Genérica  
  
1.  Na guia **Visualizador do modelo de mineração** , clique na lista **Visualizador** e selecione **Visualizador de árvore de conteúdo genérica da Microsoft**.  
  
2.  No painel **legenda do nó** , clique `Pacific Cluster (1)`em.  
  
     O nome desse nó contém o nome amigável atribuído ao cluster e a ID do nó subjacente. Você pode usar as IDs do nó para detalhar ainda mais o modelo.  
  
3.  Expanda o primeiro nó filho, **nível de sequência nomeado para o cluster 1**.  
  
     O nó de nível de sequência para um cluster contém detalhes sobre os estados e transições incluídos naquele cluster. Você pode usar esses detalhes, disponíveis na coluna NODE_DISTRIBUTION, para explorar as sequências e os estados de cada cluster ou do modelo como um todo.  
  
4.  Continue a expandir nós e a exibir detalhes no painel visualizador de HTML.  
  
 Para obter mais informações sobre o conteúdo do modelo de mineração e como usar os detalhes no visualizador, consulte [conteúdo do modelo de mineração para modelos de clustering de sequência &#40;&#41;de mineração de dados de Analysis Services ](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Voltar ao início](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando um modelo de clustering de sequências relacionados &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo de clustering de sequência da Microsoft](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Sequence Clustering Model Query Examples](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
