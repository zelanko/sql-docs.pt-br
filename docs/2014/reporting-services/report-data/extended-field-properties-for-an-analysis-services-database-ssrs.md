---
title: Propriedades de campo estendidas para uma análise dos serviços de banco de dados (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec122493d7af91bc5aa5483fbdb1de842705c90
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62695808"
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Propriedades de campo estendidas para um banco de dados do Analysis Services (SSRS)
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extensão de processamento de dados oferece suporte a propriedades de campo estendidas. Propriedades de campo estendidas são propriedades adicionais às propriedades de campo `Value` e `IsMissing` que estão disponíveis na fonte de dados e são suportadas pela extensão de processamento de dados. As propriedades estendidas não aparecem no painel de dados do relatório como parte da coleção de campos para um conjunto de dados do relatório. Você pode incluir valores de propriedade de campo estendidas em seu relatório escrevendo expressões que especificá-los por nome usando o interno `Fields` coleção.  
  
 As propriedades estendidas incluem propriedades predefinidas e personalizadas. As propriedades predefinidas são propriedades comuns a várias fontes de dados que são mapeados para nomes de propriedade de campo específico e podem ser acessados por meio de interno `Fields` coleção por nome. Propriedades personalizadas são específicas para cada provedor de dados e podem ser acessadas por meio de interno `Fields` coleta apenas pela sintaxe usando o nome da propriedade estendida como uma cadeia de caracteres.  
  
 Quando você usa o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] designer de consulta MDX no modo gráfico para definir a consulta, um conjunto predefinido de propriedades de dimensão e as propriedades de célula são adicionadas automaticamente à consulta MDX. Você só pode usar as propriedades estendidas que estiverem especificamente listadas na consulta MDX em seu relatório. Dependendo do seu relatório, você talvez queira modificar o texto do comando MDX padrão para incluir outra dimensão ou propriedades personalizadas definidas no cubo. Para obter mais informações sobre campos estendidos disponíveis nas [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fontes de dados, consulte [criando e usando valores de propriedade &#40;MDX&#41;](../../analysis-services/creating-and-using-property-values-mdx.md).  
  
## <a name="working-with-field-properties-in-a-report"></a>Trabalhando com propriedades de campo em um relatório  
 Propriedades de campo estendidas incluem propriedades predefinidas e propriedades específicas do provedor de dados. Propriedades de campo não aparecem com a lista de campo na **dados de relatório** painel, embora eles estejam na consulta criada para um conjunto de dados; portanto, é possível arrastar as propriedades de campo para a superfície de design de relatórios. Em vez disso, você deve arrastar o campo para o relatório e, em seguida, alterar o `Value` propriedade do campo para a propriedade que você deseja usar. Por exemplo, se os dados da célula de um cubo já tiverem sido formatados, você pode usar a propriedade de campo FormattedValue usando a seguinte expressão: `=Fields!FieldName.FormattedValue`.  
  
 Para fazer referência a uma propriedade estendida que não seja predefinida, use a seguinte sintaxe em uma expressão:  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>Propriedades de campo predefinidas  
 Na maioria dos casos, o campo predefinido de propriedades se aplicam a medidas, níveis ou dimensões. Uma propriedade de campo predefinida deve ter um valor correspondente armazenado no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fonte de dados. Se um valor não existir ou se você especificar uma propriedade de campo de medida somente em um nível (por exemplo), a propriedade retorna um valor nulo.  
  
 Você pode usar qualquer uma das seguintes sintaxes para se referir a uma propriedade predefinida a partir de uma expressão:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 A tabela a seguir fornece uma lista de propriedades de campo predefinidas que você pode usar.  
  
|**Property**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Especifica o valor do campo de dados.|  
|`IsMissing`|`Boolean`|Indica se o campo foi encontrado no conjunto de dados resultante.|  
|`UniqueName`|`String`|Retorna o nome totalmente qualificado de um nível. Por exemplo, o `UniqueName` valor de um funcionário pode ser *[funcionário]. [ Employee Department]. [Department]. & [Sales]. & [gerente de vendas na América do Norte. Manager].&[272]*.|  
|`BackgroundColor`|`String`|Retorna a cor de plano de fundo definida no banco de dados para o campo.|  
|`Color`|`String`|Retorna a cor de primeiro plano definida no banco de dados para o item.|  
|`FontFamily`|`String`|Retorna o nome da fonte definido no banco de dados para o item.|  
|`FontSize`|`String`|Retorna o tamanho da fonte definido no banco de dados para o item.|  
|`FontWeight`|`String`|Retorna o peso da fonte definido no banco de dados para o item.|  
|`FontStyle`|`String`|Retorna o estilo da fonte definido no banco de dados para o item.|  
|`TextDecoration`|`String`|Retorna formatação de texto especial definida no banco de dados para o item.|  
|`FormattedValue`|`String`|Retorna um valor formatado para uma figura de medidas ou a chave. Por exemplo, o `FormattedValue` propriedade para **Sales Amount Quota** retorna um formato de moeda como $1.124.400,00.|  
|`Key`|`Object`|Retorna a chave para um nível.|  
|`LevelNumber`|`Integer`|Para hierarquias pai-filho, retorna o número de dimensão ou nível.|  
|`ParentUniqueName`|`String`|Para hierarquias pai-filho, retorna um nome totalmente qualificado do nível pai.|  
  
> [!NOTE]  
>  Valores existem para essas propriedades de campo estendidas somente se a fonte de dados (por exemplo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo) fornecer esses valores quando o relatório é executado e recupera os dados para seus conjuntos de dados. Em seguida, você pode consultar esses valores de propriedade de campo de qualquer expressão usando a sintaxe descrita na seção a seguir. No entanto, como esses campos são específicos para este provedor de dados, as alterações feitas a esses valores não são salvas com a definição de relatório.  
  
### <a name="example-extended-properties"></a>Exemplo de propriedades estendidas  
 Para ilustrar as propriedades estendidas, a seguinte consulta MDX e resultado conjunto incluem várias propriedades de membro disponíveis a partir de um atributo de dimensão definido para um cubo. As propriedades de membro incluídas são MEMBER_CAPTION, UNIQUENAME, Properties ("nome de dia"), MEMBER_VALUE, PARENT_UNIQUE_NAME e MEMBER_KEY.  
  
 Essa consulta MDX é executada em relação a [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] cubo a [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados do DW, incluído com o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] bancos de dados de exemplo.  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 Quando você executa essa consulta no painel de consulta MDX, você obtém um conjunto de resultados com 1158 linhas. As primeiras quatro linhas são mostradas na tabela a seguir.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|Todos os períodos|[Data]. [Data]. [Todos os períodos]|(null)|(null)|(null)|0|  
|1-Jul-01|[Data]. [Data]. & [1]|Domingo|7/1/2001|[Data]. [Data]. [Todos os períodos]|1|  
|2-Jul-01|[Data]. [Data]. & [2]|Segunda-feira|7/2/2001|[Data]. [Data]. [Todos os períodos]|2|  
|3-Jul-01|[Data]. [Data]. & [3]|Terça-feira|7/3/2001|[Data]. [Data]. [Todos os períodos]|3|  
  
 Consultas MDX padrão incorporadas usando o Designer de consulta MDX no modo de gráfico apenas incluem MEMBER_CAPTION e UNIQUENAME para as propriedades de dimensão. Por padrão, esses valores sempre são do tipo de dados `String`.  
  
 Se você precisar de uma propriedade de membro em seu tipo de dados original, você pode incluir uma propriedade adicional MEMBER_VALUE modificando a instrução do MDX padrão no designer de consulta baseado em texto. A seguinte instrução MDX simple, MEMBER_VALUE foi adicionada à lista de propriedades de dimensão para recuperar.  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 As primeiras quatro linhas do resultado no painel resultados MDX aparecem na tabela a seguir.  
  
|Mês do ano|Contagem de pedidos|  
|-------------------|-----------------|  
|Janeiro|2,481|  
|Fevereiro|2,684|  
|Março|2,749|  
|Abril|2,739|  
  
 Embora as propriedades são parte da instrução MDX select, eles não aparecem em colunas do conjunto de resultados. No entanto, os dados estão disponíveis para um relatório usando o recurso de propriedades estendidas. Em um painel de resultados de consulta MDX no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode clicar duas vezes na célula e ver os valores de propriedade de célula se elas estiverem definidas no cubo. Se você clicar duas vezes na primeira célula contagem dos pedidos que contém 1379, você verá uma janela pop-up com as seguintes propriedades de célula:  
  
|Propriedade|Valor|  
|--------------|-----------|  
|CellOrdinal|0|  
|VALUE|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Se você criar um conjunto de dados de relatório com essa consulta e associar o conjunto de dados a uma tabela, você pode ver a propriedade de valor padrão para um campo, por exemplo, `=Fields!Month_of_Year!Value`. Se você definir essa expressão como a expressão de classificação para a tabela, seus resultados servirão para classificar a tabela em ordem alfabética por mês, porque o campo de valor usa um `String` tipo de dados. Para classificar a tabela de modo que os meses fiquem na ordem ocorrerem no ano com o primeiro de janeiro e dezembro último, uso a expressão a seguir:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 Isso classifica o valor do campo em seu tipo de dados de inteiro original da fonte de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [Coleções internas em expressões &#40;relatórios e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)   
 [Coleção de campos de conjunto de dados &#40;relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
