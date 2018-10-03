---
title: Tipo de dados ClrAssembly (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClrAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9171832bac6653e7c1d86915ae006c65022668a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159246"
---
# <a name="clrassembly-data-type-assl"></a>Tipo de dados ClrAssembly (ASSL)
  Define um tipo de dados derivado que representa uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly associado um [banco de dados](../objects/database-element-assl.md) ou [Server](../objects/server-element-assl.md) elemento  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Assembly](../objects/assembly-element-assl.md)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum (tipo abstrato)|  
|Elementos filho|[Arquivos](../collections/files-element-assl.md), [PermissionSet](../properties/permissionset-element-assl.md)|  
|Elementos derivados|Ver [Assembly](../objects/assembly-element-assl.md) ([Assemblies](../collections/assemblies-element-assl.md) coleção de [banco de dados](../objects/database-element-assl.md) ou [Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O `ClrAssembly` elemento contém os arquivos necessários para recriar uma [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly, associado a uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou com um banco de dados específico em uma instância do [!INCLUDE[ssAS](../../../includes/ssas-md.md)], bem como o permissões necessárias para executar o assembly.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ClrAssembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de arquivo &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Tipo de dados ClrAssemblyFile &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [Elemento de dados &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de dados DataBlock &#40;ASSL&#41;](datablock-data-type-assl.md)   
 [Bloqueia o elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Bloquear o elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipo de dados ComAssembly &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
