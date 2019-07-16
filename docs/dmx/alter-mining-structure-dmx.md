---
title: ALTERAR A ESTRUTURA DE MINERAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 487fb5c04d623f2a4ef408cf35784dd57b067f4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913846"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria um novo modelo de mineração baseado em uma estrutura de mineração existente.  Quando você usa o **ALTER MINING STRUCTURE** instrução para criar um novo modelo de mineração, a estrutura já deve existir. Por outro lado, quando você usa a instrução [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), você cria um modelo e gerar automaticamente sua estrutura de mineração subjacente ao mesmo tempo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura*  
 O nome da estrutura de mineração à qual o modelo de mineração será adicionado.  
  
 *modelo*  
 Um nome exclusivo para o modelo de mineração.  
  
 *lista de definições de coluna*  
 Uma lista de definições de coluna separadas por vírgulas.  
  
 *lista de definições de coluna aninhada*  
 Uma lista de colunas de uma tabela aninhada separadas por vírgulas, se aplicável.  
  
 *critérios de filtro aninhado*  
 Uma expressão de filtro que é aplicada às colunas em uma tabela aninhada.  
  
 *algoritmo*  
 O nome de um algoritmo de mineração de dados, conforme definido pelo provedor.  
  
> [!NOTE]  
>  Uma lista dos algoritmos suportados pelo provedor atual pode ser recuperada por meio [conjunto de linhas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Para exibir os algoritmos suportados na instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [propriedades de Data Mining](../analysis-services/server-properties/data-mining-properties.md).  
  
 *lista de parâmetros*  
 Opcional. Uma lista separada por vírgulas de parâmetros definidos pelo provedor para o algoritmo.  
  
 *critérios de filtro*  
 Uma expressão de filtro que é aplicada às colunas na tabela de casos.  
  
## <a name="remarks"></a>Comentários  
 Se a estrutura de mineração contiver chaves compostas, o modelo de mineração deve incluir todas as colunas de chave definidas na estrutura.  
  
 Se o modelo não precisar de uma coluna previsível, por exemplo, os modelos criados com o [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering e com algoritmos MSC ([!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering), não será necessário incluir uma definição de coluna na instrução. Todos os atributos no modelo resultante serão tratados como entradas.  
  
 No **WITH** cláusula aplica-se a tabela de casos, você pode especificar opções de filtragem e detalhamento:  
  
-   Adicione a **filtro** palavra-chave e uma condição de filtro. O filtro se aplica aos casos no modelo de mineração.  
  
-   Adicione a **DETALHAMENTO** palavra-chave para permitir que os usuários do modelo de mineração fazer uma busca detalhada dos resultados do modelo de dados do caso. Em DMX, o detalhamento pode ser habilitado somente quando você cria o modelo.  
  
 Para usar maiusculas filtragem e detalhamento, você combinar as palavras-chave em uma única **WITH** cláusula usando a sintaxe mostrada no exemplo a seguir:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Lista de definições de coluna  
 Para definir a estrutura de um modelo, especifique uma lista de definições de coluna que inclua as seguintes informações para cada coluna:  
  
-   Nome (obrigatório)  
  
-   Alias (opcional)  
  
-   Sinalizadores de modelagem  
  
-   Solicitação de previsão, que indica ao algoritmo se a coluna contém um valor previsível, indicado pelo **PREDICT** ou **PREDICT_ONLY** cláusula  
  
 Use a seguinte sintaxe para obter a lista de definições de coluna para definir uma única coluna:  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Nome e alias de coluna  
 O nome de coluna usado na lista de definições de coluna deve ser o mesmo nome da coluna usado na estrutura de mineração. No entanto, você pode definir um alias, se desejar, para representar a coluna de estrutura no modelo de mineração. Também é possível criar várias definições para a mesma coluna de estrutura e atribuir uma utilização de alias e previsão diferente para cada cópia da coluna. Por padrão, o nome de coluna de estrutura será usado se você não definir um alias. Para obter mais informações, consulte [criar um Alias para uma coluna de modelo](../analysis-services/data-mining/create-an-alias-for-a-model-column.md).  
  
 Para colunas de tabela aninhada, especifique o nome da tabela aninhada, especifique o tipo de dados como **tabela**e, em seguida, forneça a lista de colunas aninhadas para incluir no modelo, entre parênteses.  
  
 Você pode definir uma expressão de filtro aplicável à tabela aninhada afixando uma expressão de critério de filtro depois da definição de coluna da tabela aninhada.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte aos seguintes sinalizadores de modelagem a serem usados em colunas de modelo de mineração:  
  
> [!NOTE]  
>  O sinalizador de modelagem NOT_NULL se aplica à coluna de estrutura de mineração. Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Termo|Definição|  
|**REGRESSOR**|Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão.|  
|**MODEL_EXISTENCE_ONLY**|Indica que os valores da coluna de atributo são menos importantes que a presença do atributo.|  
  
 É possível definir diversos sinalizadores de modelagem para uma coluna. Para obter mais informações sobre como usar sinalizadores de modelagem, consulte [sinalizadores de modelagem &#40;DMX&#41;](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Cláusula de previsão  
 A cláusula de previsão descreve como a coluna de previsão é usada. A tabela seguinte lista as possíveis cláusulas.  
  
|||  
|-|-|  
|**PREDICT**|Esta coluna pode ser prevista pelo modelo e seus valores podem ser usados como entrada para prever o valor de outras colunas de previsão.|  
|**PREDICT_ONLY**|Esta coluna pode ser prevista pelo modelo, mas seus valores não podem ser usados em casos de entrada para prever o valor de outras colunas de previsão.|  
  
## <a name="filter-criteria-expressions"></a>Expressões de critérios de filtro  
 Você pode definir um filtro que restringe os casos que são usados no modelo de mineração. O filtro pode ser aplicado a colunas na tabela de casos, a linhas na tabela aninhada ou a ambas.  
  
 As expressões de critérios de filtro são predicados DMX simplificados, similares à cláusula WHERE. As expressões de filtro são restritas a fórmulas que usam operadores matemáticos básicos, escalares e nomes de coluna. A exceção é o operador EXISTS, avaliado como true se pelo menos uma linha for retornada para a subconsulta. Predicados podem ser combinados usando os operadores lógicos comuns: AND, OR e não.  
  
 Para obter mais informações sobre os filtros usados com modelos de mineração, consulte [filtros para modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  As colunas em um filtro devem ser colunas de estrutura de mineração. Não é possível criar um filtro em uma coluna de modelo ou com alias.  
  
 Para obter mais informações sobre operadores e sintaxe DMX, consulte [colunas do modelo de mineração](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="parameter-definition-list"></a>Lista de definições de parâmetro  
 Você pode ajustar o desempenho e a funcionalidade de um modelo adicionando parâmetros de algoritmo à lista de parâmetros. Os parâmetros que podem ser usados dependem do algoritmo especificado na cláusula USING. Para obter uma lista de parâmetros que estão associados com cada algoritmo, consulte [algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 A sintaxe da lista de parâmetros é a seguinte:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Exemplo 1: Adicionar um modelo a uma estrutura  
 O exemplo a seguir adiciona um modelo de mineração Naive Bayes para o **novo envio** estrutura de mineração e limites que o número máximo de atributo estados como 50.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Exemplo 2: Adicionar um modelo filtrado a uma estrutura  
 O exemplo a seguir adiciona um modelo de mineração `Naive Bayes Women`, para o **novo envio** estrutura de mineração. O novo modelo tem a mesma estrutura básica do modelo de mineração adicionado no exemplo 1; no entanto, esse modelo restringe os casos da estrutura de mineração às consumidoras com mais de 50 anos.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Exemplo 3: Adicionar um modelo filtrado a uma estrutura com uma tabela aninhada  
 O exemplo a seguir adiciona um modelo de mineração a uma versão modificada da estrutura de mineração de market basket. A estrutura de mineração usada no exemplo foi modificada para adicionar um **região** coluna, que contém os atributos para a região do cliente, e um **Incomegroup** coluna, que classifica a renda do cliente usando o os valores **alta**, **moderado**, ou **baixa**.  
  
 A estrutura de mineração também inclui uma tabela aninhada que lista os itens que o cliente comprou.  
  
 Como a estrutura de mineração contém uma tabela aninhada, você pode definir um filtro na tabela de casos, na tabela aninhada ou em ambas. Esse exemplo combina um filtro de caso e um filtro de linha aninhada para restringir os casos aos consumidores europeus ricos que compraram um dos modelos de pneu.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
