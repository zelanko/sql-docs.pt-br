---
title: Elemento RootMemberIf (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RootMemberIf Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9c312a638544071697a59bf1a7ddfb44ce9c5746
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ParentIsBlankSelfOrMissing*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor da **RootMemberIf** elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento do **DimensionAttribute** elemento pai é definido como *pai*) para determinar os membros de raiz (superiores) de uma hierarquia pai-filho.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|Somente os membros que atendam a uma ou mais das condições descritas para *ParentIsBlank*, *ParentIsSelf*, ou *ParentIsMissing* são tratados como membros raiz.|  
|*ParentIsBlank*|Somente membros com um valor nulo, um zero ou uma cadeia de caracteres vazia em colunas de chave representados pelo [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) coleção de **DimensionAttribute** são tratados como membros raiz.|  
|*ParentIsSelf*|Somente os membros com eles próprios como pais são tratados como membros raiz.|  
|*ParentIsMissing*|Somente membros com pais que não podem ser encontrados são tratados como membros raiz.|  
  
 A enumeração que corresponde aos valores permitidos para **RootMemberIf** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.RootIfValue>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

