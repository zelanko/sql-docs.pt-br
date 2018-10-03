---
title: Elemento ServerMode | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e714c9f5bbc7626030d83faa7d0058c7aa13752
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140176"
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
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O servidor opera em um dos seguintes modos:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Multidimensional*|Modo multidimensional e de mineração de dados|  
|*Tabular*|Modo de Tabela|  
|*SharePoint*|SharePoint|  
  
## <a name="see-also"></a>Consulte também  
 [Servidor](../../scripting/objects/server-element-assl.md)  
  
  
