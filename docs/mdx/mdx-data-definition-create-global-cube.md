---
title: "Instrução CREATE GLOBAL CUBE (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GLOBAL CUBE
- CUBE
- GLOBAL
- CREATE
- CREATE GLOBAL
- CREATE GLOBAL CUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CREATE GLOBAL CUBE
- CREATE GLOBAL CUBE
ms.assetid: b46f3c98-a4f1-4ebb-915f-a3333f4054dc
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b9a80a053d9666ca2e8c63eb6037dddf3cf4a7a5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-global-cube"></a>Definição de dados MDX - criar cubo GLOBAL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria e popula um cubo localmente persistente, com base em um subcubo a partir de um cubo no servidor. Uma conexão com o servidor não é exigida para a conexão com o cubo localmente persistente. Para obter mais informações sobre cubos locais, consulte [cubos locais &#40; Analysis Services - dados multidimensionais &#41; ](../analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
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
 local_cube_name  
 O nome do cubo local.  
  
 'Cube_Location'  
 O nome e caminho para o cubo localmente persistente.  
  
 source_cube_name  
 O nome do cubo no qual o cubo local se baseia.  
  
 source_cube_name.measure_name  
 O nome totalmente qualificado da medida de origem incluída no cubo local. Membros calculados da dimensão de Medidas não são permitidos.  
  
 measure_name  
 O nome da medida no cubo local.  
  
 source_cube_name.dimension_name  
 O nome totalmente qualificado da dimensão de origem a serem incluída no cubo local.  
  
 dimension_name  
 O nome da dimensão no cubo local.  
  
 DE \<dim cláusula from >  
 Especificação válida somente para definição de dimensão derivada.  
  
 NOT_RELATED_TO_FACTS  
 Especificação válida somente para definição de dimensão derivada.  
  
 \<tipo de nível >  
 Especificação válida somente para definição de dimensão derivada.  
  
## <a name="remarks"></a>Comentários  
 Um cubo local é definedin termos as medidas e definições que definem-lo. Há dois tipos de dimensões:  
  
-   Dimensões de origem – São dimensões que faziam parte de um dentre mais cubos de origem.  
  
-   Dimensões derivadas – São dimensões que fornecem capacidades de análise novas. Uma dimensão derivada pode ser uma dimensão comum definida com base em uma dimensão de origem dividida vertical ou horizontalmente ou que contenha agrupamento personalizado de membros de dimensão. Uma dimensão derivada também pode ser uma dimensão de mineração de dados com base em um modelo de mineração de dados.  
  
> [!NOTE]  
>  A palavra-chave Dimensão pode se referir a dimensões ou hierarquias.  
  
 Em um cubo local, é possível executar as seguintes tarefas:  
  
-   Eliminar dimensões que existem no cubo de origem  
  
-   Adicionar ou eliminar hierarquias a partir de uma dimensão.  
  
-   Eliminar grupos de medidas ou medidas específicas  
  
 A instrução CREATE GLOBAL CUBE segue as seguintes regras:  
  
-   A instrução CREATE GLOBAL CUBE copia automaticamente para o cubo local todos os comandos, como medidas calculadas ou ações. Se um comando tiver uma linguagem MDX que faça referências explícitas ao cubo pai, o cubo local não poderá executar aquele comando. Para evitar esse problema, use o **CURRENTCUBE** palavra-chave na definição de expressões MDX para comandos. O **CURRENTCUBE** palavra-chave usa o contexto de cubo atual ao fazer referência a um cubo dentro de uma expressão MDX.  
  
-   Um cubo global, criado a partir de um cubo global existente em um arquivo de cubo local, não pode ser salvo no mesmo arquivo de cubo local. Por exemplo, você cria um cubo global chamado SalesLocal1 e salva esse cubo no arquivo C:\\SalesLocal.cub. É feita, então, a conexão com o arquivo C:\\SalesLocal.cub e cria-se um segundo cubo global chamado SalesLocal2. Caso tente salvar agora o cubo global SalesLocal2 no arquivo C:\\SalesLocal.cub, você receberá uma mensagem de erro. Porém, é possível salvar o cubo global SalesLocal2 em um arquivo de cubo local diferente.  
  
-   Cubos globais não dão suporte a medidas de contagem distintas. Como os cubos que incluem medidas de contagem distintas são não aditivos, a instrução CREATE GLOBAL CUBE não dá suporte à criação ou ao uso de medidas de contagem distintas.  
  
-   Ao adicionar uma medida a um cubo local, deve-se incluir também pelo menos uma dimensão relacionada à medida que está sendo adicionada.  
  
-   Ao adicionar uma hierarquia pai-filho a um cubo local, níveis e filtros de uma hierarquia pai-filho são ignorados e toda a hierarquia pai-filho é incluída.  
  
-   Propriedades de membro não têm suporte em cubos locais.  
  
-   Não é possível criar um cubo local a partir de uma perspectiva.  
  
-   Quando se inclui uma medida semiaditiva a um cubo local, as seguintes regras são aplicadas:  
  
    -   Deve-se incluir a dimensão de Contas se a propriedade AggregateFunction para a medida que é adicionada for ByAccount.  
  
    -   Deve-se incluir a dimensão Temporal inteira se a medida de propriedade AggregateFunction que é adicionada for FirstChild, LastChild, FirstNonEmpty, LastNonEmpty ou AverageOfChildren.  
  
-   Não é possível adicionar dimensões de mineração de dados a um cubo local.  
  
-   Dimensões de referência são materializadas e adicionadas como dimensões comuns.  
  
-   Quando uma dimensão muitos para muitos é incluída, as seguintes regras são aplicadas:  
  
    -   Deve-se adicionar toda a dimensão muitos para muitos.  
  
    -   Deve-se adicionar o grupo de medidas intermediário.  
  
    -   Deve-se adicionar as dimensões como um todo, comuns aos dois grupos de medidas envolvidos na relação muitos para muitos.  
  
 O exemplo a seguir demonstra a criação de uma versão local persistente do cubo Adventure Works que contém somente a medida Valor das Vendas do Revendedor, a dimensão Revendedor e a dimensão Data.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 O exemplo a seguir demonstra a divisão quando se cria um cubo local. O cubo global criado tem como base o cubo Adventure Works, dividido verticalmente pelo membro do nível de Ano fiscal de 2005, e horizontalmente pelos níveis de Ano fiscal e Mês.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [Criar instrução de cubo de sessão &#40; MDX &#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  

