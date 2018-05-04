---
title: Elemento MdxMissingMemberMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MdxMissingMemberMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MdxMissingMemberMode element
ms.assetid: aca6130b-5fb8-4fa1-af8b-8e1ef361926f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2452957134b0c1118695e5a34565ca6053010eb8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdxmissingmembermode-element-assl"></a>Elemento MdxMissingMemberMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Determina como são tratados membros ausentes para linguagens MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
   ...  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Default*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimensão](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Ignorar*|São ignorados membros ausentes.|  
|*Erro*|Um erro surgirá se membros ausentes forem encontrados.|  
|*Default*|São ignorados membros ausentes.|  
  
 O elemento que corresponde ao pai do **MdxMissingMemberMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões multidimensionais & #40; MDX & #41; Referência](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
