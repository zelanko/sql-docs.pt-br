---
title: "Tipo de elemento (associação) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (Binding)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: b5f5c485-dc83-4d66-a8d2-e96e96d068f9
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 978a5ce423cfa50bbe958046ff7f5da77314cd83
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-binding-assl"></a>Elemento Type (Binding) (ASSL)
  Contém o tipo de ligação do atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Type>...</Type>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Todos*|Todos os níveis|  
|*Chave*|Chaves de membro|  
|*Nome*|Nome do membro|  
|*Value*|Valor do membro|  
|*Tradução*|Conversões de membro|  
|*UnaryOperator*|Operadores unários|  
|*SkippedLevels*|Níveis ignorados|  
|*CustomRollup*|Fórmulas de acúmulo personalizado|  
|*CustomRollupProperties*|Propriedades de acúmulo personalizado|  
  
 Os elementos que correspondem aos pais de **tipo** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AttributeBinding> e <xref:Microsoft.AnalysisServices.CubeAttributeBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Associação de tipo de dados &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

