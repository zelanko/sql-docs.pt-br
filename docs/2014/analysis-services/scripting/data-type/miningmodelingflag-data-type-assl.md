---
title: Tipo de dados MiningModelingFlag (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelingFlag Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelingFlag
helpviewer_keywords:
- MiningModelingFlag data type
ms.assetid: aaa72ba8-051e-4b01-b1e9-9c8d83b8b752
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93b84a3509d3992ffac20ebeafcda2d4f15f2073
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153007"
---
# <a name="miningmodelingflag-data-type-assl"></a>Tipo de dados MiningModelingFlag (ASSL)
  Define um tipo de dados primitivo que representa os sinalizadores de modelagem disponíveis para um [ModelingFlag](../objects/modelingflag-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Cadeia de caracteres (enumeração)|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|None|  
|Elementos derivados|[ModelingFlag](../objects/modelingflag-element-assl.md) ([ModelingFlags](../collections/modelingflags-element-assl.md) coleção de [MiningModelColumn](miningmodelcolumn-data-type-assl.md) ou [ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O nome do sinalizador pode conter espaços. Os valores suportados de maneira nativa são listados na seguinte tabela.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|A coluna deve ser modelada como se tivesse dois estados, ausente e não ausente, independente dos valores na coluna. Esse procedimento é particularmente útil para colunas em tabelas aninhadas, onde os valores são espaçados entre as caixas.|  
|*NÃO NULO*|A coluna não pode aceitar valores NULL.|  
|*REGRESSOR*|Os valores do regressor de suprimentos da coluna para caixas de teste.|  
  
 Sinalizadores adicionais específicos do provedor podem ser usados se os provedores de mineração de dados ou OLE DB de terceiros forem agregados na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Um elemento relacionado bastante próximo ao modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.MiningModelingFlags>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
