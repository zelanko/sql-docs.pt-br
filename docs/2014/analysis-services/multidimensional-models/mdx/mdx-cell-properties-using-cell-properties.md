---
title: Usando propriedades da célula (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a8b302391eb4e7384a54181b102f4ae8f3de522
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417747"
---
# <a name="using-cell-properties-mdx"></a>Usando propriedades da célula (MDX)
  As propriedades de célula em expressões multidimensionais (MDX) contêm informações sobre o conteúdo e o formato das células de uma fonte de dados multidimensional, como um cubo.  
  
 A linguagem MDX aceita a palavra-chave CELL PROPERTIES em uma instrução MDX SELECT para recuperar propriedades de célula intrínsecas. As propriedades de célula intrínsecas são usadas geralmente para auxiliar na apresentação visual dos dados da célula.  
  
## <a name="cell-properties-keyword-syntax"></a>Sintaxe da palavra-chave CELL PROPERTIES  
 Use a sintaxe a seguir para a palavra-chave `CELL PROPERTIES` da instrução MDX `SELECT`:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 A sintaxe a seguir mostra o formato do valor `<cell_props>` e como ele utiliza a palavra-chave `CELL PROPERTIES` com uma ou mais das propriedades de célula intrínsecas:  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>Propriedades de célula intrínsecas suportadas  
 A tabela a seguir lista as propriedades de célula intrínsecas suportadas que são usadas no valor `<property>` .  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`ACTION_TYPE`|Um bitmask que indica quais tipos de ações existem na célula. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> Observação: Ações de detalhamento não são incluídas nas consultas que contêm um conjunto na cláusula where.|  
|**BACK_COLOR**|A cor do plano de fundo por exibir a propriedade `VALUE` ou `FORMATTED_VALUE`. Para obter mais informações, consulte [Conteúdo de FORE_COLOR e BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`CELL_ORDINAL`|O número ordinal da célula no conjunto de dados.|  
|**FONT_FLAGS**|O bitmask que detalha os efeitos da fonte. Por exemplo, o valor 5 representa a combinação dos efeitos de fonte negrito (`MDFF_BOLD`) e sublinhado (`MDFF_UNDERLINE`). O valor é o resultado de uma operação OR bit a bit de uma ou mais destas constantes:<br /><br /> `MDFF_BOLD` = 1<br /><br /> `MDFF_ITALIC` = 2<br /><br /> `MDFF_UNDERLINE` = 4<br /><br /> `MDFF_STRIKEOUT` = 8|  
|**FONT_NAME**|A fonte que será usada para exibir a propriedade `VALUE` ou `FORMATTED_VALUE`.|  
|**FONT_SIZE**|O tamanho de fonte que será usada para exibir a propriedade `VALUE` ou `FORMATTED_VALUE`.|  
|**FORE_COLOR**|A cor de primeiro plano para exibir a propriedade `VALUE` ou `FORMATTED_VALUE`. Para obter mais informações, consulte [Conteúdo de FORE_COLOR e BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`FORMAT`|Igual a `FORMAT_STRING`.|  
|`FORMAT_STRING`|A cadeia de caracteres de formato usada para criar o valor de propriedade `FORMATTED_VALUE`. Para obter mais informações, consulte [Conteúdo de FORMAT_STRING &#40;MDX&#41;](mdx-cell-properties-format-string-contents.md).|  
|`FORMATTED_VALUE`|A cadeia de caracteres que representa a exibição formatada da propriedade `VALUE`.|  
|`LANGUAGE`|A localidade onde `FORMAT_STRING` será aplicada. Normalmente, a propriedade `LANGUAGE` é usada para conversão de moeda.|  
|`UPDATEABLE`|Um valor que indica se a célula pode ser atualizada. Essa propriedade pode ter um dos seguintes valores:<br /><br /> `MD_MASK_ENABLED` (0x00000000) a célula pode ser atualizada.<br /><br /> `MD_MASK_NOT_ENABLED` (0x10000000) a célula não pode ser atualizada.<br /><br /> `CELL_UPDATE_ENABLED` (0x00000001) célula pode ser atualizada no conjunto de células.<br /><br /> `CELL_UPDATE_ENABLED_WITH_UPDATE` (0x00000002) a célula pode ser atualizada com uma instrução update. Pode ocorrer um erro na atualização se uma célula folha for atualizada sem estar habilitada para gravação.<br /><br /> `CELL_UPDATE_NOT_ENABLED_FORMULA` (0x10000001) a célula não pode ser atualizada porque a célula tem um membro calculado entre suas coordenadas; a célula foi recuperada com um conjunto onde cláusula. A célula pode ser atualizada mesmo que uma fórmula afete o valor da célula ou haja uma célula calculada ativada (em algum ponto do caminho de agregação). Nessa situação, o valor final da célula pode não ser o valor atualizado, pois o cálculo afetará o resultado.<br /><br /> `CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE` (0x10000002) a célula não pode ser atualizada porque não é possível atualizar medidas não são Soma (contagem, mínimo, máximo, contagem distinta, semiaditiva).<br /><br /> `CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE` (0x10000003) a célula não pode ser atualizada porque ela não existe como ele está na intersecção de uma medida e um membro de dimensão não relacionado ao grupo de medidas da medida.<br /><br /> `CELL_UPDATE_NOT_ENABLED_SECURE` (0x10000005) a célula não pode ser atualizada porque está protegida.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CALCLEVEL` (0x10000006) reservada para uso futuro.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE` (0x10000007) a célula não pode ser atualizada por motivos internos.<br /><br /> `CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE` (0x10000009) a célula não pode ser atualizada porque não há suporte para atualização no modelo de mineração, indiretas ou dimensões de mineração de dados.|  
|`VALUE`|O valor não formatado da célula.|  
  
 São necessárias apenas as propriedades de célula `CELL_ORDINAL`, `FORMATTED_VALUE` e `VALUE`. Todas as propriedades de célula, intrínsecas ou específicas do provedor, são definidas no conjunto de linhas do esquema `PROPERTIES`, incluindo seus tipos de dados e o suporte do provedor. Para obter mais informações sobre o `PROPERTIES` linhas de esquema, consulte [conjunto de linhas MDSCHEMA_PROPERTIES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-properties-rowset).  
  
 Por padrão, se a palavra-chave `CELL PROPERTIES` não for usada, serão retornadas as propriedades de célula `VALUE`, `FORMATTED_VALUE` e `CELL_ORDINAL` (nessa ordem). Se a palavra-chave `CELL PROPERTIES` for usada, serão retornadas somente as propriedades de célula explicitamente declaradas com a palavra-chave.  
  
 O exemplo a seguir demonstra o uso da palavra-chave `CELL PROPERTIES` em uma consulta MDX:  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 As propriedades de célula não são retornadas para consultas MDX que retornam conjuntos de linhas bidimensionais; nesse caso, cada célula é representada como se apenas a propriedade de célula `FORMATTED_VALUE` fosse retornada.  
  
## <a name="setting-cell-properties"></a>Definindo propriedades de célula  
 Propriedades de célula podem ser definidas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em vários locais. Por exemplo, a propriedade Format String pode ser definida para medidas normais na guia Estrutura do Cubo do Editor de Cubos no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]; a mesma propriedade pode ser definida para medidas calculadas definidas no cubo na guia Cálculos do Editor de Cubos; medidas calculadas definidas na cláusula WITH de uma consulta têm a cadeia de caracteres de formato definida nesse local também. A seguinte consulta demonstra como propriedades de célula podem ser definidas em uma medida calculada:  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
