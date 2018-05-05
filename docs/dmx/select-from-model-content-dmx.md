---
title: SELECT FROM &lt;modelo&gt;. CONTEÚDO (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
- Content
dev_langs:
- DMX
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- SELECT FROM <model>.CONTENT statement
ms.assetid: a270b33f-77be-41fa-9340-2f6cb0dd75e5
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c68fe4831c0fcbae281eae4ca3ed823d737267cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>SELECT FROM &lt;modelo&gt;. CONTEÚDO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o conjunto de linhas do esquema de modelo de mineração para o modelo de mineração de dados especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Uma lista de colunas separada por vírgula derivada do conjunto de linhas de esquema do Conteúdo.  
  
 *modelo*  
 Identificador de modelo.  
  
 *Expressão de condição*  
 Opcional. Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Remarks  
 O **SELECT FROM**  *\<modelo > * * *. CONTEÚDO** instrução retorna o conteúdo que é específico para cada algoritmo. Por exemplo, talvez você queira usar as descrições de todas as regras de um modelo de regras associado em um aplicativo personalizado. Você pode usar um **SELECT FROM \<modelo >. CONTEÚDO** instrução para retornar valores na coluna NODE_RULE do modelo.  
  
 A tabela a seguir lista as colunas que são incluídas no conteúdo do modelo de mineração.  
  
> [!NOTE]  
>  Os algoritmos podem interpretar as colunas de forma diferente para representar corretamente o conteúdo. Para obter uma descrição do modelo de mineração conteúdo para cada algoritmo e dicas sobre como interpretar e consultar o conteúdo para cada tipo de modelo do modelo de mineração, consulte [conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
|Coluna de conjunto de linhas DE CONTEÚDO|Description|  
|---------------------------|-----------------|  
|MODEL_CATALOG|Nome de um catálogo. NULL se o provedor não oferecer suporte a catálogos.|  
|MODEL_SCHEMA|Nome de um esquema não qualificado. NULL se o provedor não oferecer suporte a esquemas.|  
|MODEL_NAME|Nome de um modelo. Essa coluna não pode conter um NULL.|  
|ATTRIBUTE_NAME|O nome do atributo que corresponde ao nó.|  
|NODE_NAME|O nome do nó.|  
|NODE_UNIQUE_NAME|O nome exclusivo do nó no modelo.|  
|NODE_TYPE|Um número inteiro que representa o tipo do nó. .|  
|NODE_GUID|Nó GUID. NULL se não houver GUID.|  
|NODE_CAPTION|Rótulo ou legenda associada ao nó. Usado principalmente para fins de exibição. Se não houver legenda, NODE_NAME é retornado.|  
|CHILDREN_CARDINALITY|Número de filhos do nó.|  
|PARENT_UNIQUE_NAME|O nome exclusivo do nó pai.|  
|NODE_DESCRIPTION|Uma descrição do nó.|  
|NODE_RULE|Um fragmento XML que representa a regra inserida ao nó. Formato da cadeia de caracteres XML com base no padrão PMML.|  
|MARGINAL_RULE|Um fragmento XML que descreve o caminho do pai para o nó.|  
|NODE_PROBABILITY|A probabilidade do caminho que termina no nó.|  
|MARGINAL_PROBABILITY|A probabilidade de que o nó seja alcançado a partir do nó pai.|  
|NODE_DISTRIBUTION|Uma tabela que contém estatísticas que descrevem a distribuição dos valores no nó.|  
|NODE_SUPPORT|Número de casos que suportam esse nó.|  
  
## <a name="examples"></a>Exemplos  
 O código a seguir retorna a ID do nó pai do modelo de árvores de decisão adicionado à estrutura de mineração de Mala Direta.  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 Resultados esperados:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 A consulta a seguir usa o **IsDescendant** função para retornar os filhos imediatos do nó que foi retornado na consulta anterior.  
  
> [!NOTE]  
>  Como o valor de NODE_NAME é uma cadeia de caracteres, você não pode usar uma instrução Sub-Select para retornar NODE_ID como um argumento para o **IsDescendant** função.  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 Resultados esperados:  
  
 Como o modelo é um modelo de árvores de decisão, os descendentes do nó pai do modelo incluem um único nó de estatísticas marginais, um nó que representa o atributo previsível e vários nós que contêm atributos e valores de entrada. Para obter mais informações, consulte [Mining Model Content for Decision Tree Models &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
## <a name="using-the-flattened-keyword"></a>Usando a palavra-chave FLATTENED  
 O conteúdo de modelo de mineração frequentemente contém informações interessantes sobre o modelo nas colunas da tabela aninhada. A palavra-chave FLATTENED lhe permite recuperar os dados de uma coluna de tabela aninhada sem usar um fornecedor com suporte para conjuntos de linhas hierárquicos.  
  
 A consulta a seguir retorna um único nó, o nó de estatísticas marginais (NODE_TYPE = 26) de um modelo Naïve Bayes. No entanto, este nó contém uma tabela aninhada, na coluna NODE_DISTRIBUTION. Em virtude disso, a coluna de tabela aninhada é bidimensional e uma linha é retornada para cada linha na tabela aninhada. O valor da coluna escalar MODEL_NAME é repetido para cada linha na tabela aninhada.  
  
 Além disso, observe que se você especificar apenas o nome da coluna da tabela aninhada, uma nova coluna será retornada para cada coluna na tabela aninhada. Por padrão, o nome da tabela aninhada é usado como prefixo ao nome de cada coluna de tabela aninhada.  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Resultados do exemplo:  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Ausente|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 O exemplo a seguir demonstra como retornar apenas algumas colunas da tabela aninhada usando uma instrução sub-select. Você pode simplificar a exibição criando o alias do nome da tabela aninhada, como mostrado.  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Resultados do exemplo:  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Ausente|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>Consulte também  
 [SELECIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
