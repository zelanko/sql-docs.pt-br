---
title: Mining Model Content para modelos de Clustering de sequências (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining model content, sequence clustering models
- sequence clustering algorithms [Analysis Services]
ms.assetid: 68e1934a-e147-4d53-b122-fa15e3fd5485
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0b505e01e6b8334ed1a0baeaacbda7e29ba7407
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208146"
---
# <a name="mining-model-content-for-sequence-clustering-models-analysis-services---data-mining"></a>Conteúdo do modelo de mineração para modelos de clustering de sequências (Analysis Services – Mineração de Dados)
  Este tópico descreve o conteúdo do modelo de mineração que é específico para modelos que usam o algoritmo MSC (Microsoft Sequence Clustering). Para obter uma explicação sobre a terminologia geral e estatística relacionada ao conteúdo do modelo de mineração que se aplica a todos os tipos de modelo, consulte [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-sequence-clustering-model"></a>Entendendo a estrutura de um modelo de clustering de sequência  
 Um modelo de clustering de sequência tem um único nó pai (NODE_TYPE = 1) que representa o modelo e seus metadados. O nó pai, que recebe o rótulo **(All)**, tem um nó de sequência relacionado (NODE_TYPE = 13) que lista todas as dimensões detectadas nos dados de treinamento.  
  
 ![Estrutura do modelo de clustering de sequências](../media/modelcontent-seqclust.gif "estrutura do modelo de clustering de sequências")  
  
 O algoritmo também cria um número de clusters com base nas transições que foram encontradas nos dados e em qualquer outro atributo de entrada incluído ao criar o modelo, como informações demográficas de clientes e assim por diante. Cada cluster (NODE_TYPE = 5) contém seu próprio nó de sequência (NODE_TYPE = 13) que lista apenas as transições que foram usadas ao gerar aquele cluster específico. No nó de sequência, você pode fazer uma busca minuciosa para exibir os detalhes de transições de estado específicas (NODE_TYPE = 14).  
  
 Para obter uma explicação das transições de estado e sequência, com exemplos, consulte [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md).  
  
## <a name="model-content-for-a-sequence-clustering-model"></a>Conteúdo de um modelo de clustering de sequência  
 Esta seção fornece informações adicionais sobre colunas no conteúdo do modelo de mineração que têm relevância específica para clustering de sequência.  
  
 MODEL_CATALOG  
 Nome do banco de dados no qual o modelo é armazenado.  
  
 MODEL_NAME  
 Nome do modelo.  
  
 ATTRIBUTE_NAME  
 Sempre em branco.  
  
 NODE_NAME  
 O nome do nó. Atualmente, o mesmo valor de NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Nome exclusivo do nó.  
  
 NODE_TYPE  
 Um modelo de clustering de sequência gera os seguintes tipos de nó:  
  
|ID do tipo de nó|Description|  
|------------------|-----------------|  
|1 (Modelo)|Nó raiz do modelo.|  
|5 (Cluster)|Contém a contagem de transições no cluster, uma lista dos atributos e estatísticas que descrevem os valores no cluster.|  
|13 (Sequência)|Contém uma lista das transições incluídas no cluster.|  
|14 (Transição)|Descreve uma sequência de eventos, como uma tabela na qual a primeira linha contém o estado inicial e as outras linhas contêm estados sucessivos, juntamente com estatísticas de probabilidade e suporte.|  
  
 NODE_GUID  
 Em branco.  
  
 NODE_CAPTION  
 Um rótulo ou uma legenda associada ao nó para exibição de finalidades.  
  
 É possível renomear as legendas do cluster ao usar o modelo. Entretanto, o novo nome não é mantido ao fechar o modelo.  
  
 CHILDREN_CARDINALITY  
 Uma estimativa do número de filhos do nó.  
  
 **Raiz do modelo** O valor da cardinalidade é igual ao número de clusters, mais um. Para obter mais informações, consulte [Cardinalidade](#bkmk_cardinality).  
  
 **Nós de cluster** A cardinalidade é sempre 1, pois cada cluster tem um único nó filho, que contém a lista de sequências no cluster.  
  
 **Nós de sequência** A cardinalidade indica o número de transições que são incluídas naquele cluster. Por exemplo, a cardinalidade do nó de sequência para a raiz do modelo indica quantas transições foram encontradas em todo o modelo.  
  
 PARENT_UNIQUE_NAME  
 O nome exclusivo do nó pai.  
  
 NULL é retornado para todos os nós em nível raiz.  
  
 NODE_DESCRIPTION  
 Mesmo que a legenda do nó.  
  
 NODE_RULE  
 Sempre em branco.  
  
 MARGINAL_RULE  
 Sempre em branco.  
  
 NODE_PROBABILITY  
 **Raiz do modelo** Sempre 0.  
  
 **Nós de cluster** A probabilidade ajustada do cluster no modelo. As probabilidades ajustadas não são somadas a 1, pois o método de clustering usado no clustering de sequência permite relação parcial em diversos clusters.  
  
 **Nós de sequência** Sempre 0.  
  
 **Nós de transição** Sempre 0.  
  
 MARGINAL_PROBABILITY  
 **Raiz do modelo** Sempre 0.  
  
 **Nós de cluster** O mesmo valor de NODE_PROBABILITY.  
  
 **Nós de sequência** Sempre 0.  
  
 **Nós de transição** Sempre 0.  
  
 NODE_DISTRIBUTION  
 Uma tabela que contém probabilidades e outras informações. Para obter mais informações, consulte a [tabela NODE_DISTRIBUTION](#bkmk_NODEDIST).  
  
 NODE_SUPPORT  
 O número de transições que aceitam esse nó. Com isso, se houver 30 exemplos de sequência "Produto A seguido pelo Produto B" nos dados de treinamento, o total será 30.  
  
 **Raiz do modelo** Número total de transições no modelo.  
  
 **Nós de cluster** Suporte bruto para o cluster, o que indica o número de casos de treinamento que contribuíram com casos para esse cluster.  
  
 **Nós de sequência** Sempre 0.  
  
 **Nós de transição** A porcentagem de casos no cluster que representa uma transição específica. Pode ser 0 ou pode ter um valor positivo. Calculado a obter o suporte bruto para o nó do cluster e multiplicá-lo pela probabilidade do cluster.  
  
 No caso desse valor, você pode saber quantos casos de treinamento contribuíram com a transição.  
  
 MSOLAP_MODEL_COLUMN  
 Não aplicável.  
  
 MSOLAP_NODE_SCORE  
 Não aplicável.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 O mesmo que NODE_DESCRIPTION.  
  
## <a name="understanding-sequences-states-and-transitions"></a>Entendendo sequências, estados e transições  
 Um modelo de clustering de sequência tem uma estrutura única que combina dois tipos de objetos com tipos de informações bem distintos: o primeiro é cluster e o segundo, transições de estado.  
  
 Os clusters criados pelo clustering de sequência são como os clusters criados pelo algoritmo Microsoft Clustering. Cada cluster tem um perfil e características. Porém, no clustering de sequência, cada cluster contém também um único nó filho que lista as sequências naquele cluster. Cada nó de sequência contém vários nós filhos que descrevem as transições de estado detalhadamente, com probabilidades.  
  
 Há quase sempre mais sequências no modelo do que você poderia encontrar em um único caso, pois as sequências podem ser encadeadas. O Microsoft Analysis Services armazena ponteiros de um estado para outro de forma que você possa contabilizar o número de vezes que cada transição ocorre. Você também pode localizar informações sobre quantas vezes a sequência ocorreu e medir as probabilidades de ocorrência em relação a todo o conjunto de estados observados.  
  
 A tabela a seguir resume como as informações são armazenadas no modelo e como os nós são relacionados.  
  
|Nó|Tem nó filho|tabela NODE_DISTRIBUTION|  
|----------|--------------------|------------------------------|  
|Raiz do modelo|Vários nós de cluster<br /><br /> Nó com sequências para todo o modelo|Lista todos os produtos no modelo, com suporte e probabilidade.<br /><br /> Como esse método de clustering permite associação parcial em vários clusters, o suporte e a probabilidade podem ter valores fracionários. Ou seja, em vez de contabilizar um único caso uma vez, cada caso pode pertencer potencialmente a vários clusters. Com isso, quando a associação de cluster final é determinada, o valor é ajustado pela probabilidade daquele cluster.|  
|Nó de sequência para modelo|Vários nós de transição|Lista todos os produtos no modelo, com suporte e probabilidade.<br /><br /> Como o número de sequências para o modelo já é conhecido, os cálculos para suporte e probabilidade são diretos:<br /><br /> Suporte = contagem de casos<br /><br /> Probabilidade = probabilidade bruta de cada sequência no modelo. Todas as probabilidades devem ser somadas a 1.|  
|Nós de cluster individuais|Nó com sequências apenas para aquele cluster|Lista todos os produtos em um cluster, mas fornece valores de suporte e probabilidade apenas para os produtos que são característicos do cluster.<br /><br /> O suporte representa o valor de suporte ajustado para cada caso neste cluster. Os valores de probabilidade são a probabilidade ajustada.|  
|Nós de sequência para clusters individuais|Vários nós com transições para sequências apenas naquele cluster|Exatamente a mesma informação de nós de cluster individuais.|  
|Transições|Nenhum filho|Lista transições para o primeiro estado relacionado.<br /><br /> O suporte é um valor de suporte ajustado que indica os casos que fazem parte de cada transição. A probabilidade é a probabilidade ajustada, representada como uma porcentagem.|  
  
###  <a name="bkmk_NODEDIST"></a> tabela NODE_DISTRIBUTION  
 A tabela NODE_DISTRIBUTION fornece informações detalhadas de suporte e probabilidade para transições e sequências de um cluster específico.  
  
 Uma linha sempre é adicionada à tabela de transição para representar possíveis valores `Missing`. Para obter informações sobre o que o `Missing` valor significa e como ele afeta os cálculos, consulte [valores ausentes &#40;Analysis Services - mineração de dados&#41;](missing-values-analysis-services-data-mining.md).  
  
 Os cálculos para suporte e probabilidade diferem de acordo com os cálculos aplicados aos casos de treinamento ou de acordo com o modelo finalizado. Isso porque o método de clustering padrão, Maximização da Expectativa (ME), pressupõe que qualquer caso pode pertencer a mais de um cluster. Ao calcular suporte para os casos no modelo, é possível usar contas e probabilidades brutas. Entretanto, as probabilidades de qualquer sequência específica em um cluster devem ser ponderadas pela soma de todas as sequências possíveis e combinações de cluster.  
  
###  <a name="bkmk_cardinality"></a> Cardinalidade  
 Em um modelo de clustering, a cardinalidade de um nó pai geralmente indica quantos clusters há no modelo. Entretanto, um modelo de clustering de sequência tem dois tipos de nós no nível de cluster: um tipo de nó contém clusters e o outro tipo de nó contém uma lista de sequências para o modelo.  
  
 Sendo assim, para saber o número de clusters no modelo, você pode pegar o valor de NODE_CARDINALITY do nó (All) e subtrair um. Por exemplo, se o modelo criou 9 clusters, a cardinalidade da raiz do modelo será 10. Isso porque o modelo contém 9 nós do cluster, cada um com seu próprio nó de sequência, mais um nó de sequência adicional rotulado cluster 10, que representa as sequências do modelo.  
  
## <a name="walkthrough-of-structure"></a>Item passo a passo da estrutura  
 Um exemplo pode ajudar a esclarecer como as informações são armazenadas e como você pode interpretá-las. Por exemplo, você pode localizar o maior pedido, o que significa a cadeia mais longa observada nos dados subjacentes do [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] , usando a consulta a seguir:  
  
```  
USE AdventureWorksDW2012  
SELECT DISTINCT OrderNumber, Count(*)  
FROM vAssocSeqLineItems  
GROUP BY OrderNumber  
ORDER BY Count(*) DESC  
```  
  
 Nesses resultados, você verá que os números 'SO72656', 'SO58845' e 'SO70714' contêm as maiores sequências, com oito itens cada. Usando as IDs do pedido, é possível exibir os detalhes de um pedido específico para ver quais itens foram adquiridos e em qual pedido.  
  
|OrderNumber|LineNumber|Modelo|  
|-----------------|----------------|-----------|  
|SO58845|1|Mountain-500|  
|SO58845|2|LL Mountain Tire|  
|SO58845|3|Mountain Tire Tube|  
|SO58845|4|Fender Set - Mountain|  
|SO58845|5|Mountain Bottle Cage|  
|SO58845|6|Water Bottle|  
|SO58845|7|Sport-100|  
|SO58845|8|Jersey Logo de manga longa|  
  
 Porém, alguns clientes que compraram Mountain-500 poderiam comprar produtos diferentes. Você pode exibir todos os produtos que seguem Mountain-500 exibindo a lista de sequências no modelo. Os procedimentos a seguir mostram como exibir estas sequências usando os dois visualizadores fornecidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
#### <a name="to-view-related-sequences-by-using-the-sequence-clustering-viewer"></a>Para exibir sequências relacionadas usando o visualizador de Clustering de Sequência  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no modelo [Clustering de Sequência] e selecione Procurar.  
  
2.  No visualizador de Clustering de Sequência, clique na guia **Transições de Estado** .  
  
3.  Na lista suspensa **Cluster** , certifique-se de que **População (Tudo)** esteja selecionado.  
  
4.  Mova a barra deslizante, à esquerda do painel, para cima para visualizar todos os links.  
  
5.  No diagrama, localize **Mountain-500**e clique no nó do diagrama.  
  
6.  As linhas destacadas apontam para as próximas fases (os produtos que foram adquiridos depois de Mountain-500) e os números indicam a probabilidade. Compare esses aos resultados no visualizador do conteúdo do modelo genérico.  
  
#### <a name="to-view-related-sequences-by-using-the-generic-model-content-viewer"></a>Para exibir sequências relacionadas usando o visualizador do conteúdo do modelo genérico  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no modelo [Clustering de Sequência] e selecione Procurar.  
  
2.  Na lista suspensa do visualizador, selecione **Visualizador de Árvore de Conteúdo Genérica da Microsoft**.  
  
3.  No painel **Legenda do nó** , clique no nó chamado **Nível de sequência para cluster 16.**  
  
4.  No painel Detalhes do nó, localize a linha NODE_DISTRIBUTION e clique em qualquer lugar na tabela aninhada.  
  
     A linha superior sempre será para o valor Missing. Essa linha tem um estado de sequência 0.  
  
5.  Pressione a tecla de seta para baixo ou use as barras de rolagem para percorrer a tabela aninhada até a linha Mountain-500.  
  
     Essa linha tem um estado de sequência 20.  
  
    > [!NOTE]  
    >  Você pode obter o número da linha de um estado de sequência específico de forma programática. Porém, se estiver apenas pesquisando, pode ser mais simples copiar a tabela aninhada para uma pasta de trabalho do Excel.  
  
6.  Retorne para o painel Legenda do nó e expanda o nó **Nível de sequência para cluster 16**, caso ainda não esteja expandido.  
  
7.  Procure **Linha de transição para estado de sequência 20**entre os nós filho. Clique no nó de transição.  
  
8.  A tabela NODE_DISTRIBUTION aninhada contém os produtos e probabilidades a seguir. Compare-os aos resultados na guia **Transição de Estado** do visualizador de Cluster de Sequências.  
  
 A tabela a seguir mostra os resultados da tabela NODE_DISTRIBUTION juntamente com os valores de probabilidade arredondados que são exibidos no visualizador gráfico.  
  
|Product|Suporte (tabela NODE_DISTRIBUTION)|Probabilidade (tabela NODE_DISTRIBUTION))|Probabilidade (do gráfico)|  
|-------------|------------------------------------------|------------------------------------------------|--------------------------------|  
|Missing|48.447887|0.138028169|(não exibido)|  
|Capacete para Ciclismo|10.876056|0.030985915|0.03|  
|Fender Set - Mountain|80.087324|0.228169014|0.23|  
|Luvas de meio dedo|0.9887324|0.002816901|0.00|  
|Hydration Pack|0.9887324|0.002816901|0.00|  
|LL Mountain Tire|51.414085|0.146478873|0.15|  
|Jersey Logo de manga longa|2.9661972|0.008450704|0.01|  
|Mountain Bottle Cage|87.997183|0.250704225|0.25|  
|Mountain Tire Tube|16.808451|0.047887324|0.05|  
|Camisa esportiva clássica de manga curta|10.876056|0.030985915|0.03|  
|Sport-100|20.76338|0.05915493|0.06|  
|Water Bottle|18.785915|0.053521127|0.25|  
  
 Apesar de o caso que selecionamos inicialmente nos dados de treinamento conter o produto 'Mountain-500' seguido pelo produto 'LL Mountain Tire', você pode ver que há várias outras sequências possíveis. Para localizar informações detalhadas para qualquer cluster específico, você deve repetir o processo de detalhamento na lista das sequências no cluster para as transições reais de cada estado ou produto.  
  
 Você pode ir de uma sequência listada em um cluster específico para a linha de transição. Na linha de transição, é possível determinar qual é o próximo produto e voltar para aquele produto na lista de sequências. Ao repetir esse processo para o primeiro e segundo estados, será possível trabalhar em longas cadeias de estados.  
  
## <a name="using-sequence-information"></a>Usando informações da sequência  
 Um cenário comum para clustering de sequência é o controle de cliques do usuário em um site na Web. Por exemplo, se os dados forem dos registros de compras de clientes no site da Web de e-commerce da Adventure Works, o modelo de cluster de sequências resultante poderá ser usado para deduzir o comportamento dos clientes, reprojetar o site de e-commerce para solucionar problemas de navegação ou divulgar promoções.  
  
 Por exemplo, a análise pode mostrar que os usuários sempre seguem uma cadeia específica de produtos, independentemente dos dados demográficos. Além disso, você também pode descobrir que os usuários frequentemente encerram o site depois de clicar em um produto específico. Com isso, é possível se perguntar quais caminhos adicionais poderiam ser fornecidos aos usuários para induzi-los a permanecer no site da Web.  
  
 Se não tiver informações adicionais para classificar seus usuários, poderá simplesmente usar as informações da sequência para coletar dados sobre a navegação e, com isso, compreender melhor o comportamento geral. Entretanto, se puder coletar informações sobre clientes e compará-las com o banco de dados de clientes, poderá combinar a eficácia dos clusterings com a previsão de sequências para fornecer recomendações específicas para o usuário ou ,talvez, com base no caminho de navegação da página atual.  
  
 Outro uso das informações de transição e estado compiladas por um modelo de clustering de sequência é para determinar quais caminhos possíveis nunca são usados. Por exemplo, se você tiver muitos visitantes que foram das páginas 1 a 4, mas que nunca continuam até a página 5, poderá investigar se há problemas que estão impedindo a navegação na página 5. Isso pode ser feito ao consultar o conteúdo do modelo e compará-lo a uma lista de caminhos possíveis.  Os gráficos que indicam todos os caminhos de navegação em um site da Web podem ser criados programaticamente ou usando diversas ferramentas de análise do site.  
  
 Para saber como obter a lista dos caminhos observados ao consultar o conteúdo do modelo e para verificar exemplos de consultas em um modelo de clustering de sequência, consulte [Exemplos de consulta de modelo de clustering em sequência](clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Algoritmo msc](microsoft-sequence-clustering-algorithm.md)   
 [Exemplos de consulta dos modelos de clustering de sequências](clustering-model-query-examples.md)  
  
  
