---
title: Destinos para eventos estendidos no SQL Server | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47c64144-4432-4778-93b5-00496749665b
caps.latest.revision: "2"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de12dd7f28eb427429ecc0260ce37707ff0cec99
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="targets-for-extended-events-in-sql-server"></a>Destinos de eventos estendidos no SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artigo explica quando e como usar o destino package0 em eventos estendidos no SQL Server. Para cada destino, este artigo explica:

- Suas habilidades em coletar e relatar os dados enviados por eventos.
- Seus parâmetros, exceto quando o parâmetro é autoexplicativo.


#### <a name="xquery-example"></a>Exemplo do XQuery


A [seção ring_buffer](#h2_target_ring_buffer) inclui um exemplo de como usar o [XQuery no Transact-SQL](../../xquery/xquery-language-reference-sql-server.md) para copiar uma cadeia de caracteres XML em um conjunto de linhas relacional.


### <a name="prerequisites"></a>Pré-requisitos


- Esteja familiarizado com os conceitos básicos dos eventos estendidos, conforme descrito em [Início Rápido: Eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md).


- Instalou uma versão recente do utilitário SQL Server Management Studio (SSMS.exe) atualizado com frequência. Para obter detalhes, confira:
    - [Baixar o SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)


- No SSMS.exe, saiba como usar o **Pesquisador de Objetos** para clicar com o botão direito do mouse no nó de destino na sessão de evento para [facilitar a exibição dos dados de saída](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
    - Os dados do evento são capturados como uma cadeia de caracteres XML. Ainda neste artigo, os dados são exibidos em linhas relacionais. O SSMS foi usado para exibir os dados, que foram copiados e colados neste artigo.
    - A técnica alternativa do T-SQL para gerar conjuntos de linhas do XML é explicada na [seção ring_buffer](#h2_target_ring_buffer). Ela envolve o XQuery.



## <a name="parameters-actions-and-fields"></a>Parâmetros, ações e campos


No Transact-SQL, a instrução [CREATE EVENT SESSION](~/t-sql/statements/create-event-session-transact-sql.md) é fundamental para os eventos estendidos. Para gravar a instrução, geralmente, você precisa de uma lista e descrição dos seguintes:

- Os campos associados ao evento escolhido.
- Os parâmetros associados ao destino escolhido.

Instruções SELECT que retornam listas desse tipo das exibições do sistema estão disponíveis para cópia no seguinte artigo, seção C:

- [Seleções e junções em exibições do sistema dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)
    - Campos[C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT de um evento.
    - Parâmetros[C.6](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_6_parameters_targets) SELECT de um destino.
    - Ações[C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT.


Você pode ver os parâmetros, os campos e as ações usadas no contexto de uma instrução CREATE EVENT SESSION real, [neste link](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_B_2_TSQL_perspective).



<a name="h2_target_etw_classic_sync_target"></a>

## <a name="etwclassicsynctarget-target"></a>destino etw_classic_sync_target


Os eventos estendidos do SQL Server podem interoperar com o ETW (Rastreamento de Eventos para Windows) para monitorar a atividade do sistema. Para obter mais informações, consulte:

- [Destino do rastreamento de eventos do Windows](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [Monitorar a atividade do sistema usando Eventos Estendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)


Esse destino ETW processa os dados recebidos *de forma síncrona* , enquanto a maioria dos destinos os processa *de forma assíncrona*.


<a name="h2_target_event_counter"></a>

## <a name="eventcounter-target"></a>destino event_counter


O destino event_counter apenas conta quantas vezes cada evento especificado ocorre.


Ao contrário da maioria dos outros destinos:

- Event_counter não tem parâmetros.


- Ao contrário da maioria dos destinos, o destino event_counter processa os dados recebidos *de forma síncrona* .
    - O modo síncrono é aceitável para o event_counter simples, pois ele envolve muito pouco processamento.
    - O mecanismo de banco de dados será desconectado de um destino que está muito lento e que, portanto, ameaça reduzir o desempenho do mecanismo de banco de dados. Esse é um dos motivos pelos quais a maioria dos destinos realiza um processo *assíncrono*.


#### <a name="example-output-captured-by-eventcounter"></a>Saída de exemplo capturada por event_counter


```
package_name   event_name         count
------------   ----------         -----
sqlserver      checkpoint_begin   4
```


Veja a seguir CREATE EVENT SESSION, que gerou os resultados anteriores. Para este teste, na cláusula EVENT...WHERE, o campo **package0.counter** foi usado para interromper a contagem depois de a contagem atingir 4.


```tsql
CREATE EVENT SESSION [event_counter_1]
    ON SERVER 
    ADD EVENT sqlserver.checkpoint_begin   -- Test by issuing CHECKPOINT; statements.
    (
        WHERE ([package0].[counter] <= (4))   -- A predicate filter.
    )
    ADD TARGET package0.event_counter
    WITH
    (
        MAX_MEMORY = 4096 KB,
        MAX_DISPATCH_LATENCY = 3 SECONDS
    );
```



<a name="h2_target_event_file"></a>

## <a name="eventfile-target"></a>destino event_file


O destino **event_file** grava a saída da sessão de evento do buffer em um arquivo de disco:


- O parâmetro *filename=* é especificado na cláusula ADD TARGET.
    - .**.xel** deve ser a extensão do arquivo.


- O nome de arquivo escolhido é usado pelo sistema como um prefixo ao qual é acrescentado um inteiro longo baseado em data e hora, seguido da extensão .xel.


#### <a name="create-event-session-with-eventfile-target"></a>CREATE EVENT SESSION com o destino **event_file**


Veja a seguir, CREATE EVENT SESSION, que usamos para o teste. Uma das cláusulas ADD TARGET especifica um event_file.


```tsql
CREATE EVENT SESSION [locks_acq_rel_eventfile_22]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION (sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION(sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.event_file
    (
        SET     filename=N'C:\Junk\locks_acq_rel_eventfile_22-.xel'
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=10 SECONDS
    );
```


#### <a name="sysfnxefiletargetreadfile-function"></a>função sys.fn_xe_file_target_read_file


O destino event_file armazena os dados recebidos em um formato binário que não é legível por humanos. O Transact-SQL pode relatar o conteúdo do arquivo .xel usando SELECT FROM na função [**sys.fn_xe_file_target_read_file**](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md) .


Para o SQL Server **2016** e posterior, o T-SQL SELECT a seguir relatou os dados. O sufixo *.xel no 


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            null, null, null)  AS f;
```


Para o SQL Server **2014**, uma instrução SELECT semelhante à seguinte relatará os dados. Após o SQL Server 2014, os arquivos .xem não são mais usados.


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            'C:\junk\metafile.xem',
            null, null)  AS f;
```


Evidentemente, você também pode usar a interface do usuário do SSMS manualmente para ver os dados do .xel:


#### <a name="data-stored-in-the-eventfile-target"></a>Dados armazenados no destino event_file


Veja a seguir o relatório de SELECT em **sys.fn_xe_file_target_read_file**, no SQL Server 2016.


```
module_guid                            package_guid                           object_name     event_data                                                                                                                                                                                                                                                                                          file_name                                                      file_offset
-----------                            ------------                           -----------     ----------                                                                                                                                                                                                                                                                                          ---------                                                      -----------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_acquired   <event name="lock_acquired" package="sqlserver" timestamp="2016-08-07T20:13:35.827Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_released   <event name="lock_released" package="sqlserver" timestamp="2016-08-07T20:13:35.832Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
```



<a name="h2_target_histogram"></a>

## <a name="histogram-target"></a>destino de histograma


O destino de **histograma** é mais elaborado que o destino event_counter. O histograma pode fazer o seguinte:

- Contar as ocorrências de vários itens separadamente.
- Contar as ocorrências de diferentes tipos de itens:
    - Campos de evento.
    - Ações.


O parâmetro **source_type** é o segredo para controlar o destino de histograma:

- **source_type=0** – Significa coleta de dados de *campos de evento*).
- **source_type=1** – Significa coleta de dados de *ações*.
    - 1 é o padrão.


O parâmetro “slots” padrão é 256. Se você atribuir outro valor, o valor será arredondado para a próxima potência de 2.

- Por exemplo, slots=59 será arredondado para =64.


### <a name="action-example-for-histogram"></a>Exemplo de*ação* para histograma


Na cláusula TARGET...SET, a instrução Transact-SQL CREATE EVENT SESSION a seguir especifica a atribuição de parâmetro de destino **source_type=1**. 1 significa que o destino de histograma acompanha uma ação.

No exemplo atual, a oferta da cláusula EVENT...ACTION ocorre para oferecer apenas uma ação para o destino a ser escolhido, ou seja, **sqlos.system_thread_id**. Na cláusula TARGET...SET, vemos a atribuição **source=N'sqlos.system_thread_id'** .

- Para acompanhar mais de uma ação de origem, você pode adicionar um segundo destino de histograma à instrução CREATE EVENT SESSION.


```tsql
CREATE EVENT SESSION [histogram_lockacquired]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
        (
        ACTION
            (
            sqlos.system_thread_id
            )
        )
    ADD TARGET package0.histogram
        (
        SET
            filtering_event_name=N'sqlserver.lock_acquired',
            slots=(16),
            source=N'sqlos.system_thread_id',
            source_type=1
        )
    WITH
        (
        <.... (For brevity, numerous parameter assignments generated by SSMS.exe are not shown here.) ....>
        );
```


 Os dados a seguir foi capturados. Os valores na coluna **value** eram system_thread_id. Por exemplo, um total de 236 bloqueios foram feitos no thread 6540.


```
value   count
-----   -----
 6540     236
 9308      91
 9668      74
10144      49
 5244      44
 2396      28
```


#### <a name="select-to-discover-available-actions"></a>Use SELECT para descobrir as ações disponíveis


A instrução [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT pode encontrar as ações disponíveis no sistema para serem especificadas na instrução CREATE EVENT SESSION. Na cláusula WHERE, primeiro você editará o filtro **o.name LIKE** para que ele corresponda às ações de interesse.


Veja a seguir um conjunto de linhas de exemplo retornado por C.3 SELECT. A ação **system_thread_id** é vista na segunda linha.


```
Package-Name   Action-Name                 Action-Description
------------   -----------                 ------------------
package0       collect_current_thread_id   Collect the current Windows thread ID
sqlos          system_thread_id            Collect current system thread ID
sqlserver      create_dump_all_threads     Create mini dump including all threads
sqlserver      create_dump_single_thread   Create mini dump for the current thread
```


### <a name="event-field-example-for-histogram"></a>Exemplo de *campo* de evento para histograma


O exemplo a seguir define **source_type=0**. O valor atribuído a **source=** é um campo de evento (não uma ação).



```tsql
CREATE EVENT SESSION [histogram_checkpoint_dbid]
    ON SERVER 
    ADD EVENT  sqlserver.checkpoint_begin
    ADD TARGET package0.histogram
    (
    SET
        filtering_event_name = N'sqlserver.checkpoint_begin',
        source               = N'database_id',
        source_type          = (0)
    )
    WITH
    ( <....> );
```


Os dados a seguir foram capturados pelo destino de histograma. Os dados mostram que o banco de dados ID=5 apresentou sete eventos checkpoint_begin.


```
value   count
-----   -----
5       7
7       4
6       3
```


#### <a name="select-to-discover-available-fields-on-your-chosen-event"></a>Usar a instrução SELECT para descobrir os campos disponíveis no evento escolhido


A instrução [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT mostra os campos de evento que podem ser escolhidos. Primeiro, você editará o filtro **o.name LIKE** para que ele tenha o nome do evento escolhido.


O conjunto de linhas a seguir foi retornado pela instrução C.4 SELECT. O conjunto de linhas mostra que database_id é o único campo no evento checkpoint_begin que pode fornecer valores para o destino de histograma.


```
Package-Name   Event-Name         Field-Name   Field-Description
------------   ----------         ----------   -----------------
sqlserver      checkpoint_begin   database_id  NULL
sqlserver      checkpoint_end     database_id  NULL
```


<a name="h2_target_pair_matching"></a>

## <a name="pairmatching-target"></a>destino pair_matching


O destino pair_matching permite detectar eventos de início que ocorrem sem um evento de término correspondente. Por exemplo, isso poderá ser um problema quando ocorrer um evento lock_acquired, mas nenhum evento lock_released correspondente ocorrer a seguir de forma oportuna.


O sistema não faz a correspondência automática de eventos de início e término. Em vez disso, você explica a correspondência para o sistema na instrução CREATE EVENT SESSION. Quando um evento de início e término forem correspondentes, o par será descartado para que todos possam se concentrar nos eventos de início não correspondentes.


#### <a name="finding-matchable-fields-for-the-start-and-end-event-pair"></a>Encontrando campos que podem ser correspondentes no par de eventos de início e término


Com a instrução [C.4 SELECT](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields), vemos no conjunto de linhas a seguir que há aproximadamente 16 campos para o evento lock_acquired. O conjunto de linhas exibido aqui foi dividido manualmente para mostrar de quais campos nosso exemplo fez a correspondência. Alguns campos seriam inúteis para tentar uma correspondência, como na **duração** de ambos os eventos.


```
Package-Name   Event-Name   Field-Name               Field-Description
------------   ----------   ----------               -----------------
sqlserver   lock_acquired   database_name            NULL
sqlserver   lock_acquired   mode                     NULL
sqlserver   lock_acquired   resource_0               The ID of the locked object, when lock_resource_type is OBJECT.
sqlserver   lock_acquired   resource_1               NULL
sqlserver   lock_acquired   resource_2               The ID of the lock partition, when lock_resource_type is OBJECT, and resource_1 is 0.
sqlserver   lock_acquired   transaction_id           NULL

sqlserver   lock_acquired   associated_object_id     The ID of the object that requested the lock that was acquired.
sqlserver   lock_acquired   database_id              NULL
sqlserver   lock_acquired   duration                 The time (in microseconds) between when the lock was requested and when it was canceled.
sqlserver   lock_acquired   lockspace_nest_id        NULL
sqlserver   lock_acquired   lockspace_sub_id         NULL
sqlserver   lock_acquired   lockspace_workspace_id   NULL
sqlserver   lock_acquired   object_id                The ID of the locked object, when lock_resource_type is OBJECT. For other lock resource types it will be 0
sqlserver   lock_acquired   owner_type               NULL
sqlserver   lock_acquired   resource_description     The description of the lock resource. The description depends on the type of lock. This is the same value as the resource_description column in the sys.dm_tran_locks view.
sqlserver   lock_acquired   resource_type            NULL
```


### <a name="example-of-pairmatching"></a>Exemplo de pair_matching


A instrução CREATE EVENT SESSION a seguir especifica dois eventos e dois destinos. O destino pair_matching especifica dois conjuntos de campos para corresponder os eventos em pares. A sequência de campos delimitados por vírgula atribuída a **begin_matching_columns =** e **end_matching_columns =** deve ser a mesma. Não são permitidas guias nem novas linhas entre os campos mencionados no valor delimitado por vírgula, embora o uso de espaços seja permitido.

Para restringir os resultados, primeiro usamos a instrução SELECT em sys.objects para encontrar o object_id de nossa tabela de teste. Adicionamos um filtro à ID da cláusula EVENT...WHERE.


```tsql
CREATE EVENT SESSION [pair_matching_lock_a_r_33]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.pair_matching
    (
        SET
            begin_event = N'sqlserver.lock_acquired',
            begin_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            end_event = N'sqlserver.lock_released',
            end_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            respond_to_memory_pressure = (1)
    )
    WITH
    (
        MAX_MEMORY = 8192 KB,
        MAX_DISPATCH_LATENCY = 15 SECONDS
    );
```


Para testar a sessão de evento, propositadamente impedimos a liberação dos bloqueios adquiridos. Fizemos isso nas seguintes etapas do T-SQL:

1. BEGIN TRANSACTION.
2. UPDATE MyTable....
3. Só emitimos uma instrução COMMIT TRANSACTION depois de examinarmos os destinos.
4. Posteriormente, após os testes, emitimos uma instrução COMMIT TRANSACTION.


O destino simples **event_counter** forneceu as linhas de saída a seguir. Como 52-50=2, o resultado informa que deveremos ver dois eventos lock_acquired não emparelhados ao examinarmos a saída do destino correspondente ao par.


```
package_name   event_name      count
------------   ----------      -----
sqlserver      lock_acquired   52
sqlserver      lock_released   50
```


O destino **pair_matching** forneceu a saída a seguir. Como sugerido pela saída de event_counter, na verdade, vemos duas linhas lock_acquired. O fato de que vemos essas linhas significa que esses dois eventos lock_acquired não são emparelhados.


```
package_name   event_name      timestamp                     database_name   duration   mode   object_id   owner_type   resource_0   resource_1   resource_2   resource_description   resource_type   transaction_id
------------   ----------      ---------                     -------------   --------   ----   ---------   ----------   ----------   ----------   ----------   --------------------   -------------   --------------
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          S      370100359   Transaction  370100359    3            0            [INDEX_OPERATION]      OBJECT          34126
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          IX     370100359   Transaction  370100359    0            0                                   OBJECT          34126
```


As linhas dos eventos lock_acquired não emparelhados podem incluir o texto T-SQL, ou **sqlserver.sql_text**, que usou os bloqueios. Mas não queríamos sobrecarregar a exibição.


<a name="h2_target_ring_buffer"></a>

## <a name="ringbuffer-target"></a>destino ring_buffer


O destino ring_buffer é útil para testes de eventos rápidos e simples. Quando você interrompe a sessão de evento, a saída armazenada é descartada.

Nesta seção de ring_buffer, também vamos mostrar como é possível usar a implementação do Transact-SQL do XQuery para copiar o conteúdo XML do ring_buffer em um conjunto de linhas relacional mais legível.


#### <a name="create-event-session-with-ringbuffer"></a>CREATE EVENT SESSION com ring_buffer


Não há nada de especial nessa instrução CREATE EVENT SESSION, que usa o destino ring_buffer.


```tsql
CREATE EVENT SESSION [ring_buffer_lock_acquired_4]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET collect_resource_description=(1)

        ACTION(sqlserver.database_name)

        WHERE
        (
            [object_id]=(370100359)  -- ID of MyTable
            AND
            sqlserver.database_name='InMemTest2'
        )
    )
    ADD TARGET package0.ring_buffer
    (
        SET max_events_limit=(98)
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=3 SECONDS
    );
```


### <a name="xml-output-received-for-lockacquired-by-ringbuffer"></a>Saída XML recebida para lock_acquired por ring_buffer


Quando é recuperado por uma instrução SELECT, o conteúdo está na forma de uma cadeia de caracteres XML. A cadeia de caracteres XML que foi armazenada pelo destino ring_buffer em nossos testes é mostrada a seguir. No entanto, para resumir a exibição XML a seguir, todos os elementos foram apagados, exceto dois elementos &#x3c;event&#x3e;. Além disso, em cada &#x3c;event&#x3e;, diversos elementos &#x3c;data&#x3e; estranhos foram excluídos.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="6" eventCount="6" droppedCount="0" memoryUsed="1032">
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:53.987Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111030</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:56.012Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111039</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
</RingBufferTarget>
```


Para ver o XML anterior, você pode emitir a instrução SELECT a seguir enquanto a sessão de evento está ativa. Os dados XML ativos são recuperados da exibição do sistema **sys.dm_xe_session_targets**.


```tsql
SELECT
        CAST(LocksAcquired.TargetXml AS XML)  AS RBufXml,
    INTO
        #XmlAsTable
    FROM
        (
        SELECT
                CAST(t.target_data AS XML)  AS TargetXml
            FROM
                     sys.dm_xe_session_targets  AS t
                JOIN sys.dm_xe_sessions         AS s

                    ON s.address = t.event_session_address
            WHERE
                t.target_name = 'ring_buffer'
                AND
                s.name        = 'ring_buffer_lock_acquired_4'
        )
            AS LocksAcquired;


SELECT * FROM #XmlAsTable;
```


### <a name="xquery-to-see-the-xml-as-a-rowset"></a>XQuery para ver o XML como um conjunto de linhas


Para ver o XML anterior como um conjunto de linhas relacional, continue após a instrução SELECT anterior emitindo o comando T-SQL a seguir. As linhas com comentários explicam cada um dos usos do XQuery.


```tsql
SELECT
         -- (A)
         ObjectLocks.value('(@timestamp)[1]',
            'datetime'     )  AS [OccurredDtTm]

        -- (B)
        ,ObjectLocks.value('(data[@name="mode"]/text)[1]',
            'nvarchar(32)' )  AS [Mode]

        -- (C)
        ,ObjectLocks.value('(data[@name="transaction_id"]/value)[1]',
            'bigint' )  AS [TxnId]

        -- (D)
        ,ObjectLocks.value('(action[@name="database_name" and @package="sqlserver"]/value)[1]',
            'nvarchar(128)')  AS [DatabaseName]
    FROM
        #TableXmlCell
    CROSS APPLY
        -- (E)
        TargetDateAsXml.nodes('/RingBufferTarget/event[@name="lock_acquired"]')  AS T(ObjectLocks);
```


#### <a name="xquery-notes-from-preceding-select"></a>Observações do XQuery da instrução SELECT anterior


(A)
- timestamp= valor do atributo, no elemento &#x3c;event&#x3e;.
- O constructo “(...)[1]” garante apenas um valor retornado por iteração, já que essa é uma limitação necessária do método .value() do XQuery de colunas e variável do tipo de dados XML.


(B)
- Valor interno do elemento &#x3c;text&#x3e; em um elemento &#x3c;data&#x3e; que tem seu atributo name= igual a “mode”.


(C)
- Valor interno do elemento &#x3c;value&#x3e; em um elemento &#x3c;data&#x3e; que tem seu atributo name= igual a “transaction_id”.


(D)
- &#x3c;event&#x3e; contém &#x3c;action&#x3e;.
- &#x3c;action&#x3e; com o atributo name= igual a “database_name” e o atributo package= igual a “sqlserver” (não “package0”) obtém o valor interno do elemento &#x3c;value&#x3e;.


(E)
- C.A. faz com que o processamento se repita para cada elemento &#x3c;event&#x3e; individual que tem o atributo name= igual a “lock_acquired”.
- Isso se aplica ao XML retornado pela cláusula FROM anterior.


#### <a name="output-from-xquery-select"></a>Saída do XQuery SELECT


Veja a seguir o conjunto de linhas gerado pelo T-SQL anterior que inclui o XQuery.


```
OccurredDtTm              Mode    DatabaseName
------------              ----    ------------
2016-08-05 23:59:53.987   SCH_S   InMemTest2
2016-08-05 23:59:56.013   SCH_S   InMemTest2
```



## <a name="xevent-net-namespaces-and-cx23"></a>Namespaces XEvent .NET e C&#x23;


Package0 tem mais dois destinos, mas eles não podem ser usados no Transact-SQL:

- compressed_history
- event_stream


Uma maneira pela qual sabemos que esses dois destinos não podem ser usados no T-SQL é que seus valores não nulos da coluna *sys.dm_xe_objects.capabilities* não incluem o bit 0x1.


O destino event_stream pode ser usado em programas do .NET escritos em linguagens como o C#. Desenvolvedores do C# e outros desenvolvedores do .NET podem acessar um fluxo de eventos por meio de uma classe do .NET Framework, como no namespace Microsoft.SqlServer.XEvents.Linq.

Se for encontrado, o erro **25726** significa que o fluxo de eventos ficou cheio de dados mais rapidamente do que o cliente pode consumi-los. Isso fez com que o mecanismo de banco de dados se desconectasse do fluxo de eventos, a fim de evitar a redução do desempenho do servidor.


### <a name="xevent-namespaces"></a>Namespaces de XEvent


- [Namespace Microsoft.SqlServer.Management.XEvent](https://msdn.microsoft.com/library/microsoft.sqlserver.management.xevent.aspx)

- [Namespace Microsoft.SqlServer.XEvent.Linq](https://msdn.microsoft.com/library/microsoft.sqlserver.xevent.linq.aspx)



