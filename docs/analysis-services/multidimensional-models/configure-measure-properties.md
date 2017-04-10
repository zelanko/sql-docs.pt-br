---
title: "Configurar propriedades de medida | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aditivo [Analysis Services]"
  - "propriedade ID"
  - "propriedade ErrorConfiguration"
  - "propriedade AggregateFunction"
  - "propriedade DisplayFolder"
  - "propriedade IgnoreUnrelatedDimensions"
  - "propriedade FormatString"
  - "propriedade Description"
  - "semiaditivas"
  - "propriedades [Analysis Services], grupos de medidas"
  - "funções de agregação [Analysis Services]"
  - "propriedade DataType"
  - "propriedade ProcessingMode"
  - "propriedade MeasureExpression"
  - "propriedade AggregationPrefix "
  - "propriedade Visible"
  - "propriedades [Analysis Services], medidas"
  - "propriedade StorageLocation"
  - "propriedade StorageMode"
  - "formatos [Analysis Services], medidas"
  - "propriedade Source"
  - "agregações [Analysis Services], medidas"
  - "medidas [Analysis Services], propriedades"
  - "não aditivo [Analysis Services]"
  - "propriedade Name"
  - "medidas [Analysis Services], formatos de exibição"
  - "propriedade ProcessingPriority"
  - "grupos de medidas [Analysis Services], propriedades"
  - "propriedade Type"
  - "propriedade ProactiveCaching "
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
caps.latest.revision: 50
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 50
---
# Configurar propriedades de medida
  As medidas têm propriedades que lhe permitem definir como elas funcionam e controlar como elas aparecem para os usuários.  
  
 Você pode definir propriedades em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ao criar ou editar um cubo ou uma medida. Você pode também defini-las programaticamente, usando MDX ou AMO. Consulte [Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) ou [Instrução CREATE MEMBER &#40;MDX&#41;](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md) ou [Programando objetos OLAP AMO básicos](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md) para obter detalhes.  
  
## Propriedades das medidas  
 As medidas herdam certas propriedades do grupo de medidas do qual fazem parte, exceto se essas propriedades forem substituídas no nível da medida. As propriedades das medidas determinam como uma medida é agregada, seu tipo de dados, o nome exibido ao usuário, a pasta de exibição na qual a medida aparecerá, sua cadeia de caracteres de formato, qualquer expressão de medida, a coluna de origem subjacente e sua visibilidade aos usuários.  
  
|Propriedade|Definição|  
|--------------|----------------|  
|**AggregateFunction**|Obrigatórios. Determina como as medidas são agregadas. **Sum** é a agregação padrão. Para obter mais informações, consulte [Usar funções de agregação](../../analysis-services/multidimensional-models/use-aggregate-functions.md) para obter uma descrição de cada função.|  
|**DataType**|Obrigatórios. Especifica o tipo de dados da coluna da tabela de fatos subjacente à qual a medida está associada. Esse valor é herdado da coluna de origem por padrão.|  
|**Description**|Fornece uma descrição da medida, que pode ser exposta em aplicativos cliente.|  
|**DisplayFolder**|Especifica a pasta na qual a medida aparecerá quando os usuários conectarem-se ao cubo. Se o cubo tiver várias medidas, você pode usar as pastas de exibição para categorizar as medidas e aprimorar a experiência de navegação do usuário.|  
|**FormatString**|Você pode selecionar o formato usado para exibir valores de medida aos usuários utilizando a propriedade **FormatString** da medida.<br /><br /> Embora seja fornecida uma lista de formatos de exibição em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode especificar vários outros formatos que não constam nela. Você pode especificar qualquer formato nomeado ou definido pelo usuário que seja válido no Microsoft Visual Basic.|  
|**ID**|Obrigatórios. Exibe o identificador exclusivo (ID) da medida. Esta propriedade é somente leitura.|  
|**MeasureExpression**|Especifica uma expressão MDX restrita definindo o valor da medida. A expressão é avaliada no nível de folha antes de ser agregada e leva em consideração a importância de um valor. Por exemplo, em conversão de moedas em que um valor de vendas é ponderado pela taxa de câmbio.|  
|**Nome**|Obrigatórios. Especifica o nome da medida.|  
|**Origem**|Obrigatórios. Especifica a coluna da exibição da fonte de dados à qual a medida está associada. Consulte [Fontes de dados e associações &#40;SSAS Multidimensional&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).|  
|**Visível**|Determina a visibilidade da medida em aplicativos cliente.|  
  
## Consulte também  
 [Configurar propriedades do grupo de medidas](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modificando medidas](../../analysis-services/modifying-measures.md)  
  
  