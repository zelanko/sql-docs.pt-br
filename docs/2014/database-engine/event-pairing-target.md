---
title: Destino de emparelhamento de evento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
caps.latest.revision: 14
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e67507452104e8bef8d82d86e78c0ebbdf80609
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291332"
---
# <a name="event-pairing-target"></a>Destino de emparelhamento de evento
  O destino de emparelhamento de eventos efetua a correspondência entre dois eventos por meio de uma ou mais colunas de dados presentes em cada evento. Muitos eventos vêm em pares, por exemplo, aquisições de bloqueio e liberações de bloqueio. Após o emparelhamento de uma sequência de eventos, ambos são descartados. O descarte de conjuntos correspondidos facilita a detecção de aquisições de bloqueios que não foram liberados.  
  
 Com o uso de filtros no nível de evento, o destino de emparelhamento pode ser usado somente para capturar eventos que não correspondam aos critérios predefinidos.  
  
 Ao usar o destino de emparelhamento de evento, você pode escolher dois eventos que serão correspondidos, junto com uma sequência de colunas para executar a correspondência. Todas as colunas nessa sequência deverão ser do mesmo tipo.  
  
 A tabela a seguir descreve as opções disponíveis para configurar um emparelhamento de evento.  
  
|Opção|Valores permitidos|Description|  
|------------|--------------------|-----------------|  
|begin_event|Qualquer nome de evento presente na sessão atual.|O nome do evento que especifica o evento inicial em uma sequência emparelhada.|  
|end_event|Qualquer nome de evento presente na sessão atual.|O nome do evento que especifica o evento final em uma sequência emparelhada.|  
|begin_matching_columns|Uma lista delimitada por vírgula, ordenada por nomes de coluna.|As colunas em que a correspondência deve ser executada.|  
|end_matching_columns|Uma lista delimitada por vírgula, ordenada por nomes de coluna.|As colunas em que a correspondência deve ser executada.|  
|begin_matching_actions|Uma lista de ações ordenadas, delimitadas por vírgula.|As ações nas quais a correspondência deve ser executada.|  
|end_matching_actions|Uma lista de ações ordenadas, delimitadas por vírgula.|As ações nas quais a correspondência deve ser executada.|  
|respond_to_memory_pressure|Um dos valores seguintes:<br /><br /> 0 = Não responda.<br /><br /> 1 = Pare de adicionar novos órfãos à lista quando houver pressão de memória.|A resposta de destino a eventos de memória. Se definido como 1 e o servidor estiver com pouca memória, as informações não emparelhadas que estão sendo mantidas serão removidas.|  
|max_orphans||Especifica o número total de eventos ímpares que serão coletados no destino. Quando o limite é atingido, os eventos não emparelhados são removidos na base PEPS (primeiro a entrar, primeiro a sair). Padrão = 10,000.|  
  
 Todos os dados associados a um evento são capturados e armazenados para emparelhamento futuro. Além disso, dados adicionados por ações também são coletados. Os dados de evento coletados são armazenados na memória e, portanto, têm um limite finito. Esse limite é baseado na capacidade e na atividade do sistema. Em vez de usar a quantidade máxima de memória a ser usada como um parâmetro, a quantidade de memória usada terá como base os recursos disponíveis do sistema. Quando esses não estiverem disponíveis, os eventos não emparelhados que foram retidos serão cancelados. Se um evento não tiver sido emparelhado e for cancelado, o evento correspondente aparecerá como um evento não emparelhado.  
  
 O destino de emparelhamento serializa eventos não emparelhados em um formato XML. Esse formato não se adapta a nenhum esquema. O formato contém apenas dois tipos de elementos. O  **\<não emparelhados >** elemento é a raiz, seguida por um. **\<evento >** elemento para cada evento não emparelhando que está sendo controlado no momento. O  **\<evento >** elemento contém um atributo que contém o nome do evento não emparelhado.  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino de correspondência de par a uma sessão de Eventos Estendidos, você deve incluir a instrução a seguir ao criar ou alterar uma sessão de evento:  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 Isso deve ser seguido por uma instrução SET, para definir os eventos iniciais e finais e quais ações ou colunas devem ser correspondidas. O exemplo a seguir mostra a sintaxe de exemplo para corresponder o par dos eventos sqlserver.lock_acquired e sqlserver.lock_released.  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 Pra obter mais informações, consulte [Determinar quais consultas estão mantendo bloqueios](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md).  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 Para examinar a saída de destino da correspondência de par, você pode usar a consulta a seguir com a substituição de *session_name* pelo nome da sessão de evento.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 O exemplo a seguir mostra o formato de saída do destino do emparelhamento.  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
