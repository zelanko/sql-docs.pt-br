---
title: SELECT FROM &lt;modelo&gt;. DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29f730f0bdff985ffceb849c429e5d1b02f70d5f
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842519"
---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM &lt;modelo&gt;. DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Um modelo de mineração pode ser usado como uma dimensão em um cubo OLAP, onde cada nó do modelo é representado como um membro da dimensão. **SELECT FROM \<modelo >. Dimension_CONTENT** instrução retorna o conteúdo do modelo que pertence ao seu uso como uma dimensão.  
  
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
  
 *Expressão de condição*  
 Opcional. Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Remarks  
 Provedores de algoritmo definem qual conteúdo é retornado e como organizar isto. Por exemplo, o provedor poderia limitar o número de nós que são descritos no conteúdo de dimensão.  
  
 A tabela a seguir lista as colunas que podem ser consultadas para o conteúdo de dimensão e a função que cada coluna executa como dimensão de mineração de dados.  
  
|Coluna de conjunto de linhas DE CONTEÚDO|Função em dimensão de mineração de dados|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|Propriedade do membro.|  
|NODE_NAME|Propriedade do membro.|  
|NODE_UNIQUE_NAME|Atributo de chave.|  
|NODE_TYPE|Propriedade do membro.|  
|NODE_CAPTION|CaptionColumn para **chave** atributo.|  
|CHILDREN_CARDINALITY|Propriedade do membro.|  
|PARENT_UNIQUE_NAME|RelatedAttribute para **chave** atributo (ParentAttribute em hierarquia pai-filho).|  
|NODE_DESCRIPTION|Propriedade do membro.|  
|NODE_RULE|Propriedade do membro.|  
|MARGINAL_RULE|Propriedade do membro.|  
|NODE_PROBABILITY|Propriedade do membro.|  
|MARGINAL_PROBABILITY|Propriedade do membro.|  
|NODE_SUPPORT|Propriedade do membro.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo seleciona todas as colunas do conteúdo do modelo `[TM Decision Tree]` que pertencem a uso do modelo como uma dimensão.  
  
### <a name="code"></a>Código  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>Consulte também  
 [SELECIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
