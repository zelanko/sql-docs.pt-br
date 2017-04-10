---
title: "Refer&#234;ncia t&#233;cnica do algoritmo de associa&#231;&#227;o da Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parâmetro MINIMUM_ITEMSET_SIZE"
  - "parâmetro MAXIMUM_SUPPORT"
  - "algoritmos de associação [Analysis Services]"
  - "parâmetro MINIMUM_SUPPORT"
  - "parâmetro OPTIMIZED_PREDICTION_COUNT"
  - "associações [Analysis Services]"
  - "parâmetro MAXIMUM_ITEMSET_COUNT"
  - "parâmetro MAXIMUM_ITEMSET_SIZE"
  - "parâmetro MINIMUM_PROBABILITY"
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 24
---
# Refer&#234;ncia t&#233;cnica do algoritmo de associa&#231;&#227;o da Microsoft
  O algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma implementação direta do já conhecido algoritmo Apriori.  
  
 Tanto o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] como o Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] podem ser usados para analisar associações, mas as regras encontradas podem variar conforme o algoritmo. Em um modelo de árvores de decisão, as divisões que levam as regras específicas baseiam-se nas informações obtidas, enquanto no modelo de associação elas se baseiam totalmente na confiança. Assim, em um modelo de associação, um regra forte, ou aquela com mais confiança, não seria necessariamente interessante porque não fornece informações novas.  
  
## Implementação do algoritmo Associação da Microsoft  
 O algoritmo Apriori não analisa padrões, mas gera e, em seguida, conta *conjuntos de itens candidatos*. Um item pode representar um evento, um produto ou o valor de um atributo, dependendo do tipo de dados que está sendo analisado.  
  
 No tipo mais comum de modelo de associação, variáveis Booleanas que representam um valor Sim/Não ou Ausente/Existente são atribuídas a cada atributo, como o nome de um produto ou evento. Uma análise da cesta de compras é um exemplo de modelo de regras de associação que usa variáveis Booleanas para representar a presença ou a ausência de determinados produtos na cesta de compras de um cliente.  
  
 Para cada conjunto de itens, o algoritmo cria pontuações que representam suporte e confiança. Essas pontuações podem ser usadas para classificar e derivar regras interessantes a partir dos conjuntos de itens.  
  
 Também é possível criar modelos de associação para atributos numéricos. Se os atributos forem contínuos, os números poderão ser *discretizados ou* agrupados em buckets. Os valores diferenciados podem ser tratados como Boolianos ou como pares atributo-valor.  
  
### Suporte, probabilidade e importância  
 *Suporte*, que às vezes é conhecido como *frequência*, significa o número de casos que contém o item de destino ou a combinação de itens. Somente os itens que têm, no mínimo, a quantia especificada de suporte podem ser incluídos no modelo.  
  
 Um *conjunto de itens frequente* refere-se a uma coleção de itens na qual a combinação de itens também dá suporte além do limite definido pelo parâmetro MINIMUM_SUPPORT. Por exemplo, se o conjunto de itens for {A,B,C} e o valor de MINIMUM_SUPPORT for 10, cada item A, B e C deve ser encontrado pelo menos em 10 casos para ser incluído no modelo, e a combinação de itens {A,B,C} também deve ser encontrada, no mínimo, em 10 casos.  
  
 **Observação** Você também pode controlar o número de conjuntos de itens em um modelo de mineração especificando o tamanho máximo de um conjunto de itens, sendo que tamanho significa o número de itens.  
  
 Por padrão, o suporte para qualquer item ou conjunto de itens em particular representa uma contagem dos casos que contêm esse item (ou itens). No entanto, também é possível expressar MINIMUM_SUPPORT como uma porcentagem do total de casos no conjunto de dados, basta digitar o número como um valor decimal menor que 1. Por exemplo, se você especificar MINIMUM_SUPPORT com um valor de 0,03, significa que pelo menos 3% do total de casos do conjunto de dados deve conter esse item ou conjunto de itens para inclusão no modelo. Faça testes com seu modelo para determinar se faz mais sentido usar a contagem ou a porcentagem.  
  
 Por outro lado, o limite para regras é expressado não como contagem ou percentual, mas como uma probabilidade, às vezes conhecida como *confiança*. Por exemplo, se o conjunto de itens {A,B,C} ocorrer em 50 casos, mas o conjunto de itens {A,B,D} também ocorrer em 50 casos e o conjunto de itens {A,B} em outros 50 casos, é óbvio que {A,B} não é um forte indicador de {C}. Portanto, para ponderar resultados específicos em relação a todos os resultados conhecidos, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula a probabilidade da regra individual (como If {A,B} Then {C}) dividindo o suporte para o conjunto de itens {A,B,C} pelo suporte de todos os conjuntos de itens relacionados.  
  
 Você pode restringir o número de regras que um modelo produz definindo um valor para MINIMUM_PROBABILITY.  
  
 Para cada regra criada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera uma pontuação que indica sua *importância*, também chamada de *comparação de precisão*. A importância da comparação de precisão é calculada de forma diferente para conjuntos de itens e regras.  
  
 A importância de um conjunto de itens é calculada como sua probabilidade dividida pela probabilidade composta pelos itens individuais do conjunto de itens. Por exemplo, se um conjunto de itens contiver {A,B}, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] primeiro contará todos os casos que contêm essa combinação A e B, dividirá pelo número total de casos e, em seguida, normalizará a probabilidade.  
  
 A importância de uma regra é calculada pela probabilidade do log do lado direito da regra, dado o lado esquerdo da regra. Por exemplo, na regra `If {A} Then {B}`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula a proporção de casos com A e B em relação a casos com B mas sem A e, em seguida, normaliza a proporção usando uma escala logarítmica.  
  
### Seleção de recursos  
 O algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] não executa qualquer tipo de seleção de recursos automática. Em vez disso, ele fornece parâmetros que controlam os dados usados pelo algoritmo. Podem estar incluídos limites para o tamanho de cada conjunto de itens ou a configuração do suporte máximo e mínimo necessário para adicionar um conjunto de itens ao modelo.  
  
-   Para filtrar itens e eventos que são muito comuns e, portanto, desinteressantes, diminua o valor de MAXIMUM_SUPPORT para remover do modelo conjuntos de itens muito frequentes.  
  
-   Para filtrar itens e conjuntos de itens raros, aumente o valor de MINIMUM_SUPPORT.  
  
-   Para filtrar regras, aumente o valor de MINIMUM_PROBABILITY.  
  
## Personalizando o algoritmo Regras de Associação da Microsoft  
 O algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte a vários parâmetros que afetam o comportamento, o desempenho e a precisão do modelo de mineração resultante.  
  
### Definindo parâmetros de algoritmo  
 É possível alterar os parâmetros de um modelo de mineração a qualquer momento com o uso do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Você também pode alterar os parâmetros programaticamente usando a coleção <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> em AMO ou usando o [Elemento dos modelos de mineração &#40;ASSL&#41;](../../analysis-services/scripting/collections/miningmodels-element-assl.md) em XMLA. A tabela a seguir descreve cada parâmetro.  
  
> [!NOTE]  
>  Não é possível alterar os parâmetros de um modelo existente usando uma instrução DMX; você deve especificar os parâmetros na instrução DMX CREATE MODEL ou ALTER STRUCTURE… ADD MODEL ao criar o modelo.  
  
 *MAXIMUM_ITEMSET_COUNT*  
 Especifica o número de máximo de conjuntos de itens que será produzido. Se não for especificado um número, valor padrão será usado.  
  
 O padrão é 200000.  
  
> [!NOTE]  
>  Conjuntos de itens são classificados por suporte. Entre os conjuntos de itens que têm o mesmo suporte, a ordem é arbitrária.  
  
 *MAXIMUM_ITEMSET_SIZE*  
 Especifica o número máximo de itens permitidos em um conjunto de itens. Definir esse valor como 0 especifica que não há limite para o tamanho do conjunto de itens.  
  
 O padrão é 3.  
  
> [!NOTE]  
>  Diminuir esse valor pode reduzir o tempo necessário para a criação do modelo, pois o processamento será interrompido quando o limite for atingindo.  
  
 *MAXIMUM_SUPPORT*  
 Especifica o número máximo de casos que suporta um conjunto de itens. Esse parâmetro pode ser usado para eliminar itens que aparecem frequentemente e, portanto, potencialmente têm pouco significado.  
  
 Se esse valor for menor que 1, o valor representará uma porcentagem do total de casos. Valores maiores do que 1 representam o número absoluto de casos que podem conter o conjunto de itens.  
  
 O padrão é 1.  
  
 *MINIMUM_ITEMSET_SIZE*  
 Especifica o número mínimo de itens permitidos em um conjunto de itens. Se você aumentar esse número, o modelo poderá conter menos conjuntos de itens. Isso pode ser útil, por exemplo, se você quiser ignorar conjuntos de itens com apenas um item.  
  
 O padrão é 1.  
  
> [!NOTE]  
>  Não é possível reduzir o tempo de processamento do modelo diminuindo o valor mínimo, pois o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve calcular probabilidades para itens únicos de qualquer forma como parte do processamento. Contudo, definindo esse valor mais alto você pode filtrar conjuntos de itens menores.  
  
 *MINIMUM_PROBABILITY*  
 Especifica a probabilidade mínima de uma regra ser verdadeira.  
  
 Por exemplo, se você definir esse valor como 0,5, significa que nenhuma regra com menos de cinquenta por cento de probabilidade pode ser gerada.  
  
 O padrão é 0,4.  
  
 *MINIMUM_SUPPORT*  
 Especifica o número mínimo de casos que devem conter o conjunto de itens antes de o algoritmo gerar uma regra.  
  
 Se você definir esse valor como menos que 1, o número mínimo de casos será calculado como uma porcentagem do total de casos.  
  
 Se você definir esse valor como um número inteiro maior que 1, especifica que o número mínimo de casos será calculado como uma contagem de casos que devem conter o conjunto de itens. O algoritmo poderia aumentar automaticamente o valor desse parâmetro se houver limite de memória.  
  
 O padrão é 0,03. Significa que, para ser incluído no modelo, o conjunto de itens deve ser encontrado, no mínimo, em 3% dos casos.  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 Define o número de itens a ser armazenado em cache para otimizar a previsão.  
  
 O valor padrão é 0. Quando o padrão for usado, o algoritmo gerará tantas previsões quantas forem pedidas na consulta.  
  
 Se você especificar um valor diferente de zero para *OPTIMIZED_PREDICTION_COUNT*, as consultas de previsão poderão retornar no máximo o número especificado de itens, mesmo que você solicite mais previsões. No entanto, a definição de um valor pode melhorar o desempenho da previsão.  
  
 Por exemplo, se o valor for definido como 3, o algoritmo armazenará em cache apenas 3 itens para previsão. Não é possível visualizar mais previsões que possam ser igualmente prováveis para os 3 itens retornados.  
  
### Sinalizadores de modelagem  
 Há suporte para os sinalizadores de modelagem a seguir para uso com o algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 NOT NULL  
 Indica que a coluna não pode conter um nulo. Ocorrerá um erro se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontrar um nulo durante o treinamento do modelo.  
  
 Aplica-se à coluna da estrutura de mineração.  
  
 MODEL_EXISTENCE_ONLY  
 Significa que a coluna será tratada como se tivesse dois estados possíveis: **Missing** e **Existing**. Nulo é um valor ausente.  
  
 Aplica-se à coluna do modelo de mineração.  
  
## Requisitos  
 Um modelo de associação deve conter uma coluna de chave, colunas de entrada e uma única coluna previsível.  
  
### Colunas de entrada e colunas previsíveis  
 O algoritmo Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte a colunas de entrada e colunas previsíveis específicas listadas na tabela a seguir. Para obter mais informações sobre o significado de tipos de conteúdo em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Cíclico, discreto, diferenciado, chave, tabela e ordenado|  
|Atributo previsível|Cíclico, Discreto, Diferenciado, Tabela e Ordenado|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## Consulte também  
 [Algoritmo Associação da Microsoft](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Exemplos de consulta de um modelo de associação](../../analysis-services/data-mining/association-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de associação &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  