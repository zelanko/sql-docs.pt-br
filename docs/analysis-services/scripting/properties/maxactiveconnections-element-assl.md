---
title: Elemento MaxActiveConnections (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MaxActiveConnections Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MaxActiveConnections element
ms.assetid: 0dc5b64d-061d-409f-95c0-4c63f87f5ee4
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1736c2fe5a5dafcb69e226357abac3c52c7f3c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="maxactiveconnections-element-assl"></a>Elemento MaxActiveConnections (ASSL)
  Contém o número máximo de conexões simultâneas permitido por um elemento que é derivado de [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <MaxActiveConnections>...</MaxActiveConnections>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Integer|  
|Valor padrão|**10**|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Se o valor desse elemento for definido como zero, o número máximo de conexões simultâneas é determinado pelo cartucho de dados usado para acessar a fonte de dados. Se o valor desse elemento for definido como um valor negativo, o número máximo de conexões simultâneas é ilimitado.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

