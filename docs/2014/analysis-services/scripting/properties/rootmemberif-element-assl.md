---
title: Elemento RootMemberIf (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- RootMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a923b08efc636d2635d60b00f85c42dc00a312e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010518"
---
# <a name="rootmemberif-element-assl"></a>Elemento RootMemberIf (ASSL)
  Determina como são identificados os membros raiz ou membros de um atributo pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ParentIsBlankSelfOrMissing*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor da `RootMemberIf` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` elemento pai está definido como *pai*) para determinar a raiz ( membros superiores) de uma hierarquia pai-filho.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|Somente os membros que atendam a uma ou mais das condições descritas para *ParentIsBlank*, *ParentIsSelf*, ou *ParentIsMissing* são tratados como membros raiz.|  
|*ParentIsBlank*|Somente membros com um valor nulo, um zero ou uma cadeia de caracteres vazia em colunas de chave representados pelo [KeyColumns](../collections/columns-element-assl.md) coleção de `DimensionAttribute` são tratados como membros raiz.|  
|*ParentIsSelf*|Somente os membros com eles próprios como pais são tratados como membros raiz.|  
|*ParentIsMissing*|Somente membros com pais que não podem ser encontrados são tratados como membros raiz.|  
  
 A enumeração que corresponde aos valores permitidos para `RootMemberIf` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.RootIfValue>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  