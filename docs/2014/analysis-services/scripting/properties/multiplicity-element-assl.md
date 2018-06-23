---
title: Elemento multiplicity (ASSL) | Microsoft Docs
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
ms.assetid: 441e3829-9009-4b32-a8c6-fa580663387f
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 91ecb8a8b7ada49666d2b6144d1ba258a7c26b58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122917"
---
# <a name="multiplicity-element-assl"></a>Elemento Multiplicity (ASSL)
  Indica se os atributos em RelationshipEnd estão em "um" lado ou em "muitos" lados de uma relação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEnd>  
   ...  
   <Multiplicity>...</Multiplicity>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão||  
|Cardinalidade|1: Elemento requerido que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[RelationshipEnd](../data-type/relationshipend-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Um*|Esta é a extremidade de chave primária.|  
|*Muitos*|Esta é a extremidade de chave estrangeira.|  
  
 A enumeração que corresponde aos valores permitidos para `role` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Multiplicity>.  
  
  