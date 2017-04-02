---
title: "Elemento Banner (ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "elemento de faixa"
  - "formato de arquivo de saída XML [ssbdiagnose], elemento de faixa"
  - "ssbdiagnose"
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Elemento Banner (ssbdiagnose)
  Identifica qual utilitário gerou o arquivo XML de saída **ssbdiagnose**.  
  
## Sintaxe  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## Atributos do elemento  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**title**|Identifica qual utilitário gerou o arquivo de saída XML **ssbdiagnose**.|  
|**product**|Identifica qual produto gerou o arquivo de saída XML **ssbdiagnose**.|  
|**version**|Identifica qual versão do utilitário gerou o arquivo de saída XML.|  
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Ocorre uma vez por arquivo XML de saída **ssbdiagnose**.|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos filho**|Nenhum.|  
  
## Exemplo  
 Este é um exemplo de um elemento Banner.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## Consulte também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  