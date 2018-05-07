---
title: Tipo de dados MiningModelingFlag (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7d000f7efa4fc0355c8359b87931caeb0cbafa12
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="miningmodelingflag-data-type-assl"></a>Tipo de dados MiningModelingFlag (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados primitivo que representa os sinalizadores de modelagem disponíveis para um elemento [ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|Cadeia de caracteres (enumeração)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
|Elementos derivados|[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) (coleção de[ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md) [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md) ou [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O nome do sinalizador pode conter espaços. Os valores suportados de maneira nativa são listados na seguinte tabela.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|A coluna deve ser modelada como se tivesse dois estados, ausente e não ausente, independente dos valores na coluna. Esse procedimento é particularmente útil para colunas em tabelas aninhadas, onde os valores são espaçados entre as caixas.|  
|*NÃO NULO*|A coluna não pode aceitar valores NULL.|  
|*REGRESSOR*|Os valores do regressor de suprimentos da coluna para caixas de teste.|  
  
 Os sinalizadores adicionais específicos do provedor poderão ser usados se o OLE DB de terceiro ou os provedores de mineração de dados forem agregados na instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Um elemento relacionado bastante próximo ao modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.MiningModelingFlags>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
