---
title: Elemento ServerMode | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 362e91994f4c195a6fe2d48a798444041d6855e8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="servermode-element"></a>Elemento ServerMode
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  O **ServerMode** elemento server especifica o modo de servidor está operando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|(nenhum)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O servidor opera em um dos seguintes modos:  
  
|Value|Description|  
|-----------|-----------------|  
|*Multidimensional*|Modo multidimensional e de mineração de dados|  
|*Tabela*|Modo de Tabela|  
|*SharePoint*|SharePoint|  
  
## <a name="see-also"></a>Consulte também  
 [Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  
