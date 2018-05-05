---
title: Elemento CurrentStorageMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CurrentStorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f369ec1d208cae1871732ed0a26d9a6a96311590
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="currentstoragemode-element-assl"></a>Elemento CurrentStorageMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Determina o modo de armazenamento atual para o elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ROLAP*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez ou não ocorrer nenhuma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O **CurrentStorageMode** elemento indica o modo de armazenamento atualmente em uso para o cache pró-ativo e aplica-se a todos os atributos do elemento pai.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MOLAP*|O pai usa o armazenamento MOLAP (OLAP multidimensional).|  
|*ROLAP*|O pai usa o armazenamento ROLAP (OLAP relacional).|  
|*HOLAP*|O pai usa o armazenamento HOLAP (OLAP híbrido).<br /><br /> Observação: Esse valor só é válido para [partição](../../../analysis-services/scripting/objects/partition-element-assl.md) elementos pai.|  
  
 A enumeração que corresponde aos valores permitidos **CurrentStorageMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.StorageMode>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
