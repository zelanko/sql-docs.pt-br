---
title: Elemento KeepExisting (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eca536eb6ab1355f041571f451c2e1b591541fe5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="keepexisting-element-dta"></a>Elemento KeepExisting (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica as estruturas físicas de design (índices, exibições indexadas ou particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve reter ao gerar sua recomendação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, o limite de tamanho é imposto pelo servidor.|  
|**Valores permitidos**|**NONE**<br /> Não existe nenhuma estrutura.<br /><br /> **ALL**<br /> Todas as estruturas existentes.<br /><br /> **ALIGNED**<br /> Todas as estruturas alinhadas por partição.<br /><br /> **CL_IDX**<br /> Todos os índices clusterizados em tabelas<br /><br /> **IDX**<br /> Todos os índices clusterizados e não cluster em tabelas<br /><br /> Use apenas um desses valores com este elemento.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode-se usar apenas uma vez para cada elemento de **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
