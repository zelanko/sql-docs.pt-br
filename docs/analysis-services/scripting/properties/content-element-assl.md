---
title: Conteúdo de elemento (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee3c1babd828463e8654280c421d616535aca88e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036457"
---
# <a name="content-element-assl"></a>Elemento Content (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve o conteúdo da coluna no [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Essa enumeração descreve o tipo de conteúdo representado por uma coluna da estrutura de mineração e pode ser estendida conforme necessário pelos provedores de algoritmo de mineração. Para obter mais informações sobre tipos de conteúdo, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../../analysis-services/data-mining/content-types-data-mining.md).  
  
 Os valores listados na tabela a seguir normalmente têm suporte em todos os provedores de algoritmo de mineração.  
  
|Value|Description|  
|-----------|-----------------|  
|*Discreto*|A coluna contém valores discretos.|  
|*Contínua*|Os valores para a coluna definem um conjunto contínuo de dados numéricos.|  
|*Dados discretos*|Os valores da coluna representam grupos (ou blocos) de valores derivados de uma coluna contínua.|  
|*ordenados*|Os valores da coluna definem um conjunto ordenado.|  
|*Cíclico*|Os valores da coluna definem um conjunto ordenado cíclico.|  
|*Probabilidade*|Os valores da coluna especificam uma probabilidade para as colunas contidas no [ClassifiedColumns](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md) elemento do pai **ScalarMiningStructureColumn**.|  
|*Variance*|Os valores da coluna especificam uma variância para as colunas contidas no **ClassifiedColumns** elemento do pai **ScalarMiningStructureColumn**.|  
|*StdDev*|Os valores da coluna especificam um desvio padrão para as colunas contidas no **ClassifiedColumns** elemento do pai **ScalarMiningStructureColumn**.|  
|*ProbabilityVariance*|Os valores da coluna especificam uma probabilidade de variância para as colunas contidas no **ClassifiedColumns** elemento do pai **ScalarMiningStructureColumn**.|  
|*ProbabilityStdDev*|Os valores da coluna especificam uma probabilidade de desvio padrão para as colunas contidas no **ClassifiedColumns** elemento do pai **ScalarMiningStructureColumn**.|  
|*Suporte*|Os valores da coluna especificam informações de suporte para a coluna contida no **ClassifiedColumns** elemento do pai **ScalarMiningStructureColumn**.<br /><br /> Observação: Esta coluna é fornecida como parte do padrão para provedores de algoritmo de mineração de terceiros. Não faça algoritmos fornecidos pela Microsoft usar desta coluna.|  
|*Chave*|A coluna é uma coluna de chave.<br /><br /> Observação: Esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o **IsKey** é definido como **True**.|  
  
 Além desses valores padrão, os provedores de algoritmo incluídos de mineração [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] suporte os valores na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|*Sequência de teclas*|A coluna é uma coluna de chave e os valores da coluna representam uma sequência de eventos.<br /><br /> Observação: Esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o **IsKey** é definido como **True**.|  
|*Chave de tempo*|A coluna é uma coluna de chave e os valores da coluna representam unidades de medição de tempo.<br /><br /> Observação: Esse tipo de conteúdo é aplicável somente às colunas de chave, no qual o **IsKey** é definido como **True**.|  
|*Sequência*|Os valores da coluna representam uma sequência de eventos.|  
|*Hora*|Os valores da coluna representam unidades de medição de tempo.|  
  
 A enumeração que corresponde aos valores permitidos para **conteúdo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ClassifiedColumns &#40;ASSL&#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
