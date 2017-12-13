---
title: Elemento MiningModelPermission (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MiningModelPermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MiningModelPermission
helpviewer_keywords: MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 664d8a6f0488eda4cc464fdc31cd49e8463d8a77
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="miningmodelpermission-element-assl"></a>Elemento MiningModelPermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define os permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento ter um indivíduo [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModelPermissions>  
   <MiningModelPermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <AllowBrowsing>...</AllowBrowsing>  
   </MiningModelPermission>  
</MiningModelPermissions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|  
|Elementos filho|[AllowBrowsing](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Em [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode habilitar o detalhamento em estruturas de mineração adicionando a **AllowDrillthrough** permissão para o [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) coleção. Se **AllowDrillthrough** está habilitado na estrutura de mineração e o modelo de mineração, qualquer membro de uma função que tenha [elemento AllowDrillThrough &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) permissões no modelo podem consultar o modelo de mineração de dados e retornar colunas de estrutura que não foram incluídas no modelo, usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Assim, para proteger dados confidenciais ou informações pessoais, você deve conceder a permissão **AllowDrillthrough** em um modelo de mineração somente quando necessário. Para obter mais informações, consulte [elemento AllowDrillThrough &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
