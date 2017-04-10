---
title: "Elemento FeatureSet (DTA) | Microsoft Docs"
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
  - "Elemento FeatureSet"
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Elemento FeatureSet (DTA)
  Contém as estruturas físicas de design (índices ou exibições indexadas) que você gostaria que o Orientador de Otimização do Mecanismo de Banco de Dados usasse durante análise.  
  
## Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, nenhum tamanho máximo.|  
|**Valores permitidos**|**IDX_IV**<br /> Índices e exibições indexadas.<br /><br /> **IDX**<br /> Somente índices.<br /><br /> **IV**<br /> Somente exibições indexadas.<br /><br /> **NCL_IDX**<br /> Somente índices não clusterizados<br /><br /> Use um desses valores com esse elemento.|  
|**Valor padrão**|**IDX**|  
|**Ocorrência**|Necessário uma vez para cada elemento **TuningOptions**, a menos que o elemento **DropOnlyMode** seja usado. Se **DropOnlyMode** for usado, não será possível usar **FeatureSet**. Estes elementos são mutuamente exclusivos.|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  