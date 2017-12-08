---
title: Elemento AllowDrillThrough (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllowDrillThrough Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllowDrillThrough
helpviewer_keywords: AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
caps.latest.revision: "51"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 273c96e4406af12582dd3a8a459573539a357736
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="allowdrillthrough-element-assl"></a>Elemento AllowDrillThrough (ASSL)
  Determina se a extração de detalhes é permitida no elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|**Falso**|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Elemento MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **AllowDrillThrough** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, e <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
## <a name="drillthrough-on-mining-structures"></a>Detalhamento em estruturas de mineração  
 Em [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode definir **AllowDrillthrough** permissões para estruturas de mineração, bem como modelos de mineração. Quando você atribuir permissões a uma função, qualquer membro dessa função poderá consultar o modelo de mineração de dados e retornar as colunas de estrutura que não foram incluídas no modelo. Por exemplo, você cria um modelo que usa apenas estas colunas: chave do cliente, renda do cliente e compras do cliente. Ao ativar o detalhamento no modelo, os usuários podem retornar informações de outras colunas da estrutura de mineração, como emails ou nomes de cliente.  
  
 Portanto, para proteger dados confidenciais, tenha cuidado quando for adicionar colunas à estrutura de mineração. Além disso, só conceda a permissão **AllowDrillthrough** em uma estrutura quando ele for necessária.  
  
 Para detalhar colunas de estrutura, use uma consulta com um dos seguintes formulários:  
  
 `SELECT * FROM <structure>.CASES`  
  
 ou  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Role &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
