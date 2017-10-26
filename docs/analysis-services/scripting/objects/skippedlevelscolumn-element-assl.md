---
title: Elemento SkippedLevelsColumn (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SkippedLevelsColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 181e93110f5e482a04940ee5fe66bbba99b6c073
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="skippedlevelscolumn-element-assl"></a>Elemento SkippedLevelsColumn (ASSL)
    
> [!NOTE]  
>  Este recurso não está disponível nesta versão de Microsoft SQL Server. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 Fornece os detalhes de uma coluna que armazena o número de níveis ignorados (vazios) entre cada membro e seu pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **SkippedLevelsColumn** elemento é aplicável somente a atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento para o **DimensionAttribute** pai está definido para *pai*). O elemento **SkippedLevelsColumn** contém a coluna ou o atributo para o atributo pai que armazena o número de níveis ignorados entre cada membro e seu pai. Isso permite que hierarquias pai-filho baseadas no atributo pai ignorem níveis entre membros. Os valores contidos nessa coluna ou atributo devem ser inteiros não negativos; caso contrário, um erro de processamento ocorrerá. Se o elemento **SkippedLevelsColumn** não for especificado ou não contiver nenhum valor, o membro atual terá um nível abaixo de seu pai.  
  
 Para obter mais informações sobre o **DataItem** tipo, incluindo uma tabela de objetos do Analysis Services Scripting Language (ASSL) e propriedades do **DataItem** de tabela, consulte [tipos de dados DataItem &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 O elemento que corresponde ao pai do **SkippedLevelsColumn** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos de elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Elemento Dimension &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

