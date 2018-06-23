---
title: Conteúdo de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Content Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Content
helpviewer_keywords:
- Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98d2de4a0ce93e857a63ebd9fe79dd18d0f9a86e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009426"
---
# <a name="content-element-assl"></a>Elemento Content (ASSL)
  Descreve o conteúdo da coluna no [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Essa enumeração descreve o tipo de conteúdo representado por uma coluna da estrutura de mineração e pode ser estendida conforme necessário pelos provedores de algoritmo de mineração. Para obter mais informações sobre tipos de conteúdo, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../data-mining/content-types-data-mining.md).  
  
 Os valores listados na tabela a seguir normalmente têm suporte em todos os provedores de algoritmo de mineração.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Discreto*|A coluna contém valores discretos.|  
|*Contínua*|Os valores para a coluna definem um conjunto contínuo de dados numéricos.|  
|*Dados discretos*|Os valores da coluna representam grupos (ou blocos) de valores derivados de uma coluna contínua.|  
|*Ordenados*|Os valores da coluna definem um conjunto ordenado.|  
|*Cíclico*|Os valores da coluna definem um conjunto ordenado cíclico.|  
|*Probabilidade*|Os valores da coluna especificam uma probabilidade para as colunas contidas no [ClassifiedColumns](../collections/columns-element-assl.md) elemento do pai `ScalarMiningStructureColumn`.|  
|*Variance*|Os valores da coluna especificam uma variância para as colunas contidas no elemento `ClassifiedColumns` do pai `ScalarMiningStructureColumn`.|  
|*StdDev*|Os valores da coluna especificam um desvio padrão para as colunas contidas no elemento `ClassifiedColumns` do pai `ScalarMiningStructureColumn`.|  
|*ProbabilityVariance*|Os valores da coluna especificam uma probabilidade de variância para as colunas contidas no elemento `ClassifiedColumns` do pai `ScalarMiningStructureColumn`.|  
|*ProbabilityStdDev*|Os valores da coluna especificam uma probabilidade de desvio padrão para as colunas contidas no elemento `ClassifiedColumns` do pai `ScalarMiningStructureColumn`.|  
|*Suporte*|Os valores da coluna especificam informações de suporte para a coluna contida no elemento `ClassifiedColumns` do pai `ScalarMiningStructureColumn`. **Observação:** essa coluna é fornecida como parte do padrão para provedores de algoritmo de mineração de terceiros. **Observação:** fornecidos pela Microsoft algoritmos não têm nenhum uso para esta coluna. <br /><br /> para obter informações sobre a ferramenta de configuração e recursos adicionais.|  
|*Chave*|A coluna é uma coluna de chave. **Observação:** esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o `IsKey` é definido como `True`.|  
  
 Além desses valores padrão, os provedores de algoritmo incluídos de mineração [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] suporte os valores na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sequência de teclas*|A coluna é uma coluna de chave e os valores da coluna representam uma sequência de eventos. **Observação:** esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o `IsKey` é definido como `True`.|  
|*Chave de tempo*|A coluna é uma coluna de chave e os valores da coluna representam unidades de medição de tempo. **Observação:** esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o `IsKey` é definido como `True`.|  
|*Sequência*|Os valores da coluna representam uma sequência de eventos.|  
|*Hora*|Os valores da coluna representam unidades de medição de tempo.|  
  
 A enumeração que corresponde aos valores permitidos para `Content` no modelo de objeto AMO (Objetos de Gerenciamento de Análise) é <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ClassifiedColumns &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  