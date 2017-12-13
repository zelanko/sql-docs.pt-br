---
title: Bloquear elemento (ASSL) | Microsoft Docs
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
apiname: Block Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Block
helpviewer_keywords: Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e53ea02e3841aaa6bafe91d1373df72f90e34701
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="block-element-assl"></a>Elemento Block (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém todo ou parte do conteúdo binário de um [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Base64Binary|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Blocos](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40; ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Tipo de dados ClrAssembly &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Elemento de arquivos &#40; ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [Elemento File &#40; ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [Tipo de dados ClrAssemblyFile &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [Elemento de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [Tipo de dados DataBlock &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
