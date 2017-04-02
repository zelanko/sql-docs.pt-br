---
title: "Elemento de servidor para configura&#231;&#227;o (DTA) | Microsoft Docs"
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
  - "Elemento Server"
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Elemento de servidor para configura&#231;&#227;o (DTA)
  Contém as informações de identificação para o servidor no qual você quer que o Orientador de Otimização do Mecanismo de Banco de Dados avalie uma configuração hipotética (especificada pelo elemento de **Configuração**).  
  
## Sintaxe  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Obrigatório uma vez por elemento de **Configuração**.|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Configuration &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
|**Elementos filho**|[Elemento Name para Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Elemento Database para Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## Comentários  
 Você pode especificar apenas um elemento de **servidor** para o elemento de **configuração**. Esse elemento tem o nome **ServerTypecomplexType** no [Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](http://go.microsoft.com/fwlink/?linkid=43100). Não confunda esse elemento de **servidor** com aquele que é o filho do elemento **DTAInput**. Para obter mais informações, consulte [Elemento de servidor &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## Exemplo  
 Para obter um exemplo de uso, consulte a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  