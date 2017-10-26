---
title: Elemento KeyDuplicate (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- KeyDuplicate Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- KeyDuplicate
helpviewer_keywords:
- KeyDuplicate element
ms.assetid: d7000b8b-e81f-4401-8738-00c2e0f73a59
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ad7c929abb2cfbf2d3609ec72227372d8b32061
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="keyduplicate-element-assl"></a>Elemento KeyDuplicate (ASSL)
  Determina como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] manipula um erro de chave duplicada, caso seja encontrado algum durante o processamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyDuplicate>...</KeyDuplicate>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*IgnoreError*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os erros de chave duplicada são gerados apenas durante o processamento da dimensão, quando uma chave de atributo é encontrada mais de uma vez. Como as chaves de atributo devem ser exclusivas, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] descarta os registros duplicados. Os erros de chave duplicadas indicam uma falha na criação da dimensão, especificamente nas relações entre os atributos.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IgnoreError*|O processamento deve ignorar o erro e continuar.|  
|*ReportAndContinue*|O processamento deve relatar o erro e continuar.|  
|*ReportAndStop*|O processamento deve relatar o erro e parar.|  
  
 A enumeração que corresponde aos valores permitidos para **KeyDuplicate** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

