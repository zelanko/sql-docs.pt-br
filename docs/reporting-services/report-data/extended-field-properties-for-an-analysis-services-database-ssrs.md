---
title: Propriedades de campos estendidos para um banco de dados do Analysis Services (SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d5c9c11ddf274af9bf8f1851509dae5bff8e27a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Propriedades de campos estendidos para um banco de dados do Analysis Services (SSRS)
  A extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte às propriedades de campo estendidas. As propriedades de campo estendidas são propriedades adicionais às propriedades de campo **Value** e **IsMissing** que estão disponíveis na fonte de dados e que têm suporte na extensão de processamento de dados. As propriedades estendidas não são exibidas no painel Dados do Relatório como parte da coleção de campos de um conjunto de dados do relatório. Você pode inclui os valores de propriedade do campo estendido em seu relatório escrevendo expressões que os especifiquem por nome usando a coleção interna de **Fields** .  
  
 As propriedades estendidas incluem propriedades predefinidas e propriedades personalizadas. As propriedades predefinidas são propriedades comuns a várias fontes de dados mapeadas para nomes de propriedade de campo específico e podem ser acessadas por nome por meio da coleção interna de **Fields** . As propriedades personalizadas são específicas de cada provedor de dados e podem ser acessadas por meio da coleção interna de **Fields** apenas pela sintaxe usando o nome da propriedade estendida como uma cadeia de caracteres.  
  
 Ao usar o designer de consultas MDX do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo gráfico para definir a consulta, um conjunto predefinido de propriedades de células e propriedades de dimensão é adicionado automaticamente à consulta MDX. Apenas as propriedades estendidas que estiverem especificamente listadas na consulta MDX em seu relatório poderão ser usadas. Dependendo do relatório, é possível modificar o texto do comando MDX padrão para incluir outra dimensão ou propriedades personalizadas definidas no cubo. Para obter mais informações sobre os campos estendidos disponíveis nas fontes de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Criando e usando valores de propriedade &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2).  
  
## <a name="working-with-field-properties-in-a-report"></a>Trabalhando com as propriedades de campo em um relatório  
 As propriedades de campo estendidas incluem as propriedades predefinidas e as propriedades específicas para um provedor de dados. As propriedades de campo não são exibidas com a lista de campos no painel **Dados do Relatório** , embora elas estejam na consulta criada para um conjunto de dados; portanto, não é possível arrastar as propriedades de campo para a superfície de design de relatórios. Em vez disso, você deverá arrastar o campo para o relatório e alterar a propriedade **Value** do campo para a propriedade que você quer usar. Por exemplo, se os dados da célula de um cubo já tiverem sido formatados, você poderá usar a propriedade de campo FormattedValue usando a seguinte expressão: `=Fields!FieldName.FormattedValue`.  
  
 Para consultar uma propriedade estendida que não seja predefinida, use a seguinte sintaxe em uma expressão:  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>Propriedades de campo predefinidas  
 Na maioria dos casos, as propriedades de campo predefinidas são aplicadas a medidas, níveis ou dimensões. Uma propriedade de campo predefinida deve ter um valor correspondente armazenado na fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se não existir um valor ou se você especificar uma propriedade de campo em um nível apenas para medida (por exemplo), a propriedade retornará um valor nulo.  
  
 Para consultar uma propriedade predefinida a partir de uma expressão, use as seguintes sintaxes:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 A tabela a seguir fornece uma lista das propriedades de campo predefinidas que você pode usar.  
  
|**Propriedade**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Objeto**|Especifica o valor de dados do campo.|  
|**IsMissing**|**Booliano**|Indica se o campo foi encontrado no conjunto de dados resultante.|  
|**UniqueName**|**String**|Retorna o nome totalmente qualificado de um nível. Por exemplo, o valor **UniqueName** de um funcionário pode ser *[Employee].[Employee Department].[Department].&[Sales].&[North American Sales Manager].&[272]*.|  
|**BackgroundColor**|**String**|Retorna a cor do segundo plano definida no banco de dados para o campo.|  
|**Color**|**String**|Retorna a cor do primeiro plano definida no banco de dados para o item.|  
|**FontFamily**|**String**|Retorna o nome da fonte definido no banco de dados para o item.|  
|**FontSize**|**String**|Retorna o tamanho da fonte definido no banco de dados para o item.|  
|**FontWeight**|**String**|Retorna a espessura da fonte definida no banco de dados para o item.|  
|**FontStyle**|**String**|Retorna o estilo da fonte definido no banco de dados para o item.|  
|**TextDecoration**|**String**|Retorna a formatação de texto especial definida no banco de dados para o item.|  
|**FormattedValue**|**String**|Retorna um valor formatado para a medida ou o número chave. Por exemplo, a propriedade **FormattedValue** para **Cota do Valor de Vendas** retorna um formato de moeda como US$ 1.124.400,00.|  
|**Chave**|**Objeto**|Retorna a chave para um nível.|  
|**LevelNumber**|**Integer**|Para hierarquias pai-filho, retorna o nível ou o número de dimensões.|  
|**ParentUniqueName**|**String**|Para hierarquias pai-filho, retorna um nome totalmente qualificado do nível pai.|  
  
> [!NOTE]  
>  Os valores dessas propriedades de campo estendidas passarão a existir somente se a fonte de dados (por exemplo, o cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) fornecer esses valores quando você executar e recuperar os dados de seus conjuntos de dados. Dessa forma, você poderá consultar esses valores da propriedade de campo a partir de qualquer expressão usando a sintaxe descrita na seguinte seção. Entretanto, como esses campos são específicos para esse provedor de dados, as alterações que forem feitas nesse valor não serão salvas com a definição de relatório.  
  
### <a name="example-extended-properties"></a>Exemplo de propriedades estendidas  
 Para ilustrar as propriedades estendidas, a consulta MDX e o conjunto de resultados a seguir incluem várias propriedades de membro disponíveis a partir de um atributo de dimensão definido para um cubo. As propriedades de membro incluídas são MEMBER_CAPTION, UNIQUENAME, Properties("Nome do Dia"), MEMBER_VALUE, PARENT_UNIQUE_NAME e MEMBER_KEY.  
  
 Essa consulta MDX é executada no cubo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW, incluído com os bancos de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
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
  
 Ao executar essa consulta em um painel de consulta MDX, você pode obter um conjunto de resultados com 1158 linhas. As primeiras quatro linhas são exibidas na tabela a seguir.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|Todos os Períodos|[Data].[Data].[Todos os Períodos]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|Domingo|7/1/2001|[Data].[Data].[Todos os Períodos]|1|  
|2-Jul-01|[Date].[Date].&[2]|Segunda-feira|7/2/2001|[Data].[Data].[Todos os Períodos]|2|  
|3-Jul-01|[Date].[Date].&[3]|Terça-feira|7/3/2001|[Data].[Data].[Todos os Períodos]|3|  
  
 As consultas MDX padrão incorporadas usando o Designer de Consulta MDX no modo gráfico incluem apenas MEMBER_CAPTION e UNIQUENAME para as propriedades de dimensão. Por padrão, esses valores sempre são do tipo de dados **String**.  
  
 Se precisar de uma propriedade do membro em seu tipo de dados original, você poderá incluir uma propriedade adicional MEMBER_VALUE modificando a instrução MDX padrão no designer de consulta baseado em texto. Na instrução MDX simples indicada a seguir, MEMBER_VALUE foi adicionada à lista de propriedades de dimensão a ser recuperada.  
  
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
  
 As primeiras quatro linhas do resultado no painel Resultados MDX aparecem na tabela a seguir.  
  
|Mês do ano|Contagem de pedidos|  
|-------------------|-----------------|  
|Janeiro|2,481|  
|Fevereiro|2,684|  
|Março|2,749|  
|Abril|2,739|  
  
 Embora as propriedades façam parte da instrução de seleção MDX, elas não são exibidas nas colunas de conjunto de resultados. No entanto, os dados são disponibilizados para um relatório usando o recurso de propriedades estendidas. No painel de resultados da consulta MDX no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode clicar duas vezes na célula e ver os valores de propriedade da célula, caso eles estejam definidos no cubo. Se clicar duas vezes na primeira célula Contagem de Pedidos que contém 1379, será exibida uma janela com as seguintes propriedades da célula:  
  
|Propriedade|Valor|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Se você criar um conjunto de dados de relatório com essa consulta e associar o conjunto de dados a uma tabela, poderá ver a propriedade VALUE padrão de um campo, por exemplo, `=Fields!Month_of_Year!Value`. Se você definir essa expressão como a expressão de classificação para a tabela, seus resultados servirão para classificar a tabela em ordem alfabética, por mês, porque o campo Value usa um tipo de dados **String** . Para classificar a tabela de forma que os meses fiquem na ordem correta do ano, de janeiro a dezembro, use a seguinte expressão:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 Isso classifica o valor do campo em seu tipo de dados de inteiro original a partir da fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
