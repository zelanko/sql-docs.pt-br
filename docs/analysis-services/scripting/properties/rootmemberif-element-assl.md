---
title: Elemento RootMemberIf (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cca19adce1c964272c87495af9ef0ed74a315ca7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="rootmemberif-element-assl"></a>Elemento RootMemberIf (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
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
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
