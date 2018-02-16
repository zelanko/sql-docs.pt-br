---
title: "Membros calculados em subseleções e subcubos | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e35e8f7-ae1c-4549-8432-accf036d2373
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 95a989d092a5b69662fc9f7f542792d9c2895b47
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>Membros calculados em subseleções e subcubos
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Um membro calculado é um membro da dimensão cujo valor é calculado a partir de uma expressão em tempo de execução e pode ser usado em subseleções e subcubos para definir com mais precisão o cubespace de uma consulta.  
  
## <a name="enabling-calculated-members-in-the-subspace"></a>Permissão de membros calculados no subespaço  
 A propriedade de cadeia de conexão **SubQueries** na propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> ou **DBPROPMSMDSUBQUERIES** em [Propriedades XMLA com suporte &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) define o comportamento ou a permissão de membros ou conjuntos calculados em subseleções ou subcubos. No contexto deste documento, subseleção se refere a subseleções e subcubos, exceto quando indicado o contrário.  
  
 A propriedade SubQueries permite os seguintes valores.  
  
|||  
|-|-|  
|Value|Descrição|  
|0|Os membros calculados não são permitidos em subseleções ou subcubos.<br /><br /> Ocorrerá um erro durante a avaliação da subseleção ou do subcubo se um membro calculado for referenciado.|  
|1|Os membros calculados são permitidos em subseleções ou subcubos, mas nenhum membro ascendente é introduzido no subespaço retornando.|  
|2|Os membros calculados são permitidos em subseleções e subcubos, mas nenhum membro ascendente é introduzido no subespaço retornando. Além disso, a granularidade mista é permitida na seleção de membros calculados.|  
  
 O uso de valores de 1 ou 2 na propriedade SubQueries permite que membros calculados sejam usados para filtrar o subespaço retornando de subseleções.  
  
 Um exemplo ajudará a esclarecer o conceito; primeiro, um membro calculado deve ser criado e, em seguida, uma consulta de subseleção é emitida para mostrar o comportamento acima.  
  
 O exemplo a seguir cria um membro calculado que adiciona [Seattle Metro] como uma cidade à hierarquia [Geography].[Geography] no estado de Washington.  
  
 Para executar o exemplo, a cadeia de conexão deve conter a propriedade SubQueries com um valor igual a 1 e todas as instruções MDX devem ser executadas na mesma sessão.  
  
> [!IMPORTANT]  
>  Se você estiver usando o Management Studio para testar as consultas, clique no botão Opções no Gerenciador de Conexão para acessar o painel adicional de propriedades da cadeia de conexão, no qual você pode inserir subqueries= 1 ou 2 afim de permitir membros calculados no subespaço.  
  
 Primeiro emita a seguinte expressão MDX:  
  
```  
  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 Em seguida, emita a consulta MDX a seguir para ver os membros calculados permitidos em subseleções.  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Os resultados obtidos são:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2011|CY 2012|CY 2013|CY 2014|  
|Seattle Metro Agg|$2,383,545.69|1$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 Como já dissemos, os ascendentes de [Seattle Metro] não existem no subespaço retornado, quando SubQueries=1, logo, [Geography].[Geography].allmembers só contém o membro calculado.  
  
 Se o exemplo for executado usando-se SubQueries=2, na cadeia de conexão, os resultados obtidos serão:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|United States|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 Como já dissemos, ao usarem SubQueries=2, os ascendentes de [Seattle Metro] estão no subespaço retornado, mas não há nenhum valor para esses membros porque não existe nenhum membro regular a ser fornecido para as agregações. Por isso, os valores NULL são fornecidos para todos os membros ascendentes do membro calculado desse exemplo.  
  
 Para compreender o comportamento acima, isso ajuda a perceber que os membros calculados não contribuem para as agregações dos pais, como acontece com os membros regulares. No primeiro caso, a filtragem por membros calculados sozinha levará a ascendentes vazios porque não há membro regular que contribua para os valores agregados do subespaço resultante. Se você adicionar membros regulares à expressão de filtragem, os valores agregados virão desses membros regulares. Continuando o exemplo anterior, se as cidades de Portland, em Oregon, e de Spokane, em Washington, forem adicionadas ao mesmo eixo onde o membro calculado é exibido; como mostrado na próxima expressão MDX:  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Os resultados a seguir são obtidos.  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|United States|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 Nos resultados acima, os valores agregados para [All Geographies], [United States], [Oregon] e [Washington] vêm da agregação dos descendentes de &[Portland]&[OR] and &[Spokane]&[WA]. Nada vem do membro calculado.  
  
### <a name="remarks"></a>Comentários  
 Apenas membros globais ou calculados pela sessão são permitidos nas expressões de subseleção ou subcubo. Os membros calculados da consulta na expressão MDX irão gerar um erro quando a expressão de subseleção ou subcubo for avaliada.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Subseleções em consultas](../../../analysis-services/multidimensional-models/mdx/subselects-in-queries.md)   
 [Propriedades XMLA suportadas &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)  
  
  
