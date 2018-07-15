---
title: Elemento MiningModelPermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningModelPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermission
helpviewer_keywords:
- MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb714eb08fac3a6611669d48bf10aaee3580ee8c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176433"
---
# <a name="miningmodelpermission-element-assl"></a>Elemento MiningModelPermission (ASSL)
  Define os permissões que os membros de um [função](role-element-assl.md) elemento ter em um indivíduo [MiningModel](miningmodel-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../data-type/permission-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)|  
|Elementos filho|[AllowBrowsing](../properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Na [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode habilitar o detalhamento em estruturas de mineração adicionando a `AllowDrillthrough` permissão para o [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) coleção. Se `AllowDrillthrough` está habilitado na estrutura de mineração e o modelo de mineração, qualquer membro de uma função que tenha [elemento AllowDrillThrough &#40;ASSL&#41; ](../properties/allowdrillthrough-element-assl.md) permissões no modelo podem consultar o modelo de mineração de dados e retornar colunas de estrutura que não foram incluídas no modelo, usando a sintaxe a seguir:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Assim, para proteger dados confidenciais ou informações pessoais, você deve conceder a permissão `AllowDrillthrough` em um modelo de mineração somente quando necessário. Para obter mais informações, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
