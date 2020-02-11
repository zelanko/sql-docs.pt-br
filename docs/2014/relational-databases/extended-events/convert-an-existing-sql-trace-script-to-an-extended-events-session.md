---
title: Converter um script de rastreamento do SQL existente em uma sessão de eventos estendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83cf9390524d2fdc013fdddc41c610c28930e998
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63015768"
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>Converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos
  Se você tiver um script de Rastreamento do SQL que deseja converter em sessão de Eventos Estendidos, poderá usar os procedimentos deste tópico para criar uma sessão de Eventos Estendidos equivalente. Usando as informações das tabelas de sistema trace_xe_action_map e trace_xe_event_map, você pode coletar as informações que precisa para fazer a conversão.  
  
 As etapas incluem o seguinte:  
  
1.  Execute o script existente para criar uma sessão de Rastreamento do SQL obter a ID do rastreamento.  
  
2.  Execute uma consulta que usa a função fn_trace_geteventinfo para localizar os Eventos Estendidos e as ações e eventos para cada classe de evento Rastreamento do SQL e suas colunas associadas.  
  
3.  Use a função fn_trace_getfilterinfo para listar os filtros e as ações equivalentes de Eventos Estendidos a serem usados.  
  
4.  Crie manualmente uma sessão de Eventos Estendidos, usando os eventos, as ações e os predicados (filtros) equivalentes de Eventos Estendidos.  
  
## <a name="to-obtain-the-trace-id"></a>Para obter a ID de rastreamento  
  
1.  Abra o script de Rastreamento do SQL no Editor de Consultas e execute o script para criar a sessão de rastreamento. Saiba que a sessão de rastreamento não precisa estar em execução para concluir este procedimento.  
  
2.  Obtenha a ID do rastreamento. Para fazer isso, use a seguinte consulta:  
  
    ```sql
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  ID de Rastreamento 1 geralmente indica o rastreamento padrão.  
  
## <a name="to-determine-the-extended-events-equivalents"></a>Para determinar os equivalentes de Eventos Estendidos  
  
1.  Para determinar os eventos e as ações equivalentes de Eventos Estendidos, execute a seguinte consulta, em que *trace_id* é definido como o valor da ID de rastreamento que você obteve no procedimento anterior.  
  
    > [!NOTE]  
    >  Nesse exemplo, a ID do rastreamento padrão (1) é usada.  
  
    ```sql
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     A ID de evento, o nome de pacote, o nome de evento, a ID de coluna e o nome de ação equivalentes dos Eventos Estendidos são retornados. Você usará essa saída no procedimento "Para criar a sessão de Eventos Estendidos" mais adiante neste tópico.  
  
     Em alguns casos, a coluna filtrada é mapeada para um campo de dados de evento incluído por padrão no evento de Eventos Estendidos. Portanto, a coluna "Extended_Events_action_name" será NULL. Se isso acontecer, você deve fazer o seguinte para determinar qual campo de dados é equivalente à coluna filtrada:  
  
    1.  Para as ações que retornam NULL, identifique quais classes de evento de Rastreamento do SQL no script contém a coluna que está sendo filtrada.  
  
         Por exemplo, você pode ter usado a classe de evento SP:StmtCompleted e especificado um filtro no nome de coluna de rastreamento Duração (ID 45 da classe de evento de Rastreamento do SQL e ID 13 da coluna de Rastreamento do SQL). Nesse caso, o nome de ação aparecerá como NULL nos resultados da consulta.  
  
    2.  Para cada classe de evento de Rastreamento do SQL identificada na etapa anterior, localize o nome de evento equivalente de Eventos Estendidos. (Se você não tiver certeza do nome do evento equivalente, use a consulta no tópico [Exibir os Eventos Estendidos equivalentes às classes de evento de Rastreamento do SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md).)  
  
    3.  Use a seguinte consulta a fim de identificar os campos de dados corretos para os eventos que você identificado na etapa anterior. A consulta mostra os campos de dados de Eventos Estendidos na coluna "event_field". Na consulta, substitua *<event_name>* pelo nome de um evento que você especificou na etapa anterior.  
  
        ```sql
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         Por exemplo, a classe de evento SP: StmtCompleted é mapeada para o evento sp_statement_completed do Eventos Estendidos. Se você especificar sp_statement_completed como nome de evento da consulta, a coluna "event_field" mostrará os campos que são incluídos por padrão no evento. Observando os campos, você constatará que há um campo "duração". Para criar o filtro na sessão equivalente de Eventos Estendidos, você adicionará um predicado como "WHERE duration > 0". Para obter um exemplo, consulte o procedimento "Para criar a sessão de Eventos Estendidos" neste tópico.  
  
## <a name="to-create-the-extended-events-session"></a>Para criar a sessão de Eventos Estendidos  
 Use o Editor de Consultas para criar a sessão de Eventos Estendidos e gravar a saída em um destino de arquivo. As etapas a seguir descrevem uma única consulta, com explicações para mostrar como criar a consulta. Para obter o exemplo de consulta completo, consulte a seção "Exemplo" deste tópico.  
  
1.  Adicione instruções para criar a sessão de evento, substituindo s*ession_name* pelo nome que você deseja usar para a sessão de eventos estendidos.  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  Adicione os eventos e as ações de Eventos Estendidos que foram retornados como saída no procedimento "Determinar os equivalentes de Eventos Estendidos" e adicione os predicados (filtros) que você identificou no procedimento "Para determinar os filtros usados no script".  
  
     O exemplo a seguir usa um script de Rastreamento do SQL que inclui as classes de evento SQL:StmtStarting e SP:StmtCompleted, com filtros para ID e duração de sessão. A saída de exemplo da consulta no procedimento "Determinar os equivalentes de Eventos Estendidos" retornou este conjunto de resultados:  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     Para converter isso no equivalente de Eventos Estendidos, são adicionados os eventos sqlserver.sp_statement_starting e sqlserver.sp_statement_completed com uma lista de ações. As instruções de predicado são incluídas como cláusulas WHERE.  
  
    ```sql
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  Adicione o destino de arquivo assíncrono, substituindo os caminhos de arquivo com a localização em que você deseja salvar a saída. Ao especificar o destino de arquivo, você deve incluir um arquivo de log e um arquivo de caminho de arquivo de metadados.  
  
    ```sql
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>Para exibir os resultados  
  
1.  Você pode usar a função sys.fn_xe_file_target_read_file para exibir a saída. Para fazer isso, execute a seguinte consulta, substituindo os caminhos de arquivo pelos caminhos que você especificou:  
  
    ```sql
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  A conversão dos dados de evento como XML é opcional.  
  
     Para obter mais informações sobre a função sys.fn_xe_file_target_read_file, consulte [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql).  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>Exemplo  
  
```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir os Eventos Estendidos equivalentes às classes de rastreamento de eventos do SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
