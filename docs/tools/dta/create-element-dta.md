---
title: "Criar elemento (DTA) | Microsoft Docs"
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
  - "Criar elemento (DTA)"
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Criar elemento (DTA)
  Contém informações sobre estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário.  
  
## Sintaxe  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Necessária uma vez para cada tipo de estrutura física de design (estruturas de índices, estatísticas ou de heap).|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Recommendation &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**Elementos filho**|[Elemento Index &#40;DTA&#41;](../../tools/dta/index-element-dta.md)<br /><br /> Elemento **Statistics** (veja o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](http://schemas.microsoft.com/sqlserver/) para obter informações)<br /><br /> Elemento **Heap** (veja o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](http://schemas.microsoft.com/sqlserver/) para obter informações)|  
  
## Comentários  
 Esse elemento tem o nome **CreateTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. É usado criar estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário. Não confunda esse elemento **Create** com os outros tipos que podem ser usados para criar exibições (**CreateViewType**) ou particionamento (**CreatePType**). Consulte o [esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](http://schemas.microsoft.com/sqlserver/) para obter informações sobre esses outros tipos de elementos **Create**.  
  
## Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  