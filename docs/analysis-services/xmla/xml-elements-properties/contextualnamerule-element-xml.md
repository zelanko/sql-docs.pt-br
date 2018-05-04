---
title: Elemento ContextualNameRule (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bfca085e32d314ba9007ea5d1529a849ca39de68
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
