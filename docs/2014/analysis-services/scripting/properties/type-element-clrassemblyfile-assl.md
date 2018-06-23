---
title: Tipo de elemento (ClrAssemblyFile) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (ClrAssemblyFile)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ab9e1e2c-ab06-4cd1-b007-16d738dc5604
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c253b2975c5e4f4cbf27c5b2d655a09617d644de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006200"
---
# <a name="type-element-clrassemblyfile-assl"></a>Elemento Type (ClrAssemblyFile) (ASSL)
  Especifica o tipo de arquivo de um dos arquivos que pertencem a um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] assembly do .NET Framework.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ClrAssemblyFile>  
      ...  
      <Type>...</Type>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Principal*|O arquivo especificado é o arquivo principal no assembly.|  
|*Dependentes*|O arquivo especificado é um arquivo dependente no assembly.|  
|*Depurador*|O arquivo especificado contém informações de depuração.|  
  
 A enumeração que corresponde aos valores permitidos para `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ClrAssemblyFileType>.  
  
 O elemento que corresponde ao pai do `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de arquivo &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Elemento de arquivos &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Elemento assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  