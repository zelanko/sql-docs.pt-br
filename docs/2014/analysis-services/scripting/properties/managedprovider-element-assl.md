---
title: Elemento ManagedProvider (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ManagedProvider Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ManagedProvider element
ms.assetid: ed5a1077-20a4-40b9-b62d-0db0d53b9624
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7b29b4db3d2acf34e684d89588ef5f1e2a935aa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101626"
---
# <a name="managedprovider-element-assl"></a>Elemento ManagedProvider (ASSL)
  Contém o nome do provedor gerenciado usado por um elemento que é derivado de [fonte de dados](../data-type/datasource-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <ManagedProvider>...</ManagedProvider>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../data-type/datasource-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Se uma fonte de dados usar um provedor gerenciado, o elemento `ManagedProvider` conterá o nome do provedor gerenciado.  
  
## <a name="see-also"></a>Consulte também  
 [Nomeie o elemento &#40;ASSL&#41;](name-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
