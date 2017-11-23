---
title: Configurar propriedades de medida | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
caps.latest.revision: "50"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d470010e8f4f5fecef9584abcfa0ad56096ccd75
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-measure-properties"></a>Configurar propriedades de medida
  As medidas têm propriedades que lhe permitem definir como elas funcionam e controlar como elas aparecem para os usuários.  
  
 Você pode definir propriedades em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ao criar ou editar um cubo ou uma medida. Você pode também defini-las programaticamente, usando MDX ou AMO. Consulte [Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) ou [Instrução CREATE MEMBER &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md) ou [Programando objetos OLAP AMO básicos](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md) para obter detalhes.  
  
## <a name="measure-properties"></a>Propriedades das medidas  
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
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades do grupo de medidas](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modificando medidas](../../analysis-services/lesson-3-1-modifying-measures.md)  
  
  
