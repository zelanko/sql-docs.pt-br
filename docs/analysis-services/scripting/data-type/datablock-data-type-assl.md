---
title: Tipo de dados DataBlock (ASSL) | Microsoft Docs
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
- DataBlock Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e6d9e7f21417dc7e435b0b65e10a8dbe928a0c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="datablock-data-type-assl"></a>Tipo de dados DataBlock (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa uma coleção de blocos de dados usados para armazenar o conteúdo binário de um elemento [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
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
|Elementos filho|[Blocos](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|Elementos derivados|Elemento[Data](../../../analysis-services/scripting/objects/data-element-assl.md) do tipo [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) (coleção de[Files](../../../analysis-services/scripting/collections/files-element-assl.md) do tipo [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) )|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly & #40; ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Elemento File & #40; ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [Elemento de bloco & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
