---
title: "Elemento KeepExisting (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Elemento KeepExisting (DTA)"
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Elemento KeepExisting (DTA)
  Especifica as estruturas físicas de design (índices, exibições indexadas ou particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve reter ao gerar sua recomendação.  
  
## Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, o limite de tamanho é imposto pelo servidor.|  
|**Valores permitidos**|**NONE**<br /> Não existe nenhuma estrutura.<br /><br /> **ALL**<br /> Todas as estruturas existentes.<br /><br /> **ALIGNED**<br /> Todas as estruturas alinhadas por partição.<br /><br /> **CL_IDX**<br /> Todos os índices clusterizados em tabelas<br /><br /> **IDX**<br /> Todos os índices clusterizados e não cluster em tabelas<br /><br /> Use apenas um desses valores com este elemento.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Opcional. Pode-se usar apenas uma vez para cada elemento de **TuningOptions** .|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  