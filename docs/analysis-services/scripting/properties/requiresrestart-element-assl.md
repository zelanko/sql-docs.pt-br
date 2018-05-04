---
title: Elemento RequiresRestart (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- RequiresRestart Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RequiresRestart
helpviewer_keywords:
- RequiresRestart element
ms.assetid: 9e98f956-c41e-4e15-a7bd-e17c10ee6fc6
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5415e8b436cdf448ad05df716aa3a64aecb71167
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="requiresrestart-element-assl"></a>Elemento RequiresRestart (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém um valor somente leitura associado a um [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) elemento que determina se a alteração do valor da propriedade de servidor requer que a instância seja reiniciado para que a alteração tenha efeito.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ServerProperty>  
   ...  
   <RequiresRestart>...</RequiresRestart>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Boolean|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **RequiresRestart** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ServerProperties & #40; ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Elemento Server & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
