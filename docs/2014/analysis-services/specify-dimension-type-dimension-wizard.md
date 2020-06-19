---
title: Especificar tipo de dimensão (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0a280411bc05bdab416a177cea89f252a53ac0fc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940397"
---
# <a name="specify-dimension-type-dimension-wizard"></a>Especificar Tipo de Dimensão (Assistente para Dimensões)
  Use a página **Especificar Tipo de Dimensão** para definir o tipo de dimensão e adicionar tipos especiais de atributo associados com o tipo de dimensão selecionado para a dimensão.  
  
> [!NOTE]  
>  Esta página só será exibida se você selecionar **Dimensão padrão** na página **Selecionar o Tipo de Dimensão** .  
  
## <a name="options"></a>Opções  
 **Tipo de dimensão**  
 Selecione o tipo de dimensão para a dimensão. A tabela a seguir lista os tipos de dimensão disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Contas**|As dimensões de conta contêm dados e metadados que representam uma lista de contas.<br /><br /> Para obter mais informações sobre dimensões de conta, consulte [Criar uma Conta de Finanças de dimensão de tipo pai-filho](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**BillOfMaterials**|Dimensões de lista de materiais (ou dimensões BOM) são dimensões regulares nas quais os dados e metadados representam inventário ou informações de produção, como listas de peças para produtos.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Channel**|Dimensões de canal são dimensões regulares nas quais os dados e metadados representam informações de canal.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Currency**|Dimensões de moeda contêm dados e metadados que representam informações de moeda.<br /><br /> Para obter mais informações sobre dimensões de moeda, consulte [Criar uma dimensão de tipo de moeda](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|**Utilizam**|Dimensões de cliente são dimensões regulares nas quais os dados e metadados representam informações de cliente.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Geografia**|Dimensões de geografia são dimensões regulares nas quais os dados e metadados representam informações geográficas, como cidades ou códigos postais.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Organização**|Dimensões de organização são dimensões regulares nas quais os dados e metadados representam informações de organização, como empregados ou subsidiárias.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Produtos**|Dimensões de produto são dimensões regulares nas quais os dados e metadados representam informações de produto.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Promoção**|Dimensões de promoção são dimensões regulares nas quais os dados e metadados representam informações de promoção de marketing.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Quantitative**|Dimensões quantitativas são dimensões regulares nas quais os dados e metadados representam informações quantitativas.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Rates**|Dimensões de taxa contêm dados e metadados que representam informações de taxa de câmbio e conversão de moeda.|  
|**Regular**|As dimensões regulares são o tipo de dimensão mais comum usado no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Cenário**|Dimensões de cenário são dimensões regulares nas quais os dados e metadados representam informações de planejamento ou de análise estratégica.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Hora**|Dimensões de tempo contêm dados e metadados orientados ao tempo.<br /><br /> Para obter mais informações sobre dimensões de tempo, consulte [Criar uma dimensão de tipo de data](multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
|**Utilitário**|Dimensões de utilitário são dimensões regulares nas quais os dados e metadados representam informações que não correspondem prontamente a outro tipo de dimensão.<br /><br /> Para obter mais informações sobre dimensões regulares, consulte [Tipos de dimensão](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
  
## <a name="dimension-attributes-options"></a>Opções de atributos de dimensão  
  
> [!NOTE]  
>  As opções nesta seção só ficarão disponíveis se o **Tipo de dimensão** selecionado tiver tipos de atributo especiais associados a ele. Nem todos os tipos de dimensão têm tipos de atributo especiais associados a eles.  
  
 **Incluir**  
 Selecione para incluir o tipo de atributo na dimensão.  
  
 **Tipo de Atributo**  
 Exibe o tipo de atributo associado ao tipo de dimensão selecionado em **Tipo de dimensão**. Para obter mais informações sobre tipos de atributos, consulte [Type Element &#40;DimensionAttribute&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl) (Elemento Type &#40;DimensionAttribute&#41; &#40;ASSL&#41;).  
  
 **Atributo de Dimensão**  
 Selecione o atributo de dimensão ao qual o Assistente para Dimensões atribuirá o tipo de atributo especial exibido em **Tipo de atributo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente para dimensões](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
