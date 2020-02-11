---
title: Análise da cesta de compras (tabela AnalysisTools para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shopping basket analysis
- mining model, association
- Table Analysis tools
- association [data mining]
- market basket analysis
ms.assetid: ba40cf43-f286-49ad-8316-70f5b11f1dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dadc054a3f9927c09e9e236044dd5ddee7f3a9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068675"
---
# <a name="shopping-basket-analysis-table-analysistools-for-excel"></a>Análise da Cesta de Compras (Ferramentas de Análise de Tabela para Excel)
  ![Ferramenta Cesta de Compras](media/tat-shopbskt.gif "Ferramenta Cesta de Compras")  
  
 A ferramenta de **análise de cesta** de compras `associations` ajuda você a encontrar em seus dados. Uma associação pode informar quais itens são frequentemente adquiridos ao mesmo tempo. Em Data Mining, essa técnica é um método conhecido conhecido como análise de *cesta*de compras, usado para analisar o comportamento de compra de clientes em conjuntos de dados muito grandes. Os analistas de marketing podem usar as informações para recomendar produtos relacionados aos clientes e promover produtos relacionados substituindo-os em páginas da Web próximas, em catálogos ou no comércio.  
  
 Para usar a análise da cesta de compras, os itens que você deseja analisar devem estar relacionados por uma ID da transação. Por exemplo, se você estiver analisando todos os pedidos recebidos por meio de um site, cada pedido terá uma ID do pedido ou da transação associada a um ou mais itens comprados.  
  
 Quando o assistente terminar de analisar os dados, ele criará duas novas planilhas, **grupos de itens de cesta de compras** e regras de cesta de **compras**.  
  
 A planilha **grupos de itens da cesta de compras** contém uma lista dos itens que frequentemente aparecem juntos em transações. Esses agrupamentos comuns são chamados de *conjuntos*de itens. A planilha também contém estatísticas, como *suporte* e *elevação*, para ajudá-lo a entender o significado do conjunto. Se houver informações de preço disponíveis, a planilha também criará uma soma dos valores de todos os itens relacionados, para fornecer uma indicação do valor total das transações.  
  
 Você pode filtrar e classificar as colunas no relatório. Por exemplo, talvez você queira exibir apenas esses conjuntos de itens com dois ou mais produtos ou ordenar os conjuntos de linhas por **valor médio da cesta**.  
  
 A planilha **regras de cesta de compras** usa as estatísticas derivadas da análise para criar regras sobre como os itens são relacionados. Por exemplo, uma regra pode ser que, se os clientes comprarem o produto A, eles terão grande probabilidade de comprar o produto B. As regras podem ser usadas para criar recomendações. Cada regra tem estatísticas de suporte que ajudam a avaliar sua força potencial, para que você só possa fazer uma recomendação se a regra exceder um determinado limite de probabilidade.  
  
## <a name="using-the-shopping-basket-analysis-tool"></a>Usando a ferramenta Análise da Cesta de Compras  
  
1.  Abra uma tabela do Excel que contenha dados apropriados. Na pasta de trabalho de amostra, clique em Associar planilha.  
  
2.  Clique em **análise da cesta de compras**.  
  
3.  Na caixa de diálogo **análise da cesta de compras** , escolha a coluna que contém a ID da transação e escolha a coluna que contém os itens ou os produtos que você deseja analisar.  
  
4.  Se desejar, adicione uma coluna que contenha valores de produtos.  
  
5.  Clique em**avançado**para abrir a caixa de diálogo **configuração de parâmetros avançados** . Aumente o valor do **suporte mínimo** para reduzir o número de produtos agrupados como conjuntos de itens. Aumente a **probabilidade de regra mínima** para filtrar conjuntos de itens muito comuns.  
  
### <a name="requirements"></a>Requisitos  
 Para usar a ferramenta de **análise de cesta de compras** , seus dados devem ser armazenados em uma tabela do Excel e devem conter as seguintes colunas:  
  
-   Coluna que contenha uma ID exclusiva representando a transação. A ID pode ser numérica ou de texto, desde que o valor em cada linha seja exclusivo.  
  
-   Coluna que contenha o item ou produto que você está analisando.  
  
-   Uma coluna numérica opcional que representa o preço ou o valor de cada item. Essa coluna é usada para agregar o valor dos conjuntos de itens nos quais cada produto é encontrado e pode ajudá-lo a entender o valor total de certas transações.  
  
## <a name="how-items-are-associated"></a>Como os itens são associados  
 Os itens individuais que você está analisando devem ser agrupados por algum identificador que represente o caso, a transação ou a ocasião. Assim, você escolherá a coluna de ID da transação como o identificador, e não o número de ID do cliente ou o número de ID do produto.  
  
 Quando a ferramenta examina os produtos em cada transação, cria um conjunto de itens para cada combinação de itens que encontra. Por exemplo, se um cliente comprou três itens em uma única visita, há 7 conjuntos de itens possíveis: cada produto considerado independentemente, cada produto agrupado com outro produto e a combinação de todos os três produtos.  
  
> [!NOTE]  
>  É possível filtrar os conjuntos de itens que contêm itens exclusivos, mas a ferramenta precisa analisá-los para gerar estatísticas significativas para o conjunto de dados.  
  
 O suporte para cada conjunto de itens é calculado como o número de clientes que desejam comprar um conjunto de itens. No exemplo mencionado, se houver apenas um cliente que comprou 3 itens, com 7 conjuntos de itens possíveis, cada um desses 7 conjuntos de itens terá um valor de suporte de 1. À medida que o número de clientes aumenta e que o número de combinações possíveis cresce, o processamento do relatório poderá demorar muito mais. No entanto, alguns conjuntos de itens podem ter muito pouco suporte. Assim, talvez você decida reduzir o tempo necessário para gerar o relatório limitando o número de itens em cada conjunto de itens a 3 ou menos. Em geral, conjuntos de itens maiores têm muito menos suporte, portanto, a troca é aceitável.  
  
## <a name="specifying-minimum-support-and-rule-probability"></a>Especificando o suporte mínimo e a regra de probabilidade  
 À medida que os conjuntos de dados ficam maiores, o número de agrupamentos de itens possíveis e regras pode ficar muito grande. No entanto, você pode controlar o número de resultados gerados pela ferramenta, para enfatizar apenas os mais valiosos conjuntos de itens e regras. Defina essas opções na caixa de **diálogo parâmetros avançados da cesta de compras**.  
  
### <a name="minimum-support"></a>Suporte mínimo  
 *Suporte mínimo* significa o número de transações que devem conter um conjunto específico para que o conjunto seja considerado significativo. Por exemplo, talvez você não esteja interessado em um conjunto de itens, a menos que tenha sido adquirido em pelo menos 10 transações diferentes. Há duas maneiras de controlar o limite para o significância conjunto e ambos usam o parâmetro de **suporte mínimo** .  
  
 **Como um valor absoluto:** Insira um número que representa a contagem de transações que contêm os itens de destino. Por exemplo, se você inserir 10, qualquer conjunto de itens que apareça em pelo menos 10 cestas de compras será incluído nos resultados.  
  
 **Como uma porcentagem:** Insira um número que representa um percentual da coleção inteira de conjuntos de itens. Por exemplo, se você especificar 10, todos os conjuntos de itens serão contados e o conjunto de itens de destino deve parecer constituir pelo menos 10% do número total de conjuntos de itens. Se houver um conjunto de dados muito grande, o uso de porcentagens, em vez de uma contagem pode ajudá-lo a enfatizar os agrupamentos de itens mais importantes.  
  
> [!NOTE]  
>  Lembre-se: o número de conjuntos de itens é diferente do número de transações nos dados. Cada transação pode conter vários conjuntos de itens; no entanto, a maioria dos conjuntos de itens se repete várias vezes no conjunto de dados.  
  
### <a name="rule-probability-and-rule-importance"></a>Regra de probabilidade e regra de importância  
 A probabilidade de uma regra descrever como o resultado de uma ocorrerá. A regras de probabilidade é calculada com o uso da frequência dos conjuntos de itens com suporte para uma regra. Se um conjunto de itens ocorrer muito raramente, ele terá uma probabilidade baixa.  
  
 No entanto, regras que tenham alta probabilidade talvez nem sempre sejam úteis. Talvez elas indiquem conjuntos de itens comprados com frequência e, portanto, não precisem de promoção adicional. A importância é projetada para medir a utilidade de uma regra. Às vezes, uma regra pode ter uma probabilidade muito alta, mas pouca importância, porque a previsão não fornece novas informações. Por exemplo, se cada conjunto de itens contiver um estado específico de um atributo, uma regra que prevê o estado será trivial, embora a probabilidade seja muito alta.  
  
 Teste essas configurações para visualizar resultados diferentes e determinar qual delas gera as regras mais interessantes.  
  
## <a name="understanding-the-reports"></a>Entendendo os relatórios  
 A ferramenta de **análise de cesta de compras** cria dois relatórios complementares. O primeiro relatório, intitulado **grupos significativos de itens identificados durante a análise**, fornece uma lista de todos os conjuntos de item que foram encontrados. Use as novas ferramentas de tabela no Microsoft Excel para classificar, filtrar e explorar os dados.  
  
 O segundo relatório, intitulado **regras de cesta de compras**, informa que tipo de inferência pode ser feita com base nos conjuntos de itens listados no primeiro relatório. Enquanto a lista de conjuntos de itens é mais útil para explorar e entender os dados, a lista de regras é mais útil para fazer previsões e recomendações.  
  
### <a name="shopping-basket-item-groups-report"></a>Relatório de grupos de itens da cesta de compras  
 Este relatório contém uma lista de todas as combinações de itens possíveis encontradas no conjunto de dados. Por exemplo, se os dados da transação contiverem pedidos, para cada pedido, a ferramenta de **análise da cesta de compras** calculará quantas vezes o item individual foi ordenado e, em seguida, calculará todas as combinações desse item com outros itens.  
  
 O relatório lista os conjuntos de itens encontrados em ordem de comparação de precisão. A comparação de precisão é uma pontuação que informa a importância do conjunto de itens.  
  
|Coluna no relatório|O que informa|  
|----------------------|-----------------------|  
|Grupo de Itens|Lista os conjuntos de itens ou a combinação de itens.|  
|Tamanho do Grupo|Uma contagem do número de itens no conjunto de itens. Você pode filtrar este campo para visualizar apenas pares de itens, itens únicos etc.|  
|Suporte|Uma contagem do número de casos em que a combinação ocorreu. Você pode classificar nesta coluna para visualizar os conjuntos de itens mais comuns.|  
|Valor Médio|Uma soma dos valores dos itens nestes conjuntos de itens, dividida pelo suporte. Você pode classificar e filtrar esta coluna para direcionar produtos em intervalos de preços diferentes.|  
|Valor Médio da Cesta|Uma soma dos valores de todos os itens em pedidos que contêm este conjunto de itens, dividida pelo suporte. Essa estatística é interessante quando associada ao valor médio do conjunto de itens.|  
|Comparação de Precisão|Uma pontuação que representa o quão interessante este conjunto de itens é em todo o conjunto de dados. A comparação de precisão é calculada pela obtenção da probabilidade de dois itens ocorrerem juntos, e pela divisão da probabilidade de dois itens ocorrerem independentemente. Como resultado, se houver uma correlação forte entre os itens, a pontuação de comparação de precisão será mais alta.|  
  
### <a name="shopping-basket-rules-report"></a>Relatório de regras da cesta de compras  
 Este relatório contém um conjunto de regras criadas pela análise dos conjuntos de itens encontrados. Por exemplo, se os dados da transação revelaram que os Produtos A e B foram comprados juntos com frequência, a ferramenta Análise da Cesta de Compras criará uma regra para prever A dada a existência de B ou B dada a existência de A.  
  
 Cada regra é associada a uma probabilidade, derivada dos dados de suporte. Essas probabilidades são úteis para fazer recomendações. Por exemplo, talvez você só queira visualizar regras que tenham pelo menos 50% de possibilidade de ser precisas, com base nos dados existentes.  
  
 O relatório lista os conjuntos de itens encontrados em ordem de comparação de precisão. A comparação de precisão é uma pontuação que informa a importância do conjunto de itens.  
  
|Coluna no relatório|O que informa|  
|----------------------|-----------------------|  
|Itens Existentes|Lista os itens necessários para fazer uma recomendação.<br /><br /> Em Data Mining, esses itens são considerados no *lado esquerdo* da regra de associação.|  
|Item Previsto|Lista o item a ser recomendado.<br /><br /> Em Data Mining, esses itens são considerados no *lado direito* da regra de associação.|  
|Probabilidade|Exibe a probabilidade de a regra estar correta.|  
|Suporte|Indica o número de casos nos dados existentes que fornecem evidências para a regra.|  
|Valor da Regra|Se você fornecer um valor para os itens na análise de compras, essa coluna calculará o valor da previsão, dado o custo dos itens.|  
|Comparação de Precisão|Indica a intensidade da correlação entre os itens na primeira coluna e os itens na segunda coluna. Também conhecido como *importância*.<br /><br /> Uma comparação de precisão de 0 significa que não há correlação. Um valor positivo significa que os itens na primeira coluna preveem o item na segunda coluna. Quanto maior o número, mais sólida a correlação.|  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece funções de mineração de dados mais avançadas, também contém um assistente que executa análise de associação. Para obter mais informações, consulte [Assistente de associação &#40;cliente de mineração de dados para Excel&#41;](associate-wizard-data-mining-client-for-excel.md).  
  
 Para obter mais informações sobre o algoritmo usado para executar esta análise, consulte o tópico "Algoritmo Associação da Microsoft" nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
