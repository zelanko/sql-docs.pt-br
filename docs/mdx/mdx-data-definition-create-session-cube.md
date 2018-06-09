---
title: Instrução CREATE SESSION CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09e093b46127090d232f023a7c7277c398ec349c
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742465"
---
# <a name="mdx-data-definition---create-session-cube"></a>Definição de dados MDX - criar o cubo de sessão


  Cria e popula um cubo de sessão a partir de um cubo de servidor existente. O cubo de sessão só é visível dentro da sessão atual; ele não pode ser pesquisado ou consultado a partir de outra sessão. O cubo de sessão é excluído implicitamente quando a sessão é fechada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN  
  
```  
  
## <a name="syntax-elements"></a>Elementos de sintaxe  
 session_cube_name  
 O nome do cubo de sessão.  
  
 source_cube_name  
 O nome do cubo no qual o cubo de sessão se baseia.  
  
 source_cube_name.measure_name  
 O nome totalmente qualificado da medida de origem que está sendo incluído no cubo de sessão. Membros calculados da dimensão de Medidas não são permitidos.  
  
 measure_name  
 O nome da medida no cubo de sessão.  
  
 source_cube_name.dimension_name  
 O nome totalmente qualificado da dimensão de origem a serem incluída no cubo de sessão.  
  
 dimension_name  
 O nome da dimensão no cubo de sessão.  
  
 DE \<dim cláusula from >  
 Especificação válida somente para definição de dimensão derivada.  
  
 NOT_RELATED_TO_FACTS  
 Especificação válida somente para definição de dimensão derivada.  
  
 \<tipo de nível >  
 Especificação válida somente para definição de dimensão derivada.  
  
## <a name="remarks"></a>Remarks  
 Ao contrário do servidor e de cubos locais, um cubo de sessão não persiste além da sessão que criou o cubo de sessão. Um cubo de sessão é definido de acordo com as medidas e definições que o definem. Há dois tipos de dimensões:  
  
-   Dimensões de origem – são dimensões que faziam parte de um de mais cubos de origem.  
  
-   Dimensões derivadas – São dimensões que fornecem capacidades de análise novas. Uma dimensão derivada pode ser uma dimensão comum definida com base em uma dimensão de origem dividida vertical ou horizontalmente ou que contenha agrupamento personalizado de membros de dimensão. Uma dimensão derivada também pode ser uma dimensão de mineração de dados com base em um modelo de mineração de dados.  
  
> [!NOTE]  
>  A palavra-chave Dimensão pode se referir a dimensões ou hierarquias.  
  
 Cubos de sessão são usados principalmente para agrupamento dinâmico de membros de atributo em grupos de membros personalizados por aplicativos cliente, como Microsoft Excel. Em um cubo de sessão, você pode executar as seguintes tarefas:  
  
-   Eliminar dimensões que existem no cubo de origem.  
  
-   Adicionar ou eliminar hierarquias de uma dimensão.  
  
-   Eliminar grupos de medidas ou medidas específicas.  
  
-   Adicionar um novo atributo, com base em associação de atributo, para criar grupos em relação a um atributo existente.  
  
> [!IMPORTANT]  
>  A segurança em objetos de cubo de sessão é herdada dos objetos de origem subjacentes. Outros objetos, como ações e scripts de cálculo, também são herdados pelo cubo de sessão.  
  
 A instrução CREATE SESSION CUBE segue as seguintes regras:  
  
-   Não é possível executar agrupamento em hierarquias pai-filho.  
  
-   Não é possível executar agrupamento em dimensões ROLAP.  
  
-   Não é possível executar agrupamento em dimensões vinculadas.  
  
-   Não é possível executar agrupamento em níveis com rollups personalizados.  
  
-   Não é possível executar agrupamento em hierarquias de atributo diferenciado.  
  
-   Não é possível executar agrupamento em hierarquias não naturais, que são hierarquias do tipo um para muitos entre níveis (como idade e sexo).  
  
-   Referências explícitas a um nome de cubo em script MDX são desfeitas por agrupamento porque o cubo de sessão tem um nome diferente. Use então a palavra-chave CURRENTCUBE.  
  
-   Não é possível executar agrupamento em dimensões com membros-padrão explícitos.  
  
-   Ao executar agrupamento, são ignorados membros calculados no escopo da sessão no cubo de servidor original.  
  
-   Ao executar agrupamento em uma dimensão do cubo em um cubo de servidor, o agrupamento afeta todas as dimensões do cubo que se baseiam na mesma dimensão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra a criação de uma versão do escopo de uma sessão do cubo Adventure Works que contém a medida do Valor das Vendas do Revendedor, a dimensão Revendedor, a dimensão Produto, a dimensão Geografia e a dimensão Data. Dentro desse cubo de sessão, são criados dois grupos; um grupo contém países na Europa e outro contém grupos na América do Norte. Essa amostra é uma versão simplificada de uma instrução CREATE SESSION CUBE emitida pelo Microsoft Excel quando um usuário cria um agrupamento personalizado de membros.  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [Instrução CREATE GLOBAL CUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
