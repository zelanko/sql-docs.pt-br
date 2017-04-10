---
title: "Classe de evento PreConnect:Starting | Microsoft Docs"
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
  - "Classe de evento PreConnect:Starting"
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Classe de evento PreConnect:Starting
  A classe de evento PreConnect:Starting indica quando um gatilho LOGON ou a função classificador do Administrador de Recursos inicia a execução.  
  
## Colunas de dados da classe de evento PreConnect:Starting  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|Não|  
|SPID|**int**|O ID de processo de servidor que dispara este evento.|12|Sim|  
|EventSubClass|**int**|1 para a função de classificador definida pelo usuário.|21|Sim|  
|StartTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|14|Sim|  
|ObjectID|**int**|A ID do objeto do classificador definido pelo usuário.|22|Sim|  
|ObjectName|**nvarchar(256)**|O nome de duas partes da função de classificador definida pelo usuário. Por exemplo, dbo.classifier.|34|Sim|  
  
## Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Classe de evento PreConnect:Completed](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)  
  
  