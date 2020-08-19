---
description: Trabalhando com valores vazios
title: Trabalhando com valores vazios | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f497ba1ccf84ac642144340af4d5597d773dcadb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421890"
---
# <a name="working-with-empty-values"></a>Trabalhando com valores vazios


  Um valor vazio indica que um membro específico, tupla ou célula está vazio. Um valor de célula vazio indica que os dados da célula especificada não podem ser encontrados na tabela de fatos subjacente ou que a tupla da célula especificada representar uma combinação de membros que não é aplicável ao cubo.  
  
> [!NOTE]  
>  Embora um valor vazio seja diferente de um valor de zero, um valor vazio geralmente é tratado como zero a maior parte do tempo.  
  
 A consulta a seguir ilustra o comportamento de valores vazio e zero:  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 As informações a seguir se aplicam a valores vazios:  
  
-   A função [IsEmpty](../mdx/isempty-mdx.md) retornará **true** se e somente se a célula identificada pela tupla especificada na função estiver vazia. Caso contrário, a função retornará **false**.  
  
    > [!NOTE]  
    >  A função **IsEmpty** não pode determinar se uma expressão de membro retorna um valor nulo. Para determinar se um membro nulo é retornado de uma expressão, use o operador [is](../mdx/is-mdx.md).  
  
-   Quando o valor de célula vazio for um operando para qualquer um dos operadores numéricos (+, -, *, /), o valor de célula vazio é tratado como zero se o outro operando for um valor não vazio. Se ambos os operandos estiverem vazios, o operador numérico retornará o valor de célula vazio.  
  
-   Quando o valor de célula vazio for um operando para o operador de concatenação de cadeia de caracteres (+), o valor de célula vazio será tratado como zero se o outro operando for um valor não vazio. Se ambos os operandos estiverem vazios, o operador de concatenação de cadeias de caracteres retornará o valor de célula vazio.  
  
-   Quando o valor de célula vazio for um operando para qualquer um dos operadores de comparação (=. <>, >=, \<=, > , <), o valor da célula vazia é tratado como zero ou uma cadeia de caracteres vazia, dependendo se o tipo de dados do outro operando é numérico ou de cadeia de caracteres, respectivamente. Se ambos os operandos estiverem vazios, os operandos serão tratados como zero.  
  
-   Ao agrupar valores numéricos, o valor de célula vazio é agrupado no mesmo local como zero. Entre o valor de célula vazio e zero, vazio é agrupado antes de zero.  
  
-   Ao agrupar valores da cadeia de caracteres, o valor de célula vazio será agrupado no mesmo local como cadeia de caracteres vazia. Entre o valor de célula vazio e a cadeia de caracteres vazia, vazio é agrupado antes de uma cadeia de caracteres vazia.  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>Lidando com valores vazios em cubos e instruções MDX  
 Em instruções MDX (Multidimensional Expressions), você pode procurar valores vazios e, em seguida, executar determinados cálculos em células com dados válidos (ou seja, não vazios). Eliminar valores vazios ao executar cálculos pode ser importante porque determinados cálculos, como uma média, pode ser impreciso se os valores de célula vazios forem incluídos.  
  
 Se forem armazenados valores vazios em seus dados de tabela de fatos subjacentes, por padrão, eles serão convertidos em zeros quando o cubo for processado. Você pode usar a opção de **processamento nulo** em uma medida para controlar se fatos nulos são convertidos em 0, convertidos em um valor vazio ou até mesmo gera um erro durante o processamento. Se você não quiser que valores de célula vazios sejam exibidos nos resultados de consulta, crie consultas, membros calculados ou instruções de script MDX que eliminam os valores vazios ou os substitua por algum outro valor.  
  
 Para remover linhas ou colunas vazias de uma consulta, você pode usar a instrução NON EMPTY antes da definição de conjunto de eixos. Por exemplo, a consulta a seguir retorna somente a Categoria de Produto Bicicletas porque esta é a única categoria que foi vendida no Ano Fiscal de 2001:  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 Geralmente, para remover tuplas vazias de um conjunto, você pode usar a função NonEmpty. A consulta a seguir mostra duas medidas calculadas, uma das quais conta o número de Categorias de Produto e a segunda mostra o número de Categorias de Produto que têm valores para a medida [Valor do Imposto da Internet] e o Ano Fiscal de 2001:  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 Para obter mais informações, consulte [&#41;MDX &#40;não vazia ](../mdx/nonempty-mdx.md).  
  
## <a name="empty-values-and-comparison-operators"></a>Valores vazios e operadores de comparação  
 Quando valores vazios estão presentes em dados, os operadores lógicos e de comparação podem potencialmente retornar um terceiro resultado EMPTY em vez de somente TRUE ou FALSE. Essa necessidade de lógica com valor três é uma fonte de muitos erros de aplicativo. Essas tabelas destacam o efeito de introduzir comparações de valores vazios.  
  
 A tabela a seguir mostra os resultados de se aplicar um operador AND a dois operandos boolianos.  
  
|AND|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**TRUE**|TRUE|FALSE|FALSE|  
|**ESVAZIÁ**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 Esta tabela mostra os resultados de se aplicar um operador OR a dois operandos boolianos.  
  
|OU|TRUE|FALSE|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**ESVAZIÁ**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 Esta tabela mostra como o operador NOT nega ou reverte o resultado de um operador booliano.  
  
|Expressão booliana para a qual o operador NOT é aplicado|Avaliada como|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)   
 [Expressões &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
