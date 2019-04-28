---
title: Elemento FeatureSet (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4bf6fac03eab1e096c0ac5dc63285c11bd3f114
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735749"
---
# <a name="featureset-element-dta"></a>Elemento FeatureSet (DTA)
  Contém as estruturas físicas de design (índices ou exibições indexadas) que você gostaria que o Orientador de Otimização do Mecanismo de Banco de Dados usasse durante análise.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|`string`, nenhum tamanho máximo.|  
|**Valores permitidos**|**IDX_IV**<br /> Índices e exibições indexadas.<br /><br /> **IDX**<br /> Somente índices.<br /><br /> **IV**<br /> Somente exibições indexadas.<br /><br /> **NCL_IDX**<br /> Somente índices não clusterizados<br /><br /> Use um desses valores com esse elemento.|  
|**Valor padrão**|**IDX**|  
|**Ocorrência**|Exigido uma vez para cada elemento `TuningOptions`, a menos que seja usado o elemento `DropOnlyMode`. Se `DropOnlyMode` for usado, você não poderá usar o `FeatureSet`. Estes elementos são mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
