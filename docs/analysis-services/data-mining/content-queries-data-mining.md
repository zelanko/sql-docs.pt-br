---
title: "Consultas (mineração de dados) de conteúdo | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4f4a5a8-a230-4222-bece-9d563501f65f
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45a912354d122eadb7008c2ff260366fa46770fe
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="content-queries-data-mining"></a>Consultas de conteúdo (mineração de dados)
  Uma consulta de conteúdo é um modo de extrair informações sobre as estatísticas internas e a estrutura do modelo de mineração propriamente dito. Às vezes uma consulta de conteúdo pode fornecer detalhes que não estão prontamente disponível no visualizador. Você também pode usar os resultados de uma consulta de conteúdo para extrair informações programaticamente por outros usos.  
  
 Esta seção fornece informações gerais sobre os tipos de informações que podem ser recuperadas com uma consulta de conteúdo e a sintaxe DMX geral para consultas de conteúdo.  
  
 [Consultas básicas de conteúdo](#bkmk_ContentQuery)  
  
-   [Consultas sobre estrutura e dados do caso](#bkmk_Structure)  
  
-   [Consultas em padrões de modelo](#bkmk_Patterns)  
  
 [Exemplos](#bkmk_Examples)  
  
-   [Consulta de conteúdo em um modelo de associação](#bkmk_Assoc)  
  
-   [Consulta de conteúdo em um modelo de árvores de decisão](#bkmk_DecTree)  
  
 [Trabalhando com resultados de consulta](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> Consultas básicas de conteúdo  
 Você pode criar consultas de conteúdo usando o Construtor de consulta de previsão, usar os modelos de consulta de conteúdo DMX fornecidos no SQL Server Management Studio ou escrever consultas diretamente no DMX. Ao contrário das consultas de previsão, você não precisa unir dados externos e, dessa maneira, as consultas de conteúdo são fáceis escrever.  
  
 Esta seção fornece uma visão geral dos tipos de consultas de conteúdo que você pode criar.  
  
-   Consultas na estrutura de mineração ou dados de caso permitem exibir os dados detalhados que foram usados para treinamento.  
  
-   As consultas no modelo podem retornar padrões, listas de atributos, fórmulas e assim por diante.  
  
###  <a name="bkmk_Structure"></a> Consultas sobre estrutura e dados do caso  
 O DMX dá suporte a consultas nos dados armazenados em cache que são usados para criar estruturas de mineração e modelos. Por padrão, este cache é criado quando você define a estrutura de mineração, e é populado quando você processa a estrutura ou modelo.  
  
> [!WARNING]  
>  Este cache não poderá ser desmarcado ou excluído se você precisar separar dados em conjuntos de treinamento e teste. Se o cache for desmarcado, você não poderá consultar os dados do caso.  
  
 Os exemplos a seguir mostram os padrões comuns para criar consultas nos dados de caso ou consultas nos dados na estrutura de mineração:  
  
 **Obtenha todos os casos para um modelo**  
 `SELECT FROM <model>.CASES`  
  
 Use esta instrução para recuperar colunas especificadas nos dados do caso usados para criar um modelo. Você deve ter permissões de detalhamento no modelo para executar esta consulta.  
  
 **Exibir todos os dados que estão incluídos na estrutura**  
 `SELECT FROM <structure>.CASES`  
  
 Use essa instrução para exibir todos os dados incluídos na estrutura, incluindo as colunas que não foram adicionadas a um modelo de mineração específico. Você deve ter permissões de detalhamento no modelo, assim como na estrutura, para recuperar dados da estrutura de mineração.  
  
 **Obter intervalo de valores**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 Use esta instrução para localizar o valor mínimo, o valor máximo e a média de uma coluna contínua, ou dos buckets de uma coluna DISCRETIZED.  
  
 **Obter valores distintos**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 Use esta instrução para recuperar todos os valores de uma coluna DISCRETE.  Não use esta instrução para colunas DISCRETIZED; use as funções **RangeMin** e **RangeMax** .  
  
 **Localizar os casos usados para treinar um modelo ou estrutura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 Use esta instrução para obter o conjunto completo de dados que foram usados um modelo de treinamento.  
  
 **Localizar os casos que foram usados para testar um modelo ou estrutura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 Use esta instrução para obter os dados que foram colocados de lado para testar modelos de mineração relacionados a uma estrutura específica.  
  
 **Detalhar de um padrão de modelo específico para dados de caso subjacentes**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 Use esta instrução para recuperar dados de caso detalhado de um modelo treinado. Você deve especificar um nó específico: por exemplo, você deve saber a ID do nó do cluster, a ramificação específica da árvore de decisão etc. Além disso, você deve ter permissões de detalhamento no modelo para executar esta consulta.  
  
###  <a name="bkmk_Patterns"></a> Consultas em padrões de modelo, estatísticas e atributos  
 O conteúdo de um modelo de mineração de dados é útil para muitos propósitos. Com uma consulta de conteúdo modelo, você pode:  
  
-   Extrair fórmulas ou probabilidades para fazer seus próprios cálculos.  
  
-   Para um modelo de associação, recupere as regras que são usadas para gerar uma previsão.  
  
-   Recuperar as descrições de regras específicas de forma que você possa usar as regras em um aplicativo personalizado.  
  
-   Exibir as médias móveis detectadas por um modelo de série temporal.  
  
-   Obter a fórmula de regressão para algum segmento da linha de tendência.  
  
-   Recuperar informações acionáveis sobre clientes identificados como fazendo parte de um cluster específico.  
  
 Os exemplos a seguir mostram alguns dos padrões comuns para criar consultas no conteúdo do modelo:  
  
 **Obter padrões do modelo**  
 `SELECT FROM <model>.CONTENT`  
  
 Use esta instrução para recuperar informações detalhadas sobre nós específicos no modelo. Dependendo do tipo de algoritmo, o nó pode conter regras e fórmulas, suporte e estatísticas de variância, e assim sucessivamente.  
  
 **Recuperar atributos usados em um modelo treinado**  
 `CALL System.GetModelAttributes(<model>)`  
  
 Use este procedimento armazenado para recuperar a lista de atributos que foram usados por um modelo. Estas informações são úteis para determinar atributos que foram eliminados como resultado de seleção de recursos, por exemplo.  
  
 **Recuperar conteúdo armazenado em uma dimensão de mineração de dados**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 Use esta instrução para recuperar os dados de uma dimensão de mineração de dados.  
  
 Esse tipo de consulta destina-se principalmente ao uso interno. No entanto, nem todos os algoritmos dão suporte a esta funcionalidade. O suporte é indicado por um sinalizador no conjunto de linhas do esquema MINING_SERVICES.  
  
 Se você desenvolver seu próprio algoritmo de plug-in, pode usar esta instrução para verificar o conteúdo de seu modelo para testar.  
  
 **Obtenha a representação PMML de um modelo.**  
 `SELECT * FROM <model>.PMML`  
  
 Obtém um documento XML que representa o modelo em formato de PMML. Não há suporte para todos os tipos de modelo.  
  
##  <a name="bkmk_Examples"></a> Exemplos  
 Embora algum conteúdo de modelo seja padrão entre algoritmos, algumas partes do conteúdo variam enormemente dependendo do algoritmo usado para criar o modelo. Desse modo, ao criar uma consulta de conteúdo, você precisa saber quais as informações do modelo mais úteis para seu modelo específico.  
  
 Alguns exemplos são fornecidos nesta seção para ilustrar como a escolha de algoritmo afeta o tipo de informação que é armazenada no modelo. Para obter mais informações sobre o conteúdo do modelo de mineração e o conteúdo específico para cada tipo de modelo, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Assoc"></a> Exemplo 1: Consulta de conteúdo em um modelo de associação  
 A instrução `SELECT FROM <model>.CONTENT`retorna tipos diferentes de informações, dependendo do tipo de modelo que você está consultando. Para um modelo de associação, uma informação importante é o *tipo de nó*. Os nós são como contêineres para informações no conteúdo do modelo. Em um modelo de associação, os nós que representam regras têm o valor de NODE_TYPE igual a 8, enquanto os nós que representam conjuntos de itens têm um valor de NODE_TYPE igual a 7.  
  
 Assim, a consulta a seguir retorna os 10 principais conjuntos de itens, classificados por suporte (a ordem padrão).  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 A consulta a seguir é criada com base nestas informações. A consulta retorna três colunas: a ID do nó, a regra completa e o produto na lateral direita do conjunto de itens, isto é, o produto previsto para ser associado a alguns outros produtos como parte de um conjunto de itens.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 A palavra-chave FLATTENED indica que o conjunto de linhas aninhado deve ser convertido em uma tabela simples. O atributo que representa o produto na lateral direita da regra está contido na tabela NODE_DISTRIBUTION; portanto, recuperamos somente a linha que contém um nome de atributo, adicionando um requisito para que o comprimento seja maior do que 2.  
  
 Uma função de cadeia de caracteres simples é usada para remover o nome do modelo da terceira coluna. (Normalmente, o nome do modelo é antecedido pelos valores de colunas aninhadas.)  
  
 A cláusula WHERE especifica que o valor de NODE_TYPE deve ser 8 para recuperar apenas regras.  
  
 Para ver mais exemplos, consulte [Exemplos de consulta de um modelo associação](../../analysis-services/data-mining/association-model-query-examples.md).  
  
###  <a name="bkmk_DecTree"></a> Exemplo 2: Consulta de conteúdo em um modelo de árvores de decisão  
 Um modelo de árvore de decisão pode ser usado para previsão e também para classificação.  Este exemplo presume que você esteja usando o modelo para prever um resultado, mas você também quer descobrir quais fatores ou regras podem ser usados para classificar o resultado.  
  
 Em um modelo de árvore de decisão, os nós são usados para representar árvores e nós folha. A legenda para cada nó contém a descrição do caminho ao resultado. Portanto, para rastrear o caminho para qualquer resultado específico, você precisa identificar o nó que o contém e obter os detalhes para aquele nó.  
  
 Em sua consulta de previsão, você adiciona a função de previsão [PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md), para obter a ID do nó relacionado, como mostrado no exemplo a seguir:  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 Assim que você obtiver a ID do nó que contém o resultado, poderá recuperar a regra ou o caminho que explica a previsão criando uma consulta de conteúdo, que inclui NODE_CAPTION da seguinte maneira:  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 Para obter mais exemplos, consulte [Exemplos de consulta de modelo de árvores de decisão](../../analysis-services/data-mining/decision-trees-model-query-examples.md).  
  
##  <a name="bkmk_Results"></a> Trabalhando com resultados de consulta  
 Como demonstram os exemplos, as consultas de conteúdo retornam principalmente conjuntos de linhas tabulares, mas também podem incluir informações de colunas aninhadas. Você pode aplainar o conjunto de linhas que é retornado, mas isto pode tornar mais complexo o trabalho com resultados. O conteúdo do nó NODE_DISTRIBUTION em particular está aninhado, mas contém muitas informações interessantes sobre o modelo.  
  
 Para obter mais informações sobre como trabalhar com conjuntos de linhas hierárquicas, consulte a especificação OLEDB no MSDN.  
  
## <a name="see-also"></a>Consulte também  
 [Compreendendo a instrução DMX Select](../../dmx/understanding-the-dmx-select-statement.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
