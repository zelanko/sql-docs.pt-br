---
title: Elemento ContextualNameRule (XML) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e25061be21fdeea6d303ffce8f9ce9f66f687a34
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="contextualnamerule-element-xml"></a>Elemento ContextualNameRule (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 Fornece uma dica a aplicativos cliente sobre como criar nomes inequívocos para este atributo.  
  
 O valor de **ContextualNameRule** elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|*Nenhuma*|Use o nome do atributo.|  
|*Contexto*|Use o nome da relação de entrada.|  
|*Mesclagem*|Seguindo as regras do idioma de aplicativo, concatene o nome da relação de entrada e o nome de atributo.|  
  
  
