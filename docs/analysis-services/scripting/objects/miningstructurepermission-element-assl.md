---
title: Elemento MiningStructurePermission (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d933d5051a9280d779c23eeb60832aee286dc131
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
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
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
