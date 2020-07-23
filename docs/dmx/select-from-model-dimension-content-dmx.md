---
title: Selecione do &lt; modelo &gt; . DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d16b8b01251be6703350a1a64bb9cdd2bdc5cadb
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970584"
---
# <a name="select-from-ltmodelgtdimension_content-dmx"></a>Selecione do &lt; modelo &gt; . DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Um modelo de mineração pode ser usado como uma dimensão em um cubo OLAP, onde cada nó do modelo é representado como um membro da dimensão. **A seleção de \<model> . Dimension_CONTENT** instrução retorna o conteúdo do modelo que pertence ao seu uso como uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Lista de identificadores, separada por vírgulas, de colunas ou expressões relacionadas derivadas do conteúdo do conjunto de linhas do esquema.  
  
 *modelo*  
 Identificador de modelo.  
  
 *expressão de condição*  
 Opcional. Uma condição para restringir os valores retornados da lista de colunas.  
  
 *expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Provedores de algoritmo definem qual conteúdo é retornado e como organizar isto. Por exemplo, o provedor poderia limitar o número de nós que são descritos no conteúdo de dimensão.  
  
 A tabela a seguir lista as colunas que podem ser consultadas para o conteúdo de dimensão e a função que cada coluna executa como dimensão de mineração de dados.  
  
|Coluna de conjunto de linhas DE CONTEÚDO|Função em dimensão de mineração de dados|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|Propriedade do membro.|  
|NODE_NAME|Propriedade do membro.|  
|NODE_UNIQUE_NAME|Atributo de chave.|  
|NODE_TYPE|Propriedade do membro.|  
|NODE_CAPTION|CaptionColumn para o atributo de **chave** .|  
|CHILDREN_CARDINALITY|Propriedade do membro.|  
|PARENT_UNIQUE_NAME|RelatedAttribute para o atributo de **chave** (ParentAttribute na hierarquia pai-filho).|  
|NODE_DESCRIPTION|Propriedade do membro.|  
|NODE_RULE|Propriedade do membro.|  
|MARGINAL_RULE|Propriedade do membro.|  
|NODE_PROBABILITY|Propriedade do membro.|  
|MARGINAL_PROBABILITY|Propriedade do membro.|  
|NODE_SUPPORT|Propriedade do membro.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Descrição  
 O exemplo seleciona todas as colunas do conteúdo do modelo `[TM Decision Tree]` que pertencem a uso do modelo como uma dimensão.  
  
### <a name="code"></a>Código  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SELECIONAR&#41;&#40;DMX](../dmx/select-dmx.md)   
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
