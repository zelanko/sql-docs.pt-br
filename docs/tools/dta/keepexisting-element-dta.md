---
title: Elemento KeepExisting (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 50741d36bfd0dd3b9f566954d1ef53b86be14609
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307640"
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
  
|Característica|DESCRIÇÃO|  
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
  
  
