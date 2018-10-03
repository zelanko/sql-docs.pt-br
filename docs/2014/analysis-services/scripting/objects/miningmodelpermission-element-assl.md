---
title: Elemento MiningModelPermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6bad2b1bda46fcc1437a5f4c967ced8a6c726f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113466"
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
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)|  
|Elementos filho|[AllowBrowsing](../properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Na [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode habilitar o detalhamento em estruturas de mineração adicionando a `AllowDrillthrough` permissão para o [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) coleção. Se `AllowDrillthrough` está habilitado na estrutura de mineração e o modelo de mineração, qualquer membro de uma função que tenha [elemento AllowDrillThrough &#40;ASSL&#41; ](../properties/allowdrillthrough-element-assl.md) permissões no modelo podem consultar o modelo de mineração de dados e retornar colunas de estrutura que não foram incluídas no modelo, usando a sintaxe a seguir:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Assim, para proteger dados confidenciais ou informações pessoais, você deve conceder a permissão `AllowDrillthrough` em um modelo de mineração somente quando necessário. Para obter mais informações, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
