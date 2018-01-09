---
title: Elemento Usage (MiningModelColumn) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Usage Element (MiningModelColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Usage
helpviewer_keywords: Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a0e49b1156817f720b0c7db3205a8d1697ae6b8f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Elemento Usage (MiningModelColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve como a coluna associada no pai [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) é usado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Chave*|A coluna é uma coluna de chave.|  
|*Entrada*|A coluna é uma coluna de entrada.|  
|*Predict*|A coluna é uma coluna de previsão.|  
|*PredictOnly*|A coluna é somente uma coluna de previsão.|  
|*Nenhuma*|A coluna não é usada pelo modelo.<br /><br /> **\*\*Aviso \* \***  quando o valor de uso é "None", Analysis Services não enviará nenhum valor para o servidor por padrão; portanto, o atributo de uso não está incluído na solicitação/resposta.|  
  
 A enumeração que corresponde aos valores permitidos para **uso** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
