---
title: Tipo de dados PushedDataSource (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- PushedDataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PushedDataSource
helpviewer_keywords:
- PushedDataSource data type
ms.assetid: b319ee87-7c0a-41ec-a8af-cc7089aeb6ad
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0dab21d76eacb3fc4f4b7d8f91d94b15d92caa1b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="pusheddatasource-data-type-assl"></a>Tipo de dados PushedDataSource (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa uma fonte de dados (como um pacote [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ) usado para "empurrar" dados em um elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<PushedDataSource>  
   <Root>...</Root>  
   <EndOfData>...</EndOfData>  
</PushedDataSource>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhuma|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[EndOfData](../../../analysis-services/scripting/properties/endofdata-element-assl.md), [Root](../../../analysis-services/scripting/properties/root-element-assl.md)|  
|Elementos derivados|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 **PushedDataSource** só é usado em um comando de processamento como uma fonte de dados fora de linha. Fontes de dados persistentes nunca são desse tipo.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
