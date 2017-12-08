---
title: Elemento ContextualNameRule (XML) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fff68bc1e6cc33a89e8fece5922cb7b50a9d25c3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
  
