---
title: Navegando em um modelo de regras de associação | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ff9705949be3fb9bf99d985d0db1aa17d93ab1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088465"
---
# <a name="browsing-an-association-rules-model"></a>Procurando um modelo de regras de associação
  Quando você abre um modelo de associação usando **procurar**, o modelo é exibido em um visualizador interativo, semelhante ao Visualizador de regras de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]associação no.  O visualizador permite observar rapidamente quais itens foram correlacionados entre si e exibir as regras que você pode usar para previsão ou fazer recomendações.  
  
##  <a name="BKMK_ViewerTabs"></a>Explorar o modelo  
 Quando você abre um modelo de mineração criado usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo regras de associação, a janela **procurar** inclui as seguintes exibições, cada uma projetada para permitir que você explore um aspecto diferente do modelo:  
  
-   [Conjuntos](#BKMK_Itemsets)  
  
-   [Regras](#BKMK_Rules)  
  
-   [Rede de dependências](#BKMK_Dependency)  
  
 Anote a opção em cada guia, **Mostrar nome longo** . Ao selecionar esta opção, você poderá mostrar ou ocultar a tabela da qual o conjunto de itens se origina e reduzir ou alongar o nome da regra ou do conjunto de itens. Essa opção é particularmente útil quando os dados de caso e de atributo vêm de fontes de dados diferentes.  
  
 Para fazer experiências com um modelo de associação, você pode usar os dados de exemplo na guia Associar da pasta de trabalho de dados de exemplo e criar um modelo de associação usando todos os padrões. Você também pode criar um modelo de análise de cesta de compras e abri-lo usando **procurar**.  
  
###  <a name="BKMK_Itemsets"></a>Conjuntos  
 A guia **conjuntos** de itens é um bom lugar para começar a explorar um modelo de associação. Essa guia mostra uma lista de itens que o modelo frequentemente encontra juntos.  
  
 ![Lista de itens em um modelo de associação](media/dm13-association-itemsets.gif "Lista de itens em um modelo de associação")  
  
 O exemplo mais comum de conjuntos de itens é um modelo de cesta de compras, onde um conjunto de itens representa pares ou conjuntos de produtos que muitos clientes compram ao mesmo tempo. No entanto, dependendo de como você agrupa e pede seus itens, o conjunto de itens pode conter uma sequência de filmes que os clientes pedem durante um período de tempo ou eventos que tendem a ocorrer em um local específico.  
  
 Um *conjunto* pode conter apenas um item para dois, três ou, no entanto, muitos é definido como o tamanho máximo de conjunto para o modelo. Para cada conjunto, o visualizador exibe o *suporte*, a *probabilidade*e o *tamanho*do conjunto. O suporte e a probabilidade são as estatísticas principais usadas para classificar os conjuntos de itens e as regras geradas por um modelo de associação. Esses valores também são usados para calcular e descrever a importância.  
  
 **Suporte**. O suporte significa o número de casos ou linhas de dados de entrada que têm esse item. Por exemplo, se um conjunto contiver dois itens que são encontrados em um carrinho de compras, o número na coluna de **suporte** indica quantas vezes a combinação de itens ocorreu nos dados de origem.  
  
 **Tamanho**. Ao alterar o tamanho do conjunto de itens, você poderá controlar o comprimento das listas de conjuntos de itens. Se você não quiser ver produtos únicos na lista, altere a opção, **tamanho mínimo de conjunto**, para 2 ou mais.  Restringir a lista aumentando o tamanho mínimo de conjuntos de itens lhe permite procurar padrões mais específicos. Talvez isso seja útil se você estiver trabalhando com um conjunto de dados muito grande.  
  
 Você pode filtrar o número de conjuntos de itens que são exibidos na guia alterando os valores **mínimos de suporte** e **máximo de linhas** . Se você aumentar o valor **mínimo de suporte** , a lista mostrará menos conjuntos de itens, mas os conjuntos de itens serão os mais comuns nos dados de entrada. Se Common é o mesmo que importante é outra pergunta, que você pode explorar usando a guia **regras** .  
  
 Observe que alterar o valor de suporte ou outros controles na guia **conjuntos** de itens altera apenas os itens que são exibidos e não afeta o modelo subjacente. Se você quiser gerar menos ou mais conjuntos de itens, ou limitar seu tamanho, deverá usar os parâmetros `MINIMUM_SUPPORT` e `MAXIMUM_SUPPORT`, disponível na caixa de diálogo **parâmetros de algoritmo** .  
  
##### <a name="explore-the-itemsets-list"></a>Explorar a lista de conjuntos de itens  
  
1.  Clique na coluna **suporte** para classificar de acordo com o suporte mais alto ao mais baixo. Isso lhe dará uma ideia do que os clientes estão comprando com mais frequência.  
  
2.  Para se concentrar em um determinado conjunto de interesse, fora das combinações de muitos milhares possíveis, digite algum texto na caixa **Filtrar conjunto** .  
  
     Aqui, digitamos `Gloves`. Quando você aplica o filtro, a lista será atualizada para mostrar somente os conjuntos de itens que contêm luvas. Isso permite que você se concentre nas transações em que os clientes compraram luvas e algum outro item.  
  
     A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
3.  Altere o valor de **tamanho mínimo do conjunto** para filtrar os clientes que compraram apenas luvas e nenhum outro item.  
  
4.  Clique na lista suspensa da opção **Mostrar**para controlar como os atributos são exibidos:  
  
    -   **Mostrar nome e valor do atributo**  
  
    -   **Mostrar somente o valor do atributo**  
  
    -   **Mostrar apenas o nome do atributo**  
  
     Observe como o nome é alterado. No caso de um modelo de cesta de compras, que é criado em tabelas aninhadas dos produtos comprados por vários clientes, o nome do atributo é normalmente o nome do produto, e a presença do produto na lista é marcada como `Existing`, o que significa que o cliente comprou o item.  
  
     O oposto de `Existing` é `Missing`, que pode ser um atributo muito útil para investigar na mineração de dados. Por exemplo, suponha que o conjunto a + B seja tão popular que você queria encontrar clientes que compraram o item A, mas não o item B. Você pode fazer isso usando uma consulta de previsão e recuperando as transações com uma, mas não a outra, e fazer mais análises sobre elas. Para obter informações sobre como criar consultas de previsão em modelos de associação, consulte [exemplos de consulta de modelo de associação](data-mining/association-model-query-examples.md) no manuais online do SQL Server  
  
5.  Para forçar a lista de conjuntos de itens a exibir novamente usando seus novos critérios de filtro, você pode marcar ou desmarcar a caixa de seleção **Mostrar nome longo** .  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a>Regras  
 A guia **regras** combina informações sobre os conjuntos de itens e seu valor relativo.  
  
 ![Lista de regras criadas por um modelo de associação](media/dm13-association-rules.gif "Lista de regras criadas por um modelo de associação")  
  
 *Probabilidade* representa a fração de casos no conjunto de um que contém a combinação de itens de destino. A probabilidade é semelhante ao conceito estatístico de *confiança*e dá a você uma indicação de como é provável que o resultado de uma regra ocorra. Você pode alterar o valor de **probabilidade mínima** nesse painel para filtrar as regras que são exibidas.  
  
 O valor da **probabilidade mínima** que você vê inicialmente é o valor de limite que foi usado pelo algoritmo ao criar o modelo. Depois que o modelo for concluído, você não poderá diminuir esse valor, mas poderá aumentá-lo para mostrar apenas os itens de probabilidade mais alta.  
  
 A *importância* é projetada para medir a utilidade de uma regra. Uma regra que é muito comum pode ser tão óbvia e constante que tenha pouco valor informativo. Quanto maior a importância, mais valiosa será a regra para prever o resultado. Na [análise da cesta de compras &#40;tabela AnalysisTools para a ferramenta de&#41;do Excel](shopping-basket-analysis-table-analysistools-for-excel.md) , a importância pode ser combinada com o preço dos itens para determinar os grupos que são potencialmente mais valiosos em termos de vendas.  
  
##### <a name="explore-the-rules-list"></a>Explorar a lista de regras  
  
1.  Tente clicar nos títulos de coluna- **probabilidade**, **importância**e **regra** -para ver como os dados são alterados.  
  
2.  Use a opção **Filtrar regra** para digitar valores e se concentrar nas regras de destino.  
  
     Por exemplo, se você quiser ver todas as regras que preveem o que os clientes provavelmente comprarão juntamente com o luvas, digite "luvas" na caixa de texto e atualize o painel.  
  
     A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
3.  Para forçar a exibição da lista de regras usando critérios de filtro, você pode marcar ou desmarcar a caixa de seleção **Mostrar nome longo** .  
  
4.  Use a opção, **Mostrar** para controlar a maneira como os nomes de regra são exibidos.  
  
5.  Defina o valor para a opção **máximo de linhas** como 100 e clique em **copiar para o Excel**.  
  
     Observe que a alteração desse valor não tem nenhum efeito na quantidade de dados no modelo; Ele simplesmente controla o número de linhas na lista de exibição. Essa opção pode ser útil ao trabalhar com modelos muito grandes.  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a>Rede de dependências  
 A guia **rede de dependências** é um mapa visual das correlações entre os itens. Cada oval no grafo (chamada de *nó*) representa um par atributo-valor, como "comparações = existente" ou "idade = 1-30".  Cada linha conectando as ovais (chamadas de *borda*) representa um tipo de correlação.  
  
 ![Gráfico da rede de dependências para um modelo de associação](media/dm13-association-dependencynetwork.gif "Gráfico da rede de dependências para um modelo de associação")  
  
##### <a name="explore-the-dependency-network"></a>Explorar a rede de dependências  
  
1.  Clique no botão **Localizar** e use a caixa de diálogo **Localizar nó** para digitar um item de interesse.  
  
     Por exemplo, digite "luvas" e, em seguida, maximize o grafo na janela para que você possa ver facilmente os resultados.  
  
     O nó que contém o item será realçado, enquanto que as setas apontarão para o nó que representa uma regra que conecta os itens.  
  
     A direção da seta indica a direção da regra. Por exemplo, se alguém que adquire o luvas também tiver probabilidade de comprar um benefício, a seta será iniciada no nó "diferenciada" e terminará no nó "benefício".  
  
     Para obter estatísticas adicionais sobre essa regra, você pode clicar na guia **regras** e procurar uma regra com a descrição "diferenciada-existing"-> "comparecentes-existentes.")  
  
2.  Clique e arraste o controle deslizante à esquerda do visualizador.  
  
     O controle deslizante funciona como um filtro na probabilidade das regras. Diminuindo o controle deslizante, somente as regras mais fortes serão exibidas.  
  
3.  Clique em **copiar para o Excel** para copiar um instantâneo da janela atual para o Excel.  
  
     Você não conseguirá trabalhar com o grafo copiado no Excel; Se você precisar de um gráfico de rede interativo, use os suplementos de mineração de [dados de exibição no Visio &#40;&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Voltar ao início](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Mais sobre modelos de associação  
 Você pode usar o recurso **procurar** para abrir e explorar qualquer modelo criado usando o algoritmo regras de associação da Microsoft. Isso inclui modelos criados usando a [análise de cesta de compras &#40;tabela AnalysisTools para a ferramenta de&#41;do Excel](shopping-basket-analysis-table-analysistools-for-excel.md) , na faixa de ferramentas [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]de análise de **tabela** ou no.  
  
 Se você criar um modelo de regras de associação usando a ferramenta Análise de Cesta de Compras, muitas das opções avançadas serão configuradas automaticamente para você.  
  
 Se você quiser definir parâmetros avançados ou alterar a probabilidade e o suporte mínimos, use o assistente para [associar o &#40;cliente de mineração de dados para excel&#41;](associate-wizard-data-mining-client-for-excel.md) ou crie seu próprio modelo usando a opção [Adicionar modelo à estrutura &#40;suplementos de mineração de dados para Excel&#41;de](add-model-to-structure-data-mining-add-ins-for-excel.md) modelagem.  
  
-   **Conjuntos** de itens: Ao criar o modelo, você também pode controlar o número de conjuntos de itens que são gerados atribuindo um valor ao parâmetro MINIMUM_PROBABILITY. Este parâmetro está disponível na caixa de diálogo Parâmetros do Algoritmo.  
  
-   **Regras:** O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo regras de associação usa valores de probabilidade para restringir o número de regras que são geradas. Você pode controlar o número de regras definindo os parâmetros `MINIMUM_PROBABILITY` ou `MINIMUM _IMPORTANCE`.  
  
 Para obter mais informações sobre como configurar parâmetros avançados, consulte [algoritmos de mineração de dados &#40;SQL Server suplementos de mineração de dados&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisando modelos no Excel &#40;SQL Server suplementos de mineração de dados&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
