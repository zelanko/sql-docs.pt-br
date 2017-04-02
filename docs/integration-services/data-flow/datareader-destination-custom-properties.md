---
title: "Propriedades personalizadas do destino DataReader | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Propriedades personalizadas do destino DataReader
  O destino DataReader tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino DataReader. Todas as propriedades, exceto **DataReader**, são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|DataReader|Cadeia de caracteres|O nome da classe do destino DataReader.|  
|FailOnTimeout|Booliano|Indica se deve haver falha na ocorrência de **ReadTimeout** . O valor padrão dessa propriedade é **False**.|  
|ReadTimeout|Integer|O número de milissegundos antes de um tempo limite. O valor padrão dessa propriedade é 30000 (30 segundos).|  
  
 A entrada e as colunas de entrada do destino DataReader não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [DataReader Destination](../../integration-services/data-flow/datareader-destination.md).  
  
## Consulte também  
 [Propriedades comuns](../Topic/Common%20Properties.md)  
  
  