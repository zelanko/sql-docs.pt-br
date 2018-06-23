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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8448e5ac3111f4c1683ae3dd62dcaef992f3f0e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006198"
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
|*Tabela*|Modo de Tabela|  
|*SharePoint*|SharePoint|  
  
## <a name="see-also"></a>Consulte também  
 [Servidor](../../scripting/objects/server-element-assl.md)  
  
  