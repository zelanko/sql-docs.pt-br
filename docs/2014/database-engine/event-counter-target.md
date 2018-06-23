---
title: Destino do contador de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- synchronous event counter target [SQL Server extended events]
- targets [SQL Server extended events], synchronous event counter target
ms.assetid: 342e08d1-dcca-4a71-ae64-cb61b55b85bc
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 370835af2532a3602bbc5aa944b114ba8f7e61ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119170"
---
# <a name="event-counter-target"></a>Destino de contador de eventos
  O destino do contador de eventos conta todos os eventos ocorridos durante uma sessão de Eventos Estendidos. Com o uso do destino do contador de eventos, é possível obter informações sobre as características da carga de trabalho, sem adicionar a sobrecarga da coleção de eventos. Esse destino não tem nenhum parâmetro personalizável.  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino do contador de eventos a uma sessão de Eventos Estendidos, você deve incluir a instrução a seguir ao criar ou alterar uma sessão de evento:  
  
```  
ADD TARGET package0.event_counter  
```  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 Para examinar a saída do destino do contador de eventos, você pode usar a consulta a seguir, substituindo *session_name* pelo nome da sessão de evento:  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 O exemplo a seguir mostra o formato da saída de destino do contador de eventos.  
  
```  
<CounterTarget truncated = "0">  
  <Packages>  
    <Package name = "[package name]">  
      <Event name = "[event name]" count = "[number]" />  
    </Package>  
  </Packages>  
</CounterTarget>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
