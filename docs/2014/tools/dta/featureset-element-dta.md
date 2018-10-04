---
title: Elemento FeatureSet (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f489fba4c9ea113cffd608b496d04448399481a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191576"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|`string`, nenhum tamanho máximo.|  
|**Valores permitidos**|**IDX_IV**<br /> Índices e exibições indexadas.<br /><br /> **IDX**<br /> Somente índices.<br /><br /> **IV**<br /> Somente exibições indexadas.<br /><br /> **NCL_IDX**<br /> Somente índices não clusterizados<br /><br /> Use um desses valores com esse elemento.|  
|**Valor padrão**|**IDX**|  
|**Ocorrência**|Exigido uma vez para cada elemento `TuningOptions`, a menos que seja usado o elemento `DropOnlyMode`. Se `DropOnlyMode` é usado, você não pode usar `FeatureSet`. Estes elementos são mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
