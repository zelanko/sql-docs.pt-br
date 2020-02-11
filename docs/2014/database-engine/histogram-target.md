---
title: Destino do histograma | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a584311061a24d674eed114f37d9cbbbda43909
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064696"
---
# <a name="histogram-target"></a>Destino do histograma
  O destino do histograma agrupa ocorrências de um tipo de evento específico com base nos dados do evento. Os agrupamentos de eventos são contados com base em uma coluna de evento ou ação especificada. Você pode usar o destino do histograma para solucionar problemas de desempenho. Ao identificar quais eventos ocorrem mais frequentemente, você pode localizar "pontos de acesso" que indicam uma causa potencial de um problema de desempenho.  
  
 A tabela a seguir descreve as opções que podem ser usadas para configurar o destino do histograma.  
  
|Opção|Valores permitidos|DESCRIÇÃO|  
|------------|--------------------|-----------------|  
|slots|Qualquer valor inteiro. Esse valor é opcional.|Um valor especificado pelo usuário que indica o número máximo de agrupamentos a serem retidos. Quando esse valor é atingido, novos eventos que não pertencem aos grupos existentes são ignorados.<br /><br /> Observe que para aprimorar o desempenho, o número de slot é arredondado para a próxima potência de 2.|  
|filtering_event_name|Qualquer evento presente na sessão de Eventos Estendidos. Esse valor é opcional.|Um valor especificado pelo usuário usado para identificar uma classe de eventos. Apenas instâncias do evento especificado são particionadas. Todos os outros eventos são ignorados.<br /><br /> Se você especificar esse valor, deverá usar o formato: *package_name*.*event_name*, por exemplo, `'sqlserver.checkpoint_end'`. Você pode identificar o nome do pacote usando a seguinte consulta:<br /><br /> Selecione p.name, se. event_name<br />DE sys. dm_xe_session_events se<br />INGRESSAr em sys. dm_xe_packages p<br />EM se_event_package_guid = p. GUID<br />ORDENAr por p.name, se. event_name<br /><br /> <br /><br /> Se você não especificar o valor filtering_event_name, source_type deverá ser definido como 1 (o padrão).|  
|source_type|O tipo de objeto no qual o bucket é baseado. Esse valor é opcional e, se não for especificado, terá 1 como valor padrão.|Pode ter um dos seguintes valores:<br /><br /> 0 para um evento<br /><br /> 1 para uma ação|  
|source|Coluna do evento ou nome da ação.|A coluna do evento ou o nome da ação usado como a fonte de dados.<br /><br /> Quando especificar uma coluna de evento para origem, você deverá especificar uma coluna a partir do evento usado para o valor filtering_event_name. Para identificar as colunas potenciais, use a consulta a seguir:<br /><br /> Selecione o nome em sys. dm_xe_object_columns<br />EM que object_name =\<' eventname> '<br />E column_type! = ' ReadOnly '<br /><br /> Quando você especificar uma coluna de evento para origem, não será necessário incluir o nome do pacote no valor da origem.<br /><br /> Quando especificar um nome de ação para origem, você deverá usar uma das ações configuradas para coleta na sessão do evento para a qual esse destino está sendo usado. Para localizar valores potenciais para o nome de ação, você pode consultar a coluna action_name da exibição sys.dm_xe_sesssion_event_actions.<br /><br /> Se estiver usando um nome de ação como a fonte de dados, você deverá especificar o valor de origem usando o formato: *package_name*.*action_name*.|  
  
 O exemplo a seguir demonstra, em um nível alto, como o destino do histograma coleta dados. Neste exemplo, você deseja usar o destino do histograma para contar quantas esperas de cada tipo ocorreram. Para fazer isso, você deve especificar as seguintes opções ao definir o destino do histograma:  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0 (porque wait_type é uma coluna de evento)  
  
 No cenário do exemplo, os dados a seguir são registrados para a origem de wait_type.  
  
|Nome do evento de filtragem|Valor da coluna de origem|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|rede|  
|wait_info|rede|  
|wait_info|sleep|  
  
 Os valores de tipo de espera seriam categorizados em três slots, com os valores e as contagens de slot a seguir:  
  
|Valor|Contagem de slot|  
|-----------|----------------|  
|file_io|2|  
|rede|2|  
|sleep|1|  
  
 O destino do histograma retém apenas dados de eventos da fonte especificada. Em alguns casos, os dados de eventos podem ser muito grandes para serem retidos completamente; nesse caso, os dados são truncados. Quando os dados de eventos são truncados, o número de bytes é registrado e exibido como saída XML.  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino do histograma a uma sessão de Eventos Estendidos, você deve incluir as seguintes instruções ao criar ou alterar uma sessão de evento, de acordo com o tipo de destino desejado:  
  
```  
ADD TARGET package0.histogram  
```  
  
 Você pode usar a instrução SET instrução para definir as várias opções. O exemplo a seguir mostra a adição do destino do histograma, em que os dados do evento sqlserver.checkpoint_end são coletados.  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 Para obter mais informações, consulte [Localizar os objetos que detêm a maioria dos bloqueios](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)e [Monitorar a atividade do sistema usando Eventos Estendidos](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  
  
## <a name="reviewing-the-target-output"></a>Revisando a saída de destino  
 O destino do histograma serializa os dados para um programa de chamada ou para um procedimento em formato XML. A saída do destino não está de acordo com nenhum esquema.  
  
 Para examinar a saída de destino do histograma, você pode usar a consulta a seguir com a substituição de *session_name* pelo nome da sessão de evento.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 O exemplo a seguir ilustra o formato de saída de destino do histograma.  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
