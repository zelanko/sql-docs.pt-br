---
title: Elemento MiningStructurePermission (ASSL) | Microsoft Docs
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
- MiningStructurePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22713569509019e9d0aac30f82c898c73a034fda
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermission (ASSL)
  Define as permissões que os membros de um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento ter um indivíduo [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
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
|Elementos pai|[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
 Em [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], a permissão **AllowDrillthrough** foi estendido para aplicar a uma estrutura de mineração. Ao atribuir essa permissão a uma função, qualquer usuário que for um membro dessa função poderá consultar diretamente a estrutura de mineração usando a seguinte sintaxe:  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 Além disso, se **AllowDrillthrough** for ativado tanto na estrutura quanto no modelo de mineração, os usuários poderão consultar as colunas de estrutura que não foram incluídas no modelo de mineração usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 Por exemplo, você cria um modelo que usa apenas colunas para chave, renda e compras do cliente. Usando o detalhamento, um usuário pode retornar outras colunas de estrutura que não foram incluídas no modelo de mineração, como as informações de contato do cliente.  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, é preciso criar a exibição da fonte de dados de forma que as informações confidenciais sejam mascaradas e conceder a permissão **AllowDrillthrough** em uma estrutura somente quando for necessário.  
  
 Para obter mais informações, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

