---
title: "Tipo de elemento (dimensão) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Type Element (Dimension)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TYPE
helpviewer_keywords: Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f11755a12e1876c1883b08f2460a7d8cc264dc25
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="type-element-dimension-assl"></a>Elemento Type (Dimension) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Fornece informações sobre o conteúdo da dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Alguns valores para **Type**, por exemplo *Accounts*, determinam um comportamento específico.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|A dimensão é uma dimensão regular.|  
|*Hora*|A dimensão é uma dimensão de tempo.<br /><br /> Observação: Esse valor indica que a dimensão oferece suporte a funcionalidades específicas de dimensões de tempo.|  
|*Geografia*|A dimensão contém atributos geográficos.|  
|*Organização*|A dimensão contém atributos organizacionais.|  
|*BillOfMaterials*|A dimensão contém uma conta de atributos de materiais.|  
|*Contas*|A dimensão contém atributos relacionados à conta.<br /><br /> Observação: Esse valor indica que a dimensão oferece suporte a funcionalidades específicas de dimensões de conta.|  
|*Clientes*|A dimensão contém atributos relacionados ao cliente.|  
|*Produtos*|A dimensão contém atributos relacionados ao produto.|  
|*Cenário*|A dimensão contém atributos relacionados ao cenário.|  
|*Quantitativa*|A dimensão contém atributos quantitativos.|  
|*Utilitário*|A dimensão contém atributos de utilitário.|  
|*Moeda*|A dimensão contém atributos de moeda.|  
|*Taxas*|A dimensão contém atributos de taxa de câmbio.|  
|*Canal*|A dimensão contém atributos de canal.|  
|*Promoção*|A dimensão contém atributos relacionados à promoção.|  
  
 A enumeração que corresponde aos valores permitidos para **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionType>.  
  
 O elemento que corresponde ao pai do **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
