---
title: Explorando o modelo de Sequence Clustering (Tutorial de mineração de dados intermediário) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024988"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Explorando o modelo de clustering de sequências (Tutorial de mineração de dados intermediário)
  Agora que você criou o **Clustering de sequências com região** modelo, você pode explorá-lo usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de Clustering de sequência no **Visualizador do modelo de mineração** guia do Designer de mineração de dados. O [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Cluster Viewer contém cinco guias: **Diagrama de cluster**, **perfis de Cluster**, **características de Cluster**, **ClusterDiscrimination**, e **detransiçõesdeestado**. Para obter mais informações sobre como usar esse visualizador, consulte [procurar um modelo usando o Microsoft Sequence Cluster Viewer](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
-   [Guia diagrama de cluster](#bkmk_CDiagram)  
  
-   [Guia Perfis de cluster](#bkmk_CProfiles)  
  
-   [Guia características do cluster](#bkmk_CChars)  
  
-   [Guia discriminação de cluster](#bkmk_CDiscrim2)  
  
-   [Guia transições de estado](#bkmk_StateTran)  
  
-   [Exibição de conteúdo genérica](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a> Guia diagrama de cluster  
 O **diagrama de Cluster** guia exibe graficamente os clusters que o algoritmo descobriu no banco de dados. O layout do diagrama representa as relações dos clusters, com clusters semelhantes agrupados juntos. Por padrão, a sombra de cada nó nó representa a densidade de todos os casos no cluster: quanto mais escuro o sombreamento do nó, mais casos ele conterá. Você pode alterar o significado do sombreamento dos nós para que ele represente suporte, em cada cluster, a um atributo e a um estado.  
  
 Você também pode renomear os clusters para facilitar a identificação e o trabalho com os clusters de destino. Para este tutorial, você renomeará o cluster com a maior porcentagem de clientes da região do Pacífico e o cluster com mais casos.  
  
> [!NOTE]  
>  Os casos atribuídos a clusters específicos podem mudar quando você reprocessar o modelo, dependendo dos dados e dos parâmetros do modelo. Além disso, se você renomear clusters, os nomes serão perdidos no reprocessamento do modelo de mineração.  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>Para alterar o atributo usado para realçar clusters  
  
1.  No **variável de sombreamento** lista, selecione **modelo**.  
  
2.  Selecione **Capacete para ciclismo** na **estado** lista.  
  
     O diagrama é atualizado para mostrar a concentração do produto selecionado em cada um dos clusters. O cluster no diagrama com o sombreamento mais escuro contém a densidade mais alta de capacetes para ciclismo. Você pode alterar a variável de sombreamento para usar qualquer estado de qualquer coluna de entrada.  
  
3.  No **variável de sombreamento** lista, selecione **população**.  
  
     Quando você altera a variável de sombreamento para população, o diagrama é atualizado para comparar os clusters por tamanho. O cluster no diagrama com o sombreamento mais escuro contém mais casos do que os outros clusters.  
  
#### <a name="to-rename-nodes-in-the-model"></a>Para renomear nós no modelo  
  
1.  Alteração **variável de sombreamento** à `Region`e defina **estado** para **Pacific**.  
  
2.  Realce o nó mais escuro no gráfico.  
  
3.  Este cluster com o botão direito e selecione **renomear Cluster.**  
  
4.  Digite o nome**Cluster do Pacífico.**  
  
5.  Altere o valor de **variável de sombreamento** à **população**.  
  
6.  No gráfico atualizado, localize o cluster mais escuro, que deverá ser o maior. Se você não conseguir saber, pelo sombreamento, que cluster é o maior, coloque o mouse sobre cada cluster e exiba a Dica de Ferramenta e escolha o cluster que contém mais casos.  
  
7.  Este cluster com o botão direito e selecione **renomear Cluster**. Digite o novo nome, `Largest Cluster`.  
  
 Você pode detalhar o nó que representa o cluster para exibir detalhes dos casos de cada cluster. Isso pode ser útil caso você queira executar uma ação sobre os resultados da sua análise, como o envio de um email ao cliente. Você também pode navegar por outros atributos dos casos incluídos na estrutura mas que não foram usados no modelo, como Região e IncomeGroup. Para obter mais informações sobre detalhamento de modelos de mineração para os casos subjacentes, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>Para detalhar o diagrama Cluster  
  
1.  Clique com botão direito `Pacific Cluster`, selecione **Detalhar**e, em seguida, selecione **colunas de modelo e estrutura**.  
  
     O **Detalhar** caixa de diálogo é aberta. Colunas que não são usados no modelo, mas que estão disponíveis para consulta têm o prefixo **estrutura**.  
  
     Você pode ver que esse cluster contém como maioria clientes da região do Pacífico, com somente alguns poucos clientes de outras regiões.  
  
2.  Clique no sinal de mais na coluna aninhada v Assoc Seq Line Items para exibir a sequência de itens em uma determinada ordem de clientes.  
  
3.  Fechar o **Detalhar** caixa de diálogo.  
  
    > [!NOTE]  
    >  O **reproduzir** botão permite que você consulte novamente os dados; no entanto, repetir a consulta não altera os dados que são exibidos, a menos que o modelo tenha sido dinamicamente atualizado em segundo plano por algum outro processo.  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a> Guia Perfis de cluster  
 O **perfis de Cluster** guia exibe as sequências que estão em cada cluster. Os clusters são listados em colunas individuais à direita do **estados** coluna.  
  
 No visualizador, o **modelo** linha descreve a distribuição geral de itens em um cluster e o **Samples** linha contém sequências dos itens. Cada linha das sequências de cores em cada célula de **Samples** linha representa o comportamento de um usuário selecionado aleatoriamente no cluster.  
  
 Cada cor em um histograma de sequência individual representa um modelo de produto. A Legenda de Mineração mostra as sequências de produtos usando a codificação de cores e os nomes de modelos do produto. Se você adicionou outras colunas ao modelo de clustering, como Região ou IncomeGroup, o visualizador conterá uma linha adicional para cada coluna, mostrando a distribuição desses valores em cada cluster.  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>Para exibir as sequências mais comuns em um cluster  
  
1.  Clique com botão direito do **modelo** linha da coluna para o cluster `Largest Cluster`e selecione **Mostrar legenda**.  
  
     O **cor** coluna contém uma barra sombreada que indica a frequência de itens encontrados em sequências. Cada item é representado por uma cor diferente. O **significado** coluna lista os nomes de modelo de produto para cada cor. O **distribuição** coluna informa a porcentagem de casos que contêm esse item em uma sequência.  
  
2.  Fechar o **legenda de mineração**.  
  
3.  Clique com botão direito do **Samples** linha da coluna com o título **população,** e selecione **Mostrar legenda**.  
  
4.  Examine a lista de sequências no modelo geral`.`  
  
     A Legenda de Mineração lista as sequências mais comuns primeiro, para que você possa ver que o Tubo de Pneu para Mountain Bike é o primeiro item de muitas sequências. Isso significa que um cliente muito provavelmente coloca o Tubo de Pneu pra Mountain Bike primeiro na cesta de compras.  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>Para detalhar casos a partir do visualizador de clusters  
  
1.  Role para baixo no painel atributo até localizar a linha para o `Region` atributo.  
  
     A linha contém um histograma para cada cluster no modelo, além de um histograma adicional para **população**, que significa que todo o conjunto de casos usados no modelo. Um histograma é uma barra com cores diferentes, onde cada cor representa um atributo e o tamanho da seção colorida desse atributo representa a sua porcentagem de casos.  
  
2.  Compare os histogramas de clusters que você renomeou `Pacific Cluster` e `Largest Cluster`. Cada cluster aparece em uma coluna diferente.  
  
     Ambos têm cores sólidas, mas as cores são diferentes.  
  
3.  No `Region` linha, coloque o mouse sobre o histograma colorido para `Largest Cluster`.  
  
     A Dica de Ferramenta exibirá valores que mostram as porcentagens reais de casos de cada região.  
  
4.  Clique com botão direito no histograma colorido na `Region` de linha para `Pacific Cluster`, selecione **Detalhar**e, em seguida, selecione **colunas do modelo somente**.  
  
5.  Mova a barra de rolagem para revisar todos os clientes desse cluster.  
  
     Novamente, a partir do detalhamento, é possível ver que o cluster contém, em grande parte, pedidos da região do Pacífico, mas também alguns das regiões da América do Norte e da Europa.  
  
6.  Fechar o **Detalhar** caixa de diálogo.  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a> Guia características do cluster  
 O **características do Cluster** guia resume as transições entre estados em um cluster exibindo barras que representam visualmente a importância do valor do atributo para o cluster selecionado. O **variáveis** coluna indica que o modelo encontrado para ser importante para o cluster ou população selecionados: um valor específico ou a relação entre valores, conhecidos como *transição*. O **valores** coluna fornece mais detalhes sobre o valor ou transição e o **probabilidade** coluna representa visualmente o peso desse atributo ou transição.  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>Para exibir os atributos importantes para um cluster  
  
1.  No **Cluster** lista suspensa, selecione `Pacific Cluster`.  
  
     A lista é atualizada para mostrar as características do cluster que você renomeou `Pacific Cluster`. Nesse cluster, a característica mais importante é `Region`.  
  
2.  Coloque o mouse sobre a barra sombreada na linha de `Region`.  
  
     A probabilidade do valor ser Pacífico é muito alta. Para obter mais informações sobre como interpretar esses valores, consulte [Microsoft sequência Clustering Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
3.  Examine a lista de características do cluster até localizar a primeira linha de transição.  
  
4.  Uma linha de transição contém o texto transição na **variáveis** coluna e uma combinação de valores de atributo sequencial a **valor** coluna. A sequência também pode conter pontos iniciais e valores ausentes.  
  
     Por exemplo, suponha que a transição tenha o valor [Iniciar] -> Tubo de Pneu de Estrada. Isso significa que clientes deste cluster colocam com frequência o Tubo de Pneu de Estrada em sua cesta de compras. Isso poderia significar que o produto é um item popular e procurado primeiro por clientes, ou pode simplesmente indicar que o produto é fácil de localizar no site de compras.  
  
5.  Percorra a lista até encontrar a primeira transição que não tem **[Iniciar]** ou **ausente** nele.  
  
     Por exemplo, suponha que você localizou a transição **pneu de passeio, tubo de pneu de passeio**. Isso significa que clientes deste cluster com frequência compraram esses itens juntos, exatamente nessa ordem.  
  
6.  Coloque o mouse sobre a barra sombreada para essa transição.  
  
     A probabilidade dessa transição é exibida como uma porcentagem.  
  
7.  No **Cluster** lista suspensa, selecione **população (tudo)**.  
  
     A lista de atributos é atualizada para mostrar as características de todas as ordens usadas na criação do modelo. Nesse modelo de mineração, é a característica mais importante para fazer a distinção entre clusters `Region`, com um valor de **América do Norte**.  
  
 Depois de revisar essas tarefas, você percebe duas coisas. A primeira é que precisa de muitos dados para obter um número significativo de combinações. Por exemplo, as sequências com as maiores probabilidades são propensos a incluir uma **[Iniciar]** ou **ausente** estado.  
  
 A segunda é que há um grande efeito de clustering em atributos para `Region`, que torna mais difícil ver os grupos de sequências. Dessa forma, você decide criar outro modelo que use somente sequências e que não inclua as colunas para região ou renda.  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a> Guia discriminação de cluster  
 O **discriminação do Cluster** guia o ajuda a comparar dois clusters, para determinar quais atributos distinguem um cluster específico de outro cluster. A guia contém quatro colunas: **Variáveis**, **valores**, **Cluster 1**, e **Cluster 2**.  Você pode escolher qualquer cluster para usar como **Cluster 1** e **Cluster 2**.  
  
 O **variáveis** coluna indica o nome do atributo, que pode ser um nome de coluna ou combinação de nome de coluna e a palavra **transição**. O **valores** coluna mostra o valor exato do atributo ou transição. As barras sombreadas nas colunas **Cluster 1** e **Cluster 2** indicam a força do atributo nos clusters que estão sendo comparados. Quanto mais longa for a barra, mais será provável que o cluster inclua casos com esse atributo.  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>Para comparar dois clusters usando a guia Distinção de Cluster  
  
1.  No **discriminação do Cluster** guia, para **Cluster 1**, selecione `Pacific Cluster`.  
  
     Por padrão, a seleção para **Cluster 2** alterações **complemento do Cluster do Pacífico**.  
  
     O principal atributo que distingue `Pacific Cluster` de todos os outros casos é a região. A região é um atributo tão forte para o clustering que obscurece outros atributos. Para impedir esse efeito, tente comparar vários clusters menores uns aos outros. Quando você fizer isso, a lista de atributos mudará e poderá incluir mais transições entre modelos.  
  
2.  Localize uma linha de transição e coloque o mouse sobre a barra sombreada.  
  
     Os itens a **valores** coluna pode incluir estados e transições. O sombreamento de cada item indica a contagem de distinção. Para saber mais sobre o significado de pontuações diferentes, consulte [Mining Model Content para modelos de Clustering de sequência de &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a> Guia transições de estado  
 Sobre o **transições de estado** guia, você pode selecionar um cluster e percorra as transições de estado. Se você selecionar **população (tudo)** na lista suspensa do cluster, o diagrama mostra a distribuição de estados para o modelo de mineração inteira.  
  
 Cada nó do gráfico representa um estado, ou um valor possível das sequências que você está tentando analisar. A cor de fundo dos nós representa a frequência do estado. As linhas conectam alguns estados, indicando uma transição entre eles. Você pode mover o controle deslizante para cima ou para baixo para alterar o limite de probabilidade para as transições. Os números são associados a alguns nós, indicando a probabilidade do estado.  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>Para explorar os relacionamentos na guia Transição de Estado  
  
1.  No **transições de estado** guia do Visualizador de modelo de mineração, selecione `Pacific Cluster` na lista de clusters. Certifique-se de que o **Mostrar rótulos de borda** opção está selecionada.  
  
     O gráfico é atualizado para mostrar as transições mais comuns desse cluster.  
  
2.  Clique em qualquer nó conectado por uma linha a outro nó.  
  
     O gráfico é atualizado e realça os nós relacionados. O valor numérico ao lado da linha indica a probabilidade da transição.  
  
3.  Suba o controle deslizante até **todos os Links**, para aumentar o número de transições incluídas no gráfico.  
  
4.  Selecione **população (tudo)** partir **Cluster**.  
  
     Observe que quando você carrega um cluster diferente, o gráfico volta a ter as configurações de exibição padrão e, portanto, o controle deslizante é redefinido para a posição intermediária.  
  
5.  Clique no nó mais escuro no gráfico, que deve ser **Sport-100**.  
  
     Observe que não há linhas conectando esse produto a outros.  
  
6.  Suba o controle deslizante uma etapa para aumentar o número de transições incluídas no gráfico. Não vá até **todos os Links** ainda.  
  
     O gráfico será atualizado pela adição de várias outras transições, mas nenhuma que inclua o modelo Sport-100.  
  
7.  Mova o controle deslizante até **todos os Links**. Clique no nó Sport-100 caso ele ainda não esteja selecionado.  
  
     O gráfico é atualizado para mostrar muitas transições que incluem o produto Sport-100. A direção da seta na linha de conexão mostra se o item Sport-100 foi selecionado como o primeiro ou o segundo item do par.  
  
8.  Clique no nó de Pneu de Passeio e mova o controle deslizante de volta à posição intermediária.  
  
     A princípio, existem muitas linhas de transição conectando Pneu de Passeio a outros produtos, mas quando você sobe o limite de probabilidade, as transições menos prováveis são eliminadas do gráfico, deixando somente a transição Pneu de Passeio > Tubo de Pneu de Passeio. Essa transição significa que se um cliente colocar um Pneu de Passeio na cesta de compras, há uma grande probabilidade de que o cliente colocará em seguida um Tubo de Pneu de Passeio na cesta.  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a> Visualizador de árvore de conteúdo genérica  
 Esse visualizador pode ser usado em todos os modelos, independentemente do algoritmo ou do tipo de modelo. O **Visualizador de árvore de conteúdo MicrosoftGeneric** está disponível a partir o **visualizador** lista suspensa.  
  
 Uma árvore de conteúdo é uma representação de qualquer modelo de mineração como uma série de nós, em que cada nó representa conhecimento adquirido sobre alguns dados de treinamento. O nó pode conter um padrão, um conjunto de regras, um cluster ou a definição de um intervalo de datas que compartilham alguns atributos. O conteúdo exato do nó difere dependendo do algoritmo e do tipo do atributo previsível; no entanto, a representação geral do conteúdo é a mesma.  
  
 É possível expandir os nós para consultar um maior número de detalhes, assim como copiar o conteúdo de qualquer um deles para a Área de Transferência. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>Para exibir detalhes de um modelo de clustering de sequências usando o Visualizador de Árvore de Conteúdo Genérica  
  
1.  No **Visualizador do modelo de mineração** , clique no **visualizador** relacionar e selecionar **Visualizador de árvore de conteúdo genérica Microsoft**.  
  
2.  No **legenda de nó** painel, clique em `Pacific Cluster (1)`.  
  
     O nome desse nó contém o nome amigável atribuído ao cluster e a ID do nó subjacente. Você pode usar as IDs do nó para detalhar ainda mais o modelo.  
  
3.  Expanda o primeiro nó filho, denominado **nível de sequência para cluster 1**.  
  
     O nó de nível de sequência para um cluster contém detalhes sobre os estados e transições incluídos naquele cluster. Você pode usar esses detalhes, disponíveis na coluna NODE_DISTRIBUTION, para explorar as sequências e os estados de cada cluster ou do modelo como um todo.  
  
4.  Continue a expandir nós e a exibir detalhes no painel visualizador de HTML.  
  
 Para obter mais informações sobre o conteúdo do modelo de mineração e como usar os detalhes no visualizador, consulte [conteúdo do modelo de mineração para modelos de Clustering de sequência de &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Voltar ao Início](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando um modelo de Clustering de sequências relacionado &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Sequence Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Exemplos de consulta de modelo de clustering em sequência](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
