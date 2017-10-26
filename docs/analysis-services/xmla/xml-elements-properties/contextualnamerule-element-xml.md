---
title: Elemento ContextualNameRule (XML) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: 6
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5860c69f618cb9c1cb131bf2da377bad405c09b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="contextualnamerule-element-xml"></a>Elemento ContextualNameRule (XML)
  Fornece uma dica sobre a melhor forma de construir um nome composto para o atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|-1|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Fornece uma dica a aplicativos cliente sobre como criar nomes inequívocos para este atributo.  
  
 O valor de **ContextualNameRule** elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Use o nome do atributo.|  
|*Contexto*|Use o nome da relação de entrada.|  
|*Mesclagem*|Seguindo as regras do idioma de aplicativo, concatene o nome da relação de entrada e o nome de atributo.|  
  
  

