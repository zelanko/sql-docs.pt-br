---
title: Instrução CREATE MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 432438fe9a6e1b39c849188050b67f816d895187
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250205"
---
# <a name="mdx-data-definition---create-member"></a>Definição de dados MDX – CREATE MEMBER


  Cria um membro calculado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cubo onde o membro será criado.  
  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de membro. Especifica um nome completamente qualificado para criar um membro dentro de uma dimensão diferente da dimensão de Medidas. Se um nome de membro completamente qualificado não for fornecido, o membro será criado na dimensão de Medidas.  
  
 *MDX_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida.  
  
 *Property_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma propriedade de membro calculado.  
  
 *Property_Value*  
 Uma expressão escalar válida que define o valor de propriedade do membro calculado.  
  
## <a name="remarks"></a>Comentários  
 A instrução CREATE MEMBRO define membros calculados disponíveis ao longo da sessão e que, então, podem ser usados em várias consultas durante a sessão. Para obter mais informações, consulte [membros calculados do criando &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 Também é possível definir um membro calculado para ser usado por uma consulta única. Para definir um membro calculado limitado a uma consulta única, use a cláusula WITH na instrução SELECT. Para obter mais informações, consulte [membros calculados do criando &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 *Property_Name* pode se referir a propriedades de qualquer um dos membro calculado padrão ou opcionais. Propriedades do membro padrão são listadas neste tópico. Membros calculados criados com CREATE MEMBER sem um **sessão** valor têm o escopo de sessão. Além disso, cadeias de caracteres dentro de definições de membros calculados são delimitadas entre aspas duplas. Isso é diferente do método definido por OLE DB que especifica quais cadeias de caracteres devem ser delimitadas por aspas simples.  
  
 A especificação de um cubo diferente daquele conectado no momento causa um erro. Portanto, deve-se usar CURRENTCUBE no lugar de um nome de cubo para indicar o cubo atual.  
  
 Para obter mais informações sobre propriedades do membro definidas por OLE DB, consulte a documentação OLE DB.  
  
## <a name="scope"></a>Scope  
 Um membro calculado pode acontecer dentro de um dos escopos listados na tabela a seguir.  
  
 Escopo de consulta  
 A visibilidade e o tempo de vida do membro calculado estão limitados à consulta. O membro calculado é definido em uma consulta individual. Escopo de consulta substitui escopo de sessão. Para obter mais informações, consulte [membros calculados do criando &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 Escopo de sessão  
 A visibilidade e o tempo de vida do membro calculado estão limitados à sessão em que são criados. (O tempo de vida é menor que a duração da sessão se uma instrução DROP MEMBER for emitida no membro calculado.) A instrução CREATE MEMBER cria um membro calculado com escopo de sessão.  
  
### <a name="scope-isolation"></a>Isolamento de escopo  
 Quando um script de cubo de linguagem MDX contém membros calculados, por padrão os membros calculados são resolvidos antes que quaisquer cálculos no escopo da sessão sejam resolvidos e antes que quaisquer cálculos definidos em consulta sejam resolvidos.  
  
> [!NOTE]  
>  Em determinados cenários, o [agregada (MDX)](../mdx/aggregate-mdx.md) função e o [VisualTotals (MDX)](../mdx/visualtotals-mdx.md) função não apresentam esse comportamento.  
  
 O comportamento permite aos aplicativos cliente genéricos trabalhar com cubos que contenham cálculos complexos, sem ter de levar em conta a implementação específica dos cálculos. No entanto, em determinados cenários, convém executar a sessão ou os de membros calculados no escopo da consulta antes de determinados cálculos no cubo e nem o **agregada** função nem a **VisualTotals** função são aplicáveis. Para isso, use a propriedade de cálculo SCOPE_ISOLATION.  
  
#### <a name="example"></a>Exemplo  
 O script a seguir é um exemplo de um cenário em que a propriedade de cálculo SCOPE_ISOLATION é exigida para produzir o resultado correto.  
  
 **Script MDX do cubo:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **Consulta MDX:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 O resultado desejado da consulta anterior é a razão de vendas para os EUA sem WA, para armazenar custo para os EUA sem WA. A consulta anterior não retorna o resultado desejado; retorna a razão dos EUA menos a razão de WA que é um resultado sem-sentido. Para alcançar o resultado desejado, é possível usar a propriedade de cálculo SCOPE_ISOLATION.  
  
 **Consulta MDX usando a propriedade de cálculo SCOPE_ISOLATION:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>Propriedades padrão  
 Cada membro calculado tem um conjunto de propriedades padrão. Quando um aplicativo cliente está conectado a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], as propriedades padrão são suportadas ou disponível para receber suporte, como o administrador escolhe.  
  
 Propriedades de membro adicionais podem estar disponíveis, dependendo da definição de cubo. As propriedades a seguir representam informações pertinentes ao nível de dimensão no cubo.  
  
|Identificador de propriedade|Significado|  
|-------------------------|-------------|  
|SOLVE_ORDER|A ordem na qual o membro calculado será resolvido quando um membro calculado fizer referência a outro membro calculado (ou seja, quando membros calculados se cruzarem).|  
|FORMAT_STRING|Uma cadeia de formato de estilo Office que o aplicativo cliente pode usar ao exibir valores de célula.|  
|VISIBLE|Um valor que indica se o membro calculado é visível em um conjunto de linhas de esquema. Calculados visíveis membros podem ser adicionados a um conjunto com o [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) função. Um valor diferente de zero indica que o membro calculado é visível. O valor padrão desta propriedade é *Visible*.<br /><br /> Membros calculados que não são visíveis (em que o valor é definido como zero) são em geral usados como etapas intermediárias em membros calculados mais complexos. Esses membros calculados também podem ser consultados por outros tipos de membros, como medidas.|  
|NON_EMPTY_BEHAVIOR|A medida ou o conjunto usado para determinar o comportamento de membros calculados ao resolver células vazias.<br /><br /> **\*\* Aviso \* \***  essa propriedade foi preterida. Evite configurá-la. Consulte [Recursos do Analysis Services preteridos no SQL Server 2016](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) para ver detalhes.|  
|CAPTION|Uma cadeia de caracteres que o aplicativo cliente usa como legenda para o membro.|  
|DISPLAY_FOLDER|Uma cadeia de caracteres que identifica o caminho da pasta de exibição que o aplicativo cliente usa para mostrar o membro. O separador de nível de pasta é definido pelo aplicativo cliente. Para as ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a barra invertida (\\) é o separador de nível. Para fornecer várias pastas de exibição para um membro definido, use um ponto-e-vírgula (;) para separar as pastas.|  
|ASSOCIATED_MEASURE_GROUP|O nome do grupo de medidas ao qual esse membro está associado.|  
  
## <a name="see-also"></a>Consulte também  
 [Instrução de membro DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [Declaração de membro de UPDATE &#40;MDX&#41;](../mdx/mdx-data-definition-update-member.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
