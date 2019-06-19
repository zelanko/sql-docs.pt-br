---
title: Destino do Buffer de anel | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 920cc72a9d99da61575249559661c01826b0e89b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088954"
---
# <a name="ring-buffer-target"></a>Destino de buffer de anel
  O destino de buffer de anel mantém brevemente dados de eventos na memória. Esse destino pode gerenciar eventos de uma das duas maneiras possíveis.  
  
-   O primeiro modo é basicamente o FIFO (primeiro a entrar, primeiro a sair), no qual o evento mais antigo é descartado quando toda a memória alocada ao destino é usada. Nesse modo (o padrão), a opção occurrence_number é definida como 0.  
  
-   O segundo modo é o FIFO por evento, no qual um número especificado de eventos de cada tipo é mantido. Nesse modo, os eventos mais antigos de cada tipo são descartados quando toda a memória alocada ao destino é usada. Você pode configurar a opção occurrence_number para especificar o número de eventos de cada tipo a ser mantido.  
  
 A tabela a seguir descreve as opções disponíveis para configurar o destino de buffer de anel.  
  
|Opção|Valores permitidos|Descrição|  
|------------|--------------------|-----------------|  
|max_memory|Qualquer inteiro de 32 bits. Esse valor é opcional.|A quantidade máxima de memória, em kilobytes (KB), para usar. Os eventos existentes são descartados com base no limite atingido primeiro: max_event_limit ou max_memory. O valor máximo é 4194303 KB. Uma consideração cuidadosa deve ser feita antes de definir o tamanho do buffer de anel como limites no intervalo de GB, pois isso pode afetar outros consumidores de memória no SQL Server|  
|max_event_limit|Qualquer inteiro de 32 bits. Esse valor é opcional.|O número máximo de eventos mantidos no ring_buffer. Os eventos existentes são descartados com base no limite atingido primeiro: max_event_limit ou max_memory. Padrão = 1000.|  
|occurrence_number|Um dos valores seguintes:<br /><br /> 0 (o padrão) = O evento mais antigo é descartado quando toda a memória alocada ao destino é usada.<br /><br /> Qualquer inteiro de 32 bits = o número de eventos de cada tipo a ser mantido antes de ser descartado da base FIFO por evento.<br /><br /> <br /><br /> Esse valor é opcional.|O modo FIFO a ser usado e, se definido com um valor maior que 0, o número preferencial de eventos de cada tipo a ser mantido no buffer.|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino de buffer de anel a uma sessão de Eventos Estendidos, você deve incluir a instrução a seguir ao criar ou alterar uma sessão de evento:  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 Para examinar o destino do buffer de anel, você pode usar a consulta a seguir com a substituição de *session_name* pelo nome da sessão de evento.  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 O exemplo a seguir mostra o formato de saída do destino do buffer de anel.  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>Consulte também

- [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

