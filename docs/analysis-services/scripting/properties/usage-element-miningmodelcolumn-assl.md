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
- analysis-services
- docset-sql-devref
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
ms.openlocfilehash: 81e11a97ca06b9d9e42639d826a92da79f0808ba
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Chave*|A coluna é uma coluna de chave.|  
|*Entrada*|A coluna é uma coluna de entrada.|  
|*Predict*|A coluna é uma coluna de previsão.|  
|*PredictOnly*|A coluna é somente uma coluna de previsão.|  
|*Nenhuma*|A coluna não é usada pelo modelo.<br /><br /> **\*\*Aviso \* \***  quando o valor de uso é "None", Analysis Services não enviará nenhum valor para o servidor por padrão; portanto, o atributo de uso não está incluído na solicitação/resposta.|  
  
 A enumeração que corresponde aos valores permitidos para **uso** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
