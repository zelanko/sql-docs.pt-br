---
title: Elemento roles (ASSL) | Microsoft Docs
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
apiname: Roles Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Roles
helpviewer_keywords: Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d125df9535303152449ad54ef577995a1da9b6d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="roles-element-assl"></a>Elemento Roles (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [função](../../../analysis-services/scripting/objects/role-element-assl.md) elementos definidos no elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Database](../../../analysis-services/scripting/objects/database-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|[Função](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento **Roles** associado a um elemento **Server** contém apenas uma função, chamada Administrators, que representa a função do administrador do servidor. A função de administrador de servidor não pode ser alterada nem excluída, nem podem ser adicionadas funções à coleção.  
  
 O elemento **Roles** associado a um elemento **Database** contém as funções definidas para aquele banco de dados.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.RoleCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
