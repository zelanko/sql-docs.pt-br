---
title: Elemento de particionamento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 379e5dae0c70278b7c0b576190faffea84c8fa19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019023"
---
# <a name="partitioning-element-dta"></a>Elemento de particionamento (DTA)
  Contém o esquema de particionamento que você gostaria que o Database Engine Tuning Advisor usasse durante a análise.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|`string`, nenhum tamanho máximo.|  
|**Valores permitidos**|**NONE**<br /> Sem particionamento<br /><br /> **FULL**<br /> Particionamento completo (Aprimora o desempenho.)<br /><br /> **ALIGNED**<br /> Somente o particionamento alinhado (Aprimora a capacidade de gerenciamento máxima).<br /><br /> Use apenas um desses valores com este elemento.<br /><br /> **ALIGNED** significa que na recomendação gerada pelo Database Engine Tuning Advisor cada índice proposto é particionado exatamente do mesmo modo da tabela subjacente para a qual o índice está definido. Índices não clusterizados em uma exibição indexada são alinhados com a exibição indexada.|  
|**Valor padrão**|**NONE**|  
|**Ocorrência**|Necessário uma vez para o elemento `TuningOptions`, a menos que o elemento `DropOnlyMode` seja usado. Se `DropOnlyMode` é usado, você não pode usar `Partitioning`. Estes elementos são mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  