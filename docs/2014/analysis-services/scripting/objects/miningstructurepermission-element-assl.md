---
title: Elemento MiningStructurePermission (ASSL) | Microsoft Docs
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
- MiningStructurePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f3789cd5b5b72048b9c9163c11bebf4fe5a77d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295486"
---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermission (ASSL)
  Define as permissões que os membros de um [função](role-element-assl.md) elemento ter em um indivíduo [MiningStructure](miningstructure-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../data-type/permission-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
 Na [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], a permissão `AllowDrillthrough` foi estendido para aplicar a uma estrutura de mineração. Ao atribuir essa permissão a uma função, qualquer usuário que for um membro dessa função poderá consultar diretamente a estrutura de mineração usando a seguinte sintaxe:  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 Além disso, se `AllowDrillthrough` for ativado tanto na estrutura quanto no modelo de mineração, os usuários poderão consultar as colunas de estrutura que não foram incluídas no modelo de mineração usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 Por exemplo, você cria um modelo que usa apenas colunas para chave, renda e compras do cliente. Usando o detalhamento, um usuário pode retornar outras colunas de estrutura que não foram incluídas no modelo de mineração, como as informações de contato do cliente.  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, é preciso criar a exibição da fonte de dados de forma que as informações confidenciais sejam mascaradas e conceder a permissão `AllowDrillthrough` em uma estrutura somente quando for necessário.  
  
 Para obter mais informações, consulte [Drillthrough Queries &#40;Data Mining&#41;](../../data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
