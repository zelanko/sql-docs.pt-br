---
title: Criar uma sessão de eventos estendidos usando o Editor de consultas | Microsoft Docs
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
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 38e5ff6e5da2f8800dda895fb3ffde5dfea435ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010952"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>Criar uma sessão de Eventos Estendidos usando o Editor de Consultas
  Você pode criar uma sessão de Eventos Estendidos usando o Editor de Consulta ou pode criar uma sessão no Pesquisador de Objetos. Em Pesquisador de Objetos, os Eventos Estendidos fornecem duas interfaces do usuário que você pode usar para criar, modificar e exibir dados de sessão de evento: um assistente que orienta o processo de criação de sessão de evento e uma interface de usuário Nova Sessão que fornece mais opções de configuração avançadas. Você pode criar sessões de Eventos Estendidos para diagnosticar rastreamento de SQL Server que permite resolver problemas como os seguintes:  
  
-   Localizar suas consultas mais caras  
  
-   Localizar causas raiz de contenção de trava  
  
-   Localizar uma consulta que está bloqueando outras consultas  
  
-   Solucionar problemas de uso excessivo de CPU causados por recompilação de consulta  
  
-   Solucionando problemas de deadlocks  
  
 Para obter informações sobre como criar uma sessão dos Eventos Estendidos usando o Assistente de Nova Sessão, veja [Criar uma sessão de Eventos Estendidos usando o assistente &#40;Pesquisador de Objetos&#41;](../ssms/object/object-explorer.md). Para obter informações sobre como criar uma sessão dos Eventos Estendidos usando a interface do usuário de Nova Sessão, veja [Criar uma sessão de Eventos Estendidos usando a caixa de diálogo Nova Sessão](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md).  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Para criar uma sessão de Eventos Estendidos, você deve ter a permissão ALTER ANY EVENT SESSION.  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>Criando uma sessão de Eventos Estendidos usando o Editor de Consultas  
  
#### <a name="to-create-an-extended-events-session"></a>Para criar uma sessão de Eventos Estendidos  
  
1.  O procedimento a seguir descreve como criar uma sessão de Eventos Estendidos usando o Editor de Consultas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     Determine quais eventos você deseja usar na sessão. Para consultar todos os eventos disponíveis, junto com a palavra-chave e o canal, use a seguinte consulta:  
  
    > [!NOTE]  
    >  Para obter informações sobre palavras-chave e canais, veja [Pacotes de Eventos Estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  Em uma nova janela de consulta, adicione as seguintes instruções para criar uma sessão de evento, substituindo *session_name* pelo nome de sessão que você deseja usar:  
  
    > [!IMPORTANT]  
    >  As etapas de 2 a 6 deste procedimento descrevem cada seção da definição de sessão de evento. Você adicionaria todas as instruções a uma única janela de consulta antes da execução. Para obter um exemplo completo, consulte a seção Exemplo deste tópico.  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  Adicione os eventos que você deseja monitorar, no formato *package_name*.*event_name*. Para cada evento, adicione uma linha semelhante à seguinte:  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     Por exemplo:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (Opcional) Depois que você adicionar um evento, poderá adicionar as ações a serem executadas. Você também pode adicionar predicados. Os predicados são usados para estabelecer critérios para o momento em que as informações de evento devem ser utilizadas pelo destino. As ações são adicionadas usando uma cláusula ACTION e os predicados são adicionados usando uma cláusula WHERE. Por exemplo, para adicionar uma ação e um predicado em que o texto [!INCLUDE[tsql](../includes/tsql-md.md)] é capturado para o evento sqlserver.file_read_completed, em que a ID de arquivo é igual a 1, você incluiria a seguinte instrução:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   Para exibir quais ações estão disponíveis, use a seguinte consulta:  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   Para exibir quais predicados estão disponíveis para um evento, use a seguinte consulta, substituindo *event_name* pelo nome do evento para o qual você deseja adicionar um predicado:  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         Por exemplo:  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         Esteja atento que você também pode adicionar origens de predicado globais. Uma origem de predicado global pode ser usada em qualquer expressão de predicado. Para exibir quais origens de predicado globais estão disponíveis, use a seguinte consulta:  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         Por exemplo, você poderia usar a seguinte expressão de predicado para especificar que os dados sejam coletados para um evento somente nas cinco primeiras vezes que um evento ocorrer.  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  Adicione o destino desejado, onde os dados de evento serão processados e utilizados. Use o seguinte formato:  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     O exemplo a seguir adiciona o destino de arquivo assíncrono:  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     Para exibir a lista de destinos disponíveis, use a seguinte consulta:  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  Para obter informações sobre os diferentes tipos de destino, veja [Destinos de Eventos Estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
6.  Revise e adicione qualquer opção de configuração adicional. Por exemplo, você pode configurar opções como modo de retenção de evento, quanto tempo os eventos permanecerão armazenados em buffer na memória ou se a sessão de evento deverá iniciar automaticamente quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for iniciado. As opções são descritas no tópico [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql). Saiba que os valores padrão serão atribuídos se essas opções não forem especificadas.  
  
7.  Inicie a sessão.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre como exibir os resultados da sessão, veja o tópico correspondente do tipo de destino usado no nó [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md) dos Manuais Online.  
  
 O exemplo a seguir cria uma sessão de Eventos Estendidos chamada IOActivity que captura as seguintes informações:  
  
-   Dados de evento para leituras de arquivo concluídas, incluindo o texto associado do [!INCLUDE[tsql](../includes/tsql-md.md)] para leituras de arquivo onde a ID de arquivo é igual a 1.  
  
-   Dados de evento para gravações de arquivo concluídas.  
  
-   Dados de evento sobre o momento em que os dados são gravados no cache de log para o arquivo de log físico.  
  
 A sessão envia a saída para um destino de arquivo.  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Pacotes de eventos estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
