---
title: Navegação de uma associação de modelo de regras | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 1259cc627ef53d8f5a201e42772a9dba390824cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664385"
---
# <a name="browsing-an-association-rules-model"></a>Procurando um modelo de regras de associação
  Quando você abre um modelo de associação usando **navegue**, o modelo é exibido em um visualizador interativo, semelhante ao Visualizador de regras de associação no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  O visualizador permite observar rapidamente quais itens foram correlacionados entre si e exibir as regras que você pode usar para previsão ou fazer recomendações.  
  
##  <a name="BKMK_ViewerTabs"></a> Explorar o modelo  
 Quando você abre um modelo de mineração foi criado usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de regras de associação, o **procurar** janela inclui as seguintes exibições, cada um projetado para permitir explorar um aspecto diferente do modelo:  
  
-   [Conjuntos de Itens](#BKMK_Itemsets)  
  
-   [Regras](#BKMK_Rules)  
  
-   [Rede de Dependência](#BKMK_Dependency)  
  
 Tome nota da opção em cada guia **Mostrar nome longo** . Ao selecionar esta opção, você poderá mostrar ou ocultar a tabela da qual o conjunto de itens se origina e reduzir ou alongar o nome da regra ou do conjunto de itens. Essa opção é particularmente útil quando os dados de caso e de atributo vêm de fontes de dados diferentes.  
  
 Para fazer experiências com um modelo de associação, você pode usar os dados de exemplo na guia Associar da pasta de trabalho de dados de exemplo e criar um modelo de associação usando todos os padrões. Você também pode criar um modelo de análise da cesta de compras e abri-lo usando **procurar**.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de Itens  
 O **conjuntos de itens** guia é um bom lugar para começar a explorar um modelo de associação. Essa guia mostra uma lista de itens que o modelo frequentemente encontra juntos.  
  
 ![Lista de itens em um modelo de associação](media/dm13-association-itemsets.gif "lista de itens em um modelo de associação")  
  
 O exemplo mais comum de conjuntos de itens é um modelo de cesta de compras, onde um conjunto de itens representa pares ou conjuntos de produtos que muitos clientes compram ao mesmo tempo. No entanto, dependendo de como você agrupa e pede seus itens, o conjunto de itens pode conter uma sequência de filmes que os clientes pedem durante um período de tempo ou eventos que tendem a ocorrer em um local específico.  
  
 Uma *conjunto de itens* pode conter apenas um item para duas, três, ou, no entanto, muitos são definidos como o tamanho máximo do conjunto de itens para o modelo. Para cada conjunto de itens, o visualizador exibe o conjunto de itens *suportam*, *probabilidade*, e *tamanho*. O suporte e a probabilidade são as estatísticas principais usadas para classificar os conjuntos de itens e as regras geradas por um modelo de associação. Esses valores também são usados para calcular e descrever a importância.  
  
 **Suporte**. O suporte significa o número de casos ou linhas de dados de entrada que têm esse item. Por exemplo, se um conjunto de itens contiver dois itens que são encontrados em compras carrinho de compras, o número das **suporte** coluna indica quantas vezes essa combinação de itens ocorreu nos dados de origem.  
  
 **Tamanho**. Ao alterar o tamanho do conjunto de itens, você poderá controlar o comprimento das listas de conjuntos de itens. Se você não quiser ver produtos únicos na lista, altere a opção **tamanho mínimo do conjunto de itens**para 2 ou mais.  Restringir a lista aumentando o tamanho mínimo de conjuntos de itens lhe permite procurar padrões mais específicos. Talvez isso seja útil se você estiver trabalhando com um conjunto de dados muito grande.  
  
 Você pode filtrar o número de conjuntos de itens que são exibidos na guia alterando os **suporte mínimo** e **máximo de linhas** valores. Se você aumentar o **suporte mínimo** valor, a lista mostrará menos conjuntos de itens, mas os conjuntos de itens serão os mais comuns nos dados de entrada. Se comum é o mesmo que importante é outra pergunta, que você pode explorar usando o **regras** guia.  
  
 Observe que alterar o valor de suporte ou outros controles sobre o **conjuntos de itens** altera somente os itens que são exibidos e não afetam o modelo subjacente. Se você quiser gerar menos ou mais conjuntos de itens ou limitar o tamanho, você deve usar os parâmetros `MINIMUM_SUPPORT` e `MAXIMUM_SUPPORT`, disponível para o **parâmetros de algoritmo** caixa de diálogo.  
  
##### <a name="explore-the-itemsets-list"></a>Explorar a lista de conjuntos de itens  
  
1.  Clique o **suporte** coluna para classificar pelo suporte mais alto ao mais baixo. Isso lhe dará uma ideia do que os clientes estão comprando com mais frequência.  
  
2.  Para se concentrar em um determinado conjunto de itens de interesse, das mil combinações possíveis, digite algum texto na **filtrar conjunto de itens** caixa.  
  
     Aqui nós digitamos `Gloves`. Quando você aplica o filtro, a lista será atualizada para mostrar somente os conjuntos de itens que contêm luvas. Isso permite que você se concentre nas transações em que os clientes compraram luvas e algum outro item.  
  
     A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
3.  Altere o valor de **tamanho mínimo do conjunto de itens** para filtrar os clientes que compraram somente luvas e nenhum outro item.  
  
4.  Clique na lista suspensa para a opção **Mostrar**, para controlar como os atributos são exibidos:  
  
    -   **Mostrar o nome e valor de atributo**  
  
    -   **Mostrar apenas o valor de atributo**  
  
    -   **Mostrar apenas o nome do atributo**  
  
     Observe como o nome é alterado. No caso de um modelo de cesta de compras, que é criado em tabelas aninhadas dos produtos comprados por vários clientes, o nome do atributo é normalmente o nome do produto, e a presença do produto na lista é marcada como `Existing`, o que significa que o cliente comprou o item.  
  
     O oposto de `Existing` é `Missing`, que pode ser um atributo muito útil para investigar na mineração de dados. Por exemplo, suponha que o conjunto de itens A + B seja tão popular que você queira encontrar clientes que compraram o Item, mas não o B. Você poderia fazer isso usando uma consulta de previsão e recuperando as transações com um, mas não o outro e fazer uma análise detalhada sobre aqueles. Para obter informações sobre como criar consultas de previsão em modelos de associação, consulte [exemplos de consulta de modelo de associação](data-mining/association-model-query-examples.md) nos Manuais Online do SQL Server  
  
5.  Para forçar a lista de conjuntos de itens a ser exibida novamente usando novos critérios de filtro, você pode marcar ou desmarcar os **Mostrar nome longo** caixa de seleção.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Regras  
 O **regras** guia combina informações sobre os conjuntos de itens e seu valor relativo.  
  
 ![Lista de regras criadas por um modelo de associação](media/dm13-association-rules.gif "lista de regras criadas por um modelo de associação")  
  
 *Probabilidade* representa a fração de casos no conjunto de dados que contém a combinação de itens de destino. Probabilidade é semelhante ao conceito estatístico de *confiança*e lhe dá uma indicação de como o resultado de uma regra deve ocorrer. Você pode alterar o valor de **probabilidade mínima** neste painel para filtrar as regras que são exibidas.  
  
 O valor para **probabilidade mínima** que você vê é inicialmente o valor de limite que foi usado pelo algoritmo ao criar o modelo. Depois que o modelo for concluído, você não poderá diminuir esse valor, mas você pode aumentá-lo para mostrar apenas os itens de probabilidade mais alta.  
  
 *Importância* foi projetada para medir a utilidade de uma regra. Uma regra que é muito comum pode ser tão óbvia e constante que tenha pouco valor informativo. Quanto maior a importância, mais valiosa será a regra para prever o resultado. No [análise da cesta de compras &#40;ferramentas de análise de tabela para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) ferramenta, importância pode ser combinada com o preço de itens para determinar os pacotes que são potencialmente mais úteis em termos de vendas.  
  
##### <a name="explore-the-rules-list"></a>Explorar a lista de regras  
  
1.  Experimente clicando na coluna títulos - **probabilidade**, **importância**, e **regra** – para ver como os dados são alterados.  
  
2.  Use o **regra de filtro** opção para digitar valores e se concentrar em regras de destino.  
  
     Por exemplo, se você quiser ver todas as regras que preveem quais clientes provavelmente comprarão luvas, digite "luvas" na caixa de texto e atualize o painel.  
  
     A opção **Filtrar Conjunto de Itens** também exibe uma lista dos filtros que você usou anteriormente.  
  
3.  Para forçar a lista de regras a ser exibida novamente usando critérios de filtro, você pode marcar ou desmarcar os **Mostrar nome longo** caixa de seleção.  
  
4.  Use a opção **Mostrar** para controlar a maneira que os nomes das regras são exibidos.  
  
5.  Defina o valor para o **máximo de linhas** opção a 100 e, em seguida, clique em **copiar para Excel**.  
  
     Observe que a alteração desse valor não tem nenhum efeito na quantidade de dados no modelo. ela simplesmente controla o número de linhas na lista de exibição. Essa opção pode ser útil ao trabalhar com modelos muito grandes.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Rede de Dependências  
 O **rede de dependências** guia é um mapa visual das correlações entre itens. Cada oval no gráfico (conhecido como um *nó*) representa um par atributo-valor, tal como "casaco = existente" ou "Idade = 1-30".  Cada linha que conecta os ovais (conhecido como um *edge*) representa um tipo de correlação.  
  
 ![Gráfico de rede de dependência para um modelo de associação](media/dm13-association-dependencynetwork.gif "grafo de rede de dependência para um modelo de associação")  
  
##### <a name="explore-the-dependency-network"></a>Explorar a rede de dependências  
  
1.  Clique o **encontrar** botão e usar o **localizar nó** caixa de diálogo para digitar um item de interesse.  
  
     Por exemplo, digite "luvas" e maximize o gráfico na janela para que você possa ver facilmente os resultados.  
  
     O nó que contém o item será realçado, enquanto que as setas apontarão para o nó que representa uma regra que conecta os itens.  
  
     A direção da seta indica a direção da regra. Por exemplo, se alguém que comprar luvas provavelmente também comprar um casaco, na seta para iniciar a partir do nó "luva" e encerrar no nó "casaco".  
  
     Para obter estatísticas adicionais sobre esta regra, você pode clicar na **regras** guia e procure por uma regra com a descrição, "Luva - existente" -> "Casaco – existente.")  
  
2.  Clique e arraste o controle deslizante à esquerda do visualizador.  
  
     O controle deslizante funciona como um filtro na probabilidade das regras. Diminuindo o controle deslizante, somente as regras mais fortes serão exibidas.  
  
3.  Clique em **copiar para Excel** para copiar um instantâneo da janela atual para o Excel.  
  
     Você não poderá trabalhar com o gráfico que você copiou para o Excel; Se você precisar de um gráfico de rede interativo, use o [exibindo modelos de mineração de dados no Visio &#40;Data Mining Add-ins&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Mais informações sobre modelos de associação  
 Você pode usar o **procurar** recurso para abrir e explorar qualquer modelo que foi criado usando o algoritmo regras de associação da Microsoft. Isso inclui modelos criados usando o [análise da cesta de compras &#40;ferramentas de análise de tabela para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) ferramenta, o **ferramentas de análise de tabela** faixa de opções, ou no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Se você criar um modelo de regras de associação usando a ferramenta Análise de Cesta de Compras, muitas das opções avançadas serão configuradas automaticamente para você.  
  
 Se você quiser definir parâmetros avançados ou alterar a probabilidade mínima e suporte, use o [Assistente de associação de &#40;cliente de mineração de dados para Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) assistente, ou criar seu próprio modelo usando o [Adicionar modelo à Estrutura &#40;Data Mining Add-ins para Excel&#41; ](add-model-to-structure-data-mining-add-ins-for-excel.md) opção de modelagem.  
  
-   **Conjuntos de itens:** Quando você cria o modelo, você também pode controlar o número de conjuntos de itens gerados atribuindo um valor ao parâmetro MINIMUM_PROBABILITY. Esse parâmetro está disponível na caixa de diálogo Parâmetros do algoritmo.  
  
-   **Regras:** O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo regras de associação usa valores de probabilidade para restringir o número de regras que são gerados. Você pode controlar o número de regras definindo os parâmetros `MINIMUM_PROBABILITY` ou `MINIMUM _IMPORTANCE`.  
  
 Para obter mais informações sobre como configurar parâmetros avançados, consulte [algoritmos de mineração de dados &#40;SQL Server Data Mining Add-ins&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
