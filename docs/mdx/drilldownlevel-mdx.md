---
title: DrilldownLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fbab3ea6efe0c1e5b896febeef4d1f38877b8965
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145651"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  Detalha os membros de um conjunto para um nível abaixo do nível mais baixo representado no conjunto.  
  
 Especificando o nível no qual Detalhar é opcional, mas se você definir o nível, você pode usar um **expressão de nível** ou o **nível de índice**. Esses argumentos são mutuamente exclusivos. Finalmente, se houver membros calculados na consulta, você poderá especificar um argumento para incluí-los no conjunto de linhas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Level_Expression*  
 (Opcional). Uma expressão MDX que identifica explicitamente o nível de detalhamento. Se você especificar uma expressão de nível, ignore o argumento de índice abaixo.  
  
 *Index*  
 (Opcional). Uma expressão numérica válida que especifica o número de hierarquia para uma busca detalhada dentro do conjunto. Você pode usar o nível do índice em vez de Level_Expression para identificar explicitamente o nível de detalhamento.  
  
 *Include_Calc_Members*  
 (Opcional). Um sinalizador que indica se deve-se incluir membros calculados, caso existam, no nível de drill down.  
  
## <a name="remarks"></a>Comentários  
 O **DrilldownLevel** função retorna um conjunto de filho membros em ordem hierárquica, com base nos membros incluídos no conjunto especificado. A ordem é preservada entre os membros originais no conjunto especificado, a não ser que todos os membros filho incluídos no conjunto de resultados da função sejam imediatamente incluídos com seu membro pai.  
  
 Dada uma estrutura de dados hierárquica de vários níveis, você pode escolher explicitamente um nível de detalhamento. Há dois modos mutuamente exclusivos para especificar o nível. A primeira abordagem é definir a **level_expression** argumento usando uma expressão MDX que retorna o nível, uma abordagem alternativa é especificar o **índice** argumento, usando uma expressão numérica que Especifica o nível por número.  
  
 Se uma expressão de nível não for especificada, a função construirá um conjunto em ordem hierárquica recuperando os filhos daqueles membros que estão no nível especificado. Se uma expressão de nível for especificada, e não houver nenhum membro neste nível, a expressão de nível será ignorada.  
  
 Se um valor de índice for especificado, a função construirá um conjunto em ordem hierárquica recuperando os filhos daqueles membros que estão no nível mais baixo da hierarquia referenciada no conjunto especificado dado um índice que começa por zero.  
  
 Se não for especificada uma expressão de nível ou um valor de índice, a função construirá um conjunto em ordem hierárquica recuperando os filhos apenas dos membros que estão no nível mais baixo da primeira dimensão referenciada no conjunto especificado.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; ver [propriedades XMLA com suporte &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
## <a name="examples"></a>Exemplos  
 Você pode experimentar usar os seguintes exemplos na janela de consulta MDX do SSMS usando o cubo do Adventure Works.  
  
 **Exemplo 1 – demonstra a sintaxe mínima**  
  
 O primeiro exemplo mostra a sintaxe mínima para **DrilldownLevel**. O único argumento necessário é uma expressão definida. Observe que quando você executa essa consulta, você obtém o pai [todas as categorias] e os membros do próximo nível para baixo: Acessórios, Bicicletas, e assim por diante. Embora esse exemplo seja simple, ele demonstra a finalidade básica da **DrilldownLevel** função, que é detalhar para o próximo nível abaixo.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Exemplo 2 – sintaxe alternativa usando um nível de índice explícito  
  
 Esse exemplo demonstra a sintaxe alternativa, onde o nível do índice é especificado por uma expressão numérica. Nesse caso, o nível do índice é 0. Para um índice iniciado com zero, este é o nível mais baixo.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Note que o conjunto de resultados é idêntico à consulta anterior. Como regra geral, não é necessário definir o nível do índice exceto se desejar efetuar o detalhamento para iniciar em um nível específico. Execute novamente a consulta anterior, definindo o valor do índice para 1 e depois para 2. Com o valor do índice definido para 1, você verá o detalhamento iniciando no segundo nível na hierarquia. Com o valor do índice definido para 2, o detalhamento iniciará no terceiro nível, o nível mais alto neste exemplo. Quanto mais elevada a expressão numérica, maior o nível do índice.  
  
 **Exemplo 3 – demonstra uma expressão de nível**  
  
 O exemplo a seguir mostra como usar a expressão de nível. Dado um conjunto que representa uma estrutura hierárquica, usar uma expressão de nível permite escolher um nível na hierarquia para começar a detalhar.  
  
 Neste exemplo, o nível de detalhamento começa em [Cidade], como o segundo argumento do **DrilldownLevel** função. Ao executar esta consulta, o detalhamento começa pelo nível [Cidade], para os estados de Washington e Oregon. Pela **DrilldownLevel** função, o conjunto de resultados também inclui membros do próximo nível para baixo, [CEP].  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **Exemplo 4 – incluindo membros calculados**  
  
 O último exemplo mostra um membro calculado, que aparece na parte inferior do resultado definido quando você adiciona o **include_calculated_members** sinalizador. Observe que o sinalizador é especificado como quarto parâmetro.  
  
 Esse exemplo funciona porque o membro calculado está no mesmo nível que os membros não calculados. O membro calculado [Costa Oeste] é composto pelos membros de [Estados Unidos], mais todos os membros um nível abaixo de [Estados Unidos].  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 Se você remover apenas o sinalizador e executar novamente a consulta, obterá os mesmos resultados, menos o membro calculado [Costa Oeste].  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
