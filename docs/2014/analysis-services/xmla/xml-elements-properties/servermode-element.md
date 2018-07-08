---
title: Elemento ServerMode | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b329f9882b9eff2adf1a79041ea83c51a627f15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239446"
---
# <a name="servermode-element"></a>Elemento ServerMode
  O elemento de servidor `ServerMode` especifica o modo no qual o servidor está operando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|(nenhum)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Servidor](../../scripting/objects/server-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O servidor opera em um dos seguintes modos:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Multidimensional*|Modo multidimensional e de mineração de dados|  
|*Tabular*|Modo de Tabela|  
|*SharePoint*|SharePoint|  
  
## <a name="see-also"></a>Consulte também  
 [Servidor](../../scripting/objects/server-element-assl.md)  
  
  
