---
title: Elemento DropOnlyMode (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb4fae568cb1301d1407a2694f6a2e527b0b4243
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247786"
---
# <a name="droponlymode-element-dta"></a>Elemento DropOnlyMode (DTA)
  Especifica que o Orientador de Otimização do Mecanismo de Banco de Dados deve apenas considerar descartar índices, exibições indexadas ou partições existentes durante a sessão de ajuste. Nenhuma nova estrutura de design físico é considerada quando esta opção de ajuste é especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode usar apenas uma vez para cada `TuningOptions` elemento. Não pode ser usado se os elementos seguintes forem especificados no `TuningOptions` elemento:<br /><br /> [Elemento FeatureSet &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Elemento de particionamento &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> O [Elemento KeepExisting &#40;DTA&#41;](keepexisting-element-dta.md) é definido como **ALL**|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 A exemplo a seguir mostra a `TuningOptions` seção de um arquivo de entrada XML do Orientador de otimização de mecanismo de banco de dados onde o `DropOnlyMode` for especificado. Nesse exemplo a hora de ajuste é limitada a 24 horas (1440 minutos) e todos os índices clusterizados e não clusterizados existentes serão considerados para o descarte:  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
