---
title: Elemento AllowDrillThrough (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowDrillThrough Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79abc9833c111c472776d0713a0ca50888cae27d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090846"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|`False`|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer uma vez, e somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Elemento MiningModel](../objects/miningmodel-element-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de `AllowDrillThrough` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission> e <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
## <a name="drillthrough-on-mining-structures"></a>Detalhamento em estruturas de mineração  
 Na [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode definir `AllowDrillthrough` permissões para estruturas de mineração, bem como modelos de mineração. Quando você atribuir permissões a uma função, qualquer membro dessa função poderá consultar o modelo de mineração de dados e retornar as colunas de estrutura que não foram incluídas no modelo. Por exemplo, você cria um modelo que usa apenas estas colunas: chave do cliente, renda do cliente e compras do cliente. Ao ativar o detalhamento no modelo, os usuários podem retornar informações de outras colunas da estrutura de mineração, como emails ou nomes de cliente.  
  
 Portanto, para proteger dados confidenciais, tenha cuidado quando for adicionar colunas à estrutura de mineração. Além disso, só conceda a permissão `AllowDrillthrough` em uma estrutura quando ele for necessária.  
  
 Para detalhar colunas de estrutura, use uma consulta com um dos seguintes formulários:  
  
 `SELECT * FROM <structure>.CASES`  
  
 ou em  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de função &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
