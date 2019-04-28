---
title: Consultas de previsão (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 935cd8ec3f4e5069807e914e5af20e39b645deb3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733192"
---
# <a name="prediction-queries-data-mining"></a>Prediction Queries (Data Mining)
  O objetivo de um projeto de mineração de dados típico é usar o modelo de mineração para fazer previsões. Por exemplo, você pode querer prever a quantidade de tempo de inatividade esperado para um determinado cluster de servidores ou gerar uma pontuação que indica a probabilidade de os segmentos de clientes responderem a uma campanha publicitária. Para fazer todas estas coisas, você cria uma consulta de previsão.  
  
 Funcionalmente, há tipos diferentes de consultas de previsão com suporte no SQL Server, dependendo do tipo de entradas à consulta:  
  
|Tipo de consulta|Opções de consulta|  
|----------------|-------------------|  
|Consultas de previsão singleton|Use uma consulta singleton quando quiser prever resultados para um único caso novo ou para vários casos novos. Você fornece os valores de entrada diretamente na consulta e ela é executada como uma única sessão.|  
|Previsões em lotes|Use previsões em lote quando você tiver dados externos que você queira alimentar no modelo, para usar como a base para previsões. Para fazer previsões para um conjunto inteiro de dados, você mapeia os dados na origem externa para as colunas no modelo e, em seguida, especifica o tipo de dados preditivos que deseja produzir.<br /><br /> A consulta para o conjunto de dados inteiro é executada em uma única sessão, tornando esta opção muito mais eficiente que enviar diversas consultas repetidas.|  
|Previsões de série temporal|Use uma consulta de série temporal quando quiser prever um valor em algumas etapas futuras. O SQL Server Data Mining também fornece as seguintes funcionalidades em consultas de série temporal:<br /><br /> Estenda um modelo existente adicionando dados novos como parte da consulta e faça previsões baseadas na série composta.<br /><br /> Aplique o modelo existente a uma nova série de dados usando a opção REPLACE_MODEL_CASES.<br /><br /> Você pode executar previsão cruzada.|  
  
 As seções a seguir descrevem a sintaxe geral de consultas de previsão, os tipos diferentes de consultas de previsão, e como trabalhar com os resultados de consultas de previsão.  
  
 [Design básico de consulta de previsão](#bkmk_PredQuery)  
  
-   [Adicionando funções de previsão](#bkmk_PredFunc)  
  
-   [Consultas singleton](#bkmk_SingletonQuery)  
  
-   [Consultas de previsão em lotes](#bkmk_BatchQuery)  
  
 [Trabalhando com os resultados de consultas](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> Design básico de consulta de previsão  
 Ao criar uma previsão, você normalmente fornece alguns dados novos e solicita ao modelo para gerar uma previsão com base nos dados novos.  
  
-   Em uma consulta de lote, mapeie o modelo para uma fonte de dados externa usando uma *junção de previsão*.  
  
-   Em uma consulta de previsão singleton, digite um ou mais valores para usar como entradas. Ainda é possível criar várias previsões usando uma consulta de previsão singleton. Porém, se você precisar criar muitas previsões, o desempenho será melhor quando você usar uma consulta de lote.  
  
 As consultas de previsão singleton e de lote usam a sintaxe PREDICTION JOIN para definir os novos dados. A diferença está no modo como a entrada da junção da previsão é especificada.  
  
-   Em uma consulta de previsão por lotes, os dados vêm de uma fonte de dados externa especificada com o uso da consulta OPENQUERY.  
  
-   Em uma consulta de previsão singleton, os dados são fornecidos embutidos como parte da consulta.  
  
 Para modelos de série temporal, os dados de entrada não são sempre necessários; é possível fazer previsões usando apenas nos dados existentes no modelo. No entanto, se você especificar novos dados de entrada, precisará optar entre usar os novos dados para atualizar e estender o modelo, ou substituir a série original dos dados que foram usados no modelo.  Para obter mais informações sobre essas opções, consulte [Time Series Model Query Examples](time-series-model-query-examples.md).  
  
###  <a name="bkmk_PredFunc"></a> Adicionando funções de previsão  
 Além de prever um valor, é possível personalizar uma consulta de previsão para retornar vários tipos de informações relacionadas à previsão. Por exemplo, se a previsão criar uma lista de produtos para recomendar a um cliente, talvez você também queira retornar a probabilidade para cada previsão, de forma que possa classificá-las e apresentar somente as principais recomendações para o usuário.  
  
 Para fazer isso, adicione *funções de previsão* à consulta. Cada modelo ou tipo de consulta dá suporte a funções específicas. Por exemplo, os modelos de clustering oferecem suporte a funções de previsão especiais que fornecem detalhes adicionais sobre os clusters criados pelo modelo, ao passo que modelos de série temporal têm funções que calculam diferenças com o passar do tempo. Também há funções de previsão gerais que funcionam com quase todos os tipos de modelo. Para obter uma lista das funções de previsão com suporte em tipos diferentes de consultas, consulte este tópico de referência DMX:  [Funções de previsão gerais &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
###  <a name="bkmk_SingletonQuery"></a> Criando consultas de previsão singleton  
 Uma consulta de previsão singleton é útil quando você deseja criar previsões rápidas em tempo real. Um cenário comum pode ser que você obteve informações de um cliente, talvez usando um formulário em um site e, em seguida, quer enviar esses dados como a entrada para uma consulta de previsão singleton. Por exemplo, quando um cliente escolher um produto de uma lista, você poderá usar a seleção como a entrada para uma consulta que prevê os melhores produtos para recomendar.  
  
 As consultas de previsão singleton não exigem uma tabela separada que contém entrada. Você fornece uma ou várias linhas de valores como entrada para o modelo e as previsões são retornadas em tempo real.  
  
> [!WARNING]  
>  Apesar do nome, consultas de previsão singleton não fazem apenas previsões únicas-você pode gerar várias previsões para cada conjunto de entradas. Forneça vários casos de entrada criando uma instrução SELECT para cada caso de entrada e combinando-os com o operador UNION.  
  
 Ao criar uma consulta de previsão singleton, é necessário fornecer os novos dados ao modelo na forma de uma PREDICTION JOIN. Isso significa que, mesmo que não esteja mapeando para uma tabela real, você deve verificar se os novos dados correspondem às colunas existentes no modelo de mineração. Se as colunas dos novos dados e os novos dados corresponderem de modo exato, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mapeará as colunas. Isto é chamado de *JUNÇÃO DE PREVISÃO NATURAL*. No entanto, se as colunas não coincidirem ou se os novos dados não tiverem o mesmo tipo e quantidade de dados do modelo, especifique quais colunas do modelo devem ser mapeadas para os novos dados ou especifique os valores ausentes.  
  
###  <a name="bkmk_BatchQuery"></a> Consultas de previsão em lotes  
 Uma consulta de previsão em lote é útil quando você tem dados externos que deseja usar fazendo previsões. Por exemplo, você pode ter criado um modelo que categoriza clientes por sua atividade online e histórico de compras. Você pode aplicar esse modelo a uma lista de clientes potenciais recém-adquiridos para criar projeções para vendas, ou identificar alvos para campanhas propostas.  
  
 Quando você realiza uma junção de previsão, deve mapear as colunas do modelo para as colunas na nova fonte de dados. Portanto, a fonte de dados que você escolher para uma entrada deve conter dados que sejam semelhantes aos dados no modelo. As novas informações não têm que corresponder exatamente e podem estar incompletas. Por exemplo, suponha que o modelo foi treinado usando informações sobre renda e idade; porém, a lista de clientes usada para previsões tem dados sobre idade mas não sobre renda. Neste cenário, você ainda pode mapear os novos dados para o modelo e criar uma previsão para cada cliente. Entretanto, se a renda fosse uma previsor importante para o modelo, a falta de informações completas afetaria a qualidade de previsões.  
  
 Para obter os melhores resultados, você deverá unir o máximo de colunas correspondentes possível entre os novos dados e o modelo. No entanto, a consulta será bem-sucedida mesmo se não houver nenhuma correspondência. Se nenhuma coluna for unida, a consulta retornará a previsão marginal, que é equivalente à instrução `SELECT <predictable-column> FROM <model>` sem uma cláusula PREDICTION JOIN.  
  
 Depois de ter mapeado com sucesso todas as colunas relevantes, execute a consulta e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] faz previsões para cada linha dos novos dados com base nos padrões do modelo. Você poderá salvar os resultados de volta para a nova tabela na exibição da fonte de dados que contém os dados externos, ou pode copiar e colar os dados se estiver usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  Se você usar o designer no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a fonte de dados externa deverá ser definida primeiro como uma exibição da fonte de dados.  
  
 Se a linguagem DMX for usada para criar uma junção de previsão, especifique a fonte de dados externa usando os comandos OPENQUERY, OPENROWSET ou SHAPE. O método de acesso aos dados padrão nos modelos DMX é OPENQUERY. Para obter mais informações sobre esses métodos, consulte [&#60;consulta de dados de origem&#62;](/sql/dmx/source-data-query).  
  
###  <a name="bkmk_TSQuery"></a> Previsões em modelos de mineração de série temporal  
 Modelos de série temporal são diferentes de outros tipos de modelos; você pode usar o modelo como ele é para criar previsões, ou pode fornecer novos dados para o modelo para atualizá-lo e criar previsões com base em tendências recentes. Se você adicionar novos dados, poderá especificar o modo como os novos dados devem ser usados.  
  
-   *Estender os casos de modelo* significa que você adiciona os novos dados à série existente de dados no modelo de série temporal. Daqui em diante, as previsões são baseadas na nova série combinada. Esta opção é boa quando você quiser simplesmente adicionar alguns pontos de dados a um modelo existente.  
  
     Por exemplo, imagine que você tenha um modelo de série temporal existente treinado nos dados de vendas do ano anterior. Após coletar vários meses de novos dados de vendas, você decide atualizar suas previsões de vendas para o ano atual. Você pode criar uma junção de previsão que atualize o modelo adicionando novos dados e que estenda o modelo para fazer novas previsões.  
  
-   *Substituir casos do modelo* significa manter o modelo treinado, mas substituir os casos subjacentes por um novo conjunto de dados de caso. Esta opção é útil quando você quiser manter a tendência no modelo, mas aplicá-lo a um conjunto diferente de dados.  
  
     Por exemplo, seu modelo original pode ter sido treinado em um conjunto de dados com volumes de vendas muito altos; quando você substituir os dados subjacentes por uma nova série (talvez de um repositório com volume de vendas inferior), preserva a tendência, mas as previsões começam dos valores na série de substituição.  
  
 Independentemente da abordagem usada, o ponto de partida para previsões sempre é o término da série original.  
  
 Para obter mais informações sobre como criar junções de previsão em modelos de série temporal, consulte [Exemplos de consulta de um modelo de série temporal](time-series-model-query-examples.md) ou [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
##  <a name="bkmk_WorkResults"></a> Trabalhando com os resultados de uma consulta de previsão  
 Suas opções para salvar os resultados de uma consulta de previsão de mineração de dados são diferentes dependendo de como você cria a consulta.  
  
-   Quando você criar uma consulta usando o Construtor de Consultas de Previsão no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], poderá salvar os resultados de uma consulta de previsão em uma fonte de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Exibir e salvar os resultados de uma consulta de previsão](view-and-save-the-results-of-a-prediction-query.md).  
  
-   Quando você cria consultas de previsão que usam DMX no painel de Consulta do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], pode usar as opções de saída de consulta para salvar os resultados em um arquivo, ou no painel Resultados da Consulta como texto ou em uma grade. Para obter mais informações, veja [Editores de Consultas e de Texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
-   Quando você executa uma consulta de previsão usando os componentes do Integration Services, as tarefas fornecem a capacidade de gravar os resultados em um banco de dados usando um gerenciador de conexões ADO.NET disponível ou um gerenciador de conexões OLEDB. Para obter mais informações, consulte [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
 É importante compreender que os resultados de uma consulta de previsão não são como os resultados de uma consulta em um banco de dados relacional, que sempre retorna uma única linha de valores relacionados. Cada função de previsão DMX adicionada a uma consulta retorna seu próprio conjunto de linhas. Portanto, ao fazer previsões em um único caso, o resultado pode ser um valor estimado junto com várias colunas de tabelas aninhadas que contêm detalhes adicionais.  
  
 Sempre que você combina várias funções em uma consulta, os resultados retornados são combinados como um conjunto de linhas hierárquico. Por exemplo, digamos que você use um modelo de série temporal para prever valores futuros para a quantidade de vendas, usando uma consulta como esta instrução DMX:  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 Os resultados desta consulta são duas colunas, uma para cada série prevista, onde cada linha contém uma tabela aninhada com os valores previstos:  
  
 **PredictedAmount**  
  
|$TIME|Valor|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Valor|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|201102|260|  
  
 Se o provedor não puder manipular conjuntos de linhas hierárquicos, você poderá mesclar os resultados usando a palavra-chave FLATTEN na consulta de previsão. Para obter mais informações, inclusive exemplos de conjuntos de linhas bidimensionais, consulte [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de conteúdo &#40;Data Mining&#41;](content-queries-data-mining.md)   
 [Consultas de definição de dados &#40;Data Mining&#41;](data-definition-queries-data-mining.md)  
  
  
