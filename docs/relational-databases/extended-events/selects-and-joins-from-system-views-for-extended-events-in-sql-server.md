---
title: SELECTs e JOINs de exibições do sistema dos Eventos Estendidos
description: Há exibições do sistema de eventos estendidos no SQL Server e no Banco de Dados SQL do Azure. Saiba como as informações de sessão de evento são representadas em perspectivas diferentes.
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 04521d7f-588c-4259-abc2-1a2857eb05ec
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3245b4288871e4b92b783aad0f08ca1027b401a0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79526751"
---
# <a name="selects-and-joins-from-system-views-for-extended-events-in-sql-server"></a>Seleções e junções em exibições do sistema dos Eventos Estendidos no SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artigo explica os dois conjuntos de exibições do sistema relacionados a eventos estendidos no SQL Server e no Banco de Dados SQL do Azure. O artigo ilustra:

- Como unir com JOIN várias exibições do sistema.
- Como selecionar com SELECT tipos específicos de informações de exibições do sistema.
- Como as mesmas informações de sessão de evento são representadas de várias perspectivas tecnológicas, o que reforça a compreensão de cada perspectiva.


A maioria dos exemplos é gravada para o SQL Server. Mas, com pequenas edições seria executado no Banco de Dados SQL.



## <a name="a-foundational-information"></a>a. Informações básicas


Há dois conjuntos de exibições do sistema para eventos estendidos:


#### <a name="catalog-views"></a>Exibições do catálogo:

- Essas exibições armazenam informações sobre a *definição* de cada sessão de evento que é criada por [CREATE EVENT SESSION](../../t-sql/statements/create-event-session-transact-sql.md)ou por uma interface do usuário SSMS equivalente. Mas essas exibições não sabem nada sobre se alguma das sessões já começou a ser executada.
    - Por exemplo, se o **Pesquisador de Objetos** do SSMS mostrar que não há nenhuma sessão de eventos definida, realizar a seleção da exibição *sys.server_event_session_targets* com SELECT retornará zero linhas.


- O prefixo do nome é:
    - *sys.server\_event\_session\** é o prefixo de nome no SQL Server.
    - *sys.database\_event\_session\** é o prefixo de nome no Banco de Dados SQL.


#### <a name="dynamic-management-views-dmvs"></a>DMVs (exibições de gerenciamento dinâmico):

- Armazenam informações sobre a *atividade atual* das sessões de evento em execução. Mas esses DMVs sabem muito sobre a definição das sessões.
    - Mesmo se todas as sessões de eventos estiverem paradas no momento, um SELECT da exibição de *sys.dm_xe_packages* ainda retornará linhas porque vários pacotes são carregados na memória ativa na inicialização do servidor.
    - Pelo mesmo motivo, *sys.dm_xe_objects* *sys.dm_xe_object_columns* também retorna linhas.


- O prefixo do nome para DMVs de eventos estendidos é:
    - *sys.dm\_xe\_\** é o nome do prefixo no SQL Server.
    - *sys.dm\_xe\_bancodedados\_\** geralmente é o prefixo de nome no Banco de Dados SQL.


#### <a name="permissions"></a>Permissões:


Para realizar a seleção com SELECT das exibições do sistema, a seguinte permissão é necessária:

- VIEW SERVER STATE: se for no Microsoft SQL Server.
- VIEW DATABASE STATE: se for no Banco de Dados SQL do Azure.


<a name="section_B_catalog_views"></a>

## <a name="b-catalog-views"></a>B. Exibições do catálogo


Esta seção corresponde e correlaciona três diferentes perspectivas tecnológicas na mesma sessão de eventos definida. A sessão foi definida e é visível no **Pesquisador de Objetos** do SQL Server Management Studio (SSMS.exe), mas a sessão não está em execução no momento.

Todos os meses, é aconselhável [instalar a atualização mais recente do SSMS](https://msdn.microsoft.com/library/mt238290.aspx), para evitar falhas inesperadas.


A documentação de referência sobre as exibições de catálogo para eventos estendidos está em [Exibições do catálogo de eventos estendidos (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md).


&nbsp;



#### <a name="the-sequence-in-this-section-b"></a>A sequência nesta seção B:


- [B.1 Perspectiva da interface do usuário do SSMS](#section_B_1_SSMS_UI_perspective)
    - Crie a definição de sessão de evento usando a interface do usuário do SSMS. São mostradas capturas de tela passo a passo.


- [B.2 Perspectiva do Transact-SQL](#section_B_2_TSQL_perspective)
    - Use o menu de contexto do SSMS para fazer engenharia reversa da sessão de eventos definida na instrução **CREATE EVENT SESSION** do Transact-SQL equivalente. O T-SQL mostra uma correspondência perfeita para as opções de capturas de tela do SSMS.


- [B.3 Perspectiva SELECT JOIN UNION da exibição de catálogo](#section_B_3_Catalog_view_S_J_UNION)
    - Emita uma instrução T-SQL SELECT das exibições de catálogo do sistema para nossa sessão de evento. Os resultados corresponderem às especificações de instrução **CREATE EVENT SESSION** .


&nbsp;



<a name="section_B_1_SSMS_UI_perspective"></a>

### <a name="b1-ssms-ui-perspective"></a>B.1 Perspectiva da interface do usuário do SSMS


No SSMS, no seu **Pesquisador de Objetos**, é possível iniciar a caixa de diálogo **Nova Sessão** expandindo **Gerenciamento** > **Eventos Estendidos**e clicando com o botão direito do mouse em **Sessões** > **Nova Sessão**.

Na caixa de diálogo grande **Nova Sessão** , em sua primeira seção chamada **Geral**, vemos que a opção foi selecionada para **Iniciar a sessão de evento na inicialização do servidor**.

![Nova Sessão > Geral, Iniciar a sessão de evento na inicialização do servidor.](../../relational-databases/extended-events/media/xevents-ssms-ac105-eventname-startup.png)


Em seguida, na seção **Eventos**, vemos que o evento **lock_deadlock** foi selecionado. Para esse evento, vemos que três **Ações** foram selecionadas. Isso significa que o botão **Configurar** foi clicado, que fica cinza após ser clicado.

![Nova Sessão > Eventos, Campos Globais (Ações)](../../relational-databases/extended-events/media/xevents-ssms-ac110-actions-global.png)


<a name="resource_type_PAGE_cat_view"></a>

Em seguida, ainda na seção **Eventos** > **Configurar**, vemos que [**resource_type** foi definido como **PAGE**](#resource_type_dmv_actual_row). Isso significa que os dados de eventos não serão enviados do mecanismo de evento para a página de destino se o valor de **resource_type** for algo diferente de **PAGE**.

Vemos filtros de predicado adicionais para o nome do banco de dados e para um contador.

![Nova Sessão > Eventos > Configurar > Campos de Predicado de Filtro (Ações)](../../relational-databases/extended-events/media/xevents-ssms-ac115-predicate-db.png)


Em seguida, na seção **Armazenamento de Dados**, vemos que **event_file** foi selecionado como destino. Além disso, vemos que a opção **Habilitar substituição de arquivo** foi selecionada.

![Nova Sessão > Armazenamento de Dados, eventfile_enablefileroleover](../../relational-databases/extended-events/media/xevents-ssms-ac120-target-eventfile.png)


Por fim, na seção **Avançado**, vemos que o valor de **Latência Máxima de Expedição** foi reduzido para 4 segundos.

![Nova Sessão > Avançado, Latência máxima de expedição](../../relational-databases/extended-events/media/xevents-ssms-ac125-latency4.png)


Isso conclui a perspectiva da interface do usuário do SSMS em uma definição de sessão de evento.


<a name="section_B_2_TSQL_perspective"></a>

### <a name="b2-transact-sql-perspective"></a>B.2 Perspectiva do Transact-SQL


Independentemente de como uma definição de sessão do evento é criada, na interface do usuário do SSMS, a sessão pode ser submetida à engenharia reversa em um script do Transact-SQL perfeitamente correspondente. Você pode examinar as capturas de tela de Nova Sessão anteriores e comparar as especificações visíveis com as cláusulas no seguinte script **CREATE EVENT SESSION** do T-SQL gerado.

Para realizar a engenharia reversa de uma sessão, você pode clicar com o botão direito do mouse no nó da sessão no **Pesquisador de Objetos** e selecionar **Sessão de Script como** > **CREATE para** > **Área de Transferência**.

O script do T-SQL a seguir foi criado pela engenharia reversa com o SSMS. Em seguida, o script foi manualmente “embelezado” pela manipulação estratégica somente do espaço em branco.


```sql
CREATE EVENT SESSION [event_session_test3]
    ON SERVER  -- Or, if on Azure SQL Database, ON DATABASE.

    ADD EVENT sqlserver.lock_deadlock
    (
        SET
            collect_database_name = (1)
        ACTION
        (
            package0  .collect_system_time,
            package0  .event_sequence,
            sqlserver .client_hostname
        )
        WHERE
        (
            [database_name]           = N'InMemTest2'
            AND [package0].[counter] <= (16)
            AND [resource_type]       = (6)
        )
    )

    ADD TARGET package0.event_file
    (
        SET
            filename           = N'C:\Junk\event_session_test3_EF.xel',
            max_file_size      = (20),
            max_rollover_files = (2)
    )

    WITH
    (
        MAX_MEMORY            = 4096 KB,
        EVENT_RETENTION_MODE  = ALLOW_SINGLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY  = 4 SECONDS,
        MAX_EVENT_SIZE        = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY       = OFF,
        STARTUP_STATE         = ON
    );
```


Isso conclui a perspectiva do T-SQL.


<a name="section_B_3_Catalog_view_S_J_UNION"></a>

### <a name="b3-catalog-view-select-join-union-perspective"></a>B.3 Perspectiva SELECT JOIN UNION da exibição de catálogo


Não tenha medo! A instrução T-SQL SELECT é longa apenas porque une, com UNION, vários SELECTs pequenos. Qualquer um dos SELECTs pequenos pode ser executado sozinho. Os pequenos SELECT mostram como as várias exibições de catalogação do sistema devem ser unidas, utilizando JOIN.


```sql
SELECT
        s.name        AS [Session-Name],
        '1_EVENT'     AS [Clause-Type],
        'Event-Name'  AS [Parameter-Name],
        e.name        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name         AS [Session-Name],
        '2_EVENT_SET'  AS [Clause-Type],
        f.name         AS [Parameter-Name],
        f.value        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '3_EVENT_ACTION'    AS [Clause-Type],

        a.package + '.' + a.name
                            AS [Parameter-Name],

        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_actions  As a

            ON  a.event_session_id = s.event_session_id
            AND a.event_id         = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                AS [Session-Name],
        '4_EVENT_PREDICATES'  AS [Clause-Type],
        e.predicate           AS [Parameter-Name],
        '(Not_Applicable)'    AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '5_TARGET'          AS [Clause-Type],
        t.name              AS [Parameter-Name],
        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name          AS [Session-Name],
        '6_TARGET_SET'  AS [Clause-Type],
        f.name          AS [Parameter-Name],
        f.value         AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = t.target_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name               AS [Session-Name],
        '7_WITH_MAX_MEMORY'  AS [Clause-Type],
        'max_memory'         AS [Parameter-Name],
        s.max_memory         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                  AS [Session-Name],
        '7_WITH_STARTUP_STATE'  AS [Clause-Type],
        'startup_state'         AS [Parameter-Name],
        s.startup_state         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

ORDER BY
    [Session-Name],
    [Clause-Type],
    [Parameter-Name]
;
```


#### <a name="output"></a>Saída


A tabela a seguir mostra a saída da execução de SELECT JOIN UNION anterior. Os nomes de parâmetro de saída e os valores mapeiam para o que é claramente visível na instrução CREATE EVENT SESSION anterior.

| Session-Name | Clause-Type | Parameter-Name | Parameter-Value |
|---|---|---|---|
|event_session_test3  | 1_EVENT |                Event-Name |                       lock_deadlock |
|event_session_test3  |  2_EVENT_SET |             collect_database_name |            1 |
|event_session_test3  |  3_EVENT_ACTION |          sqlserver.client_hostname |       (Not_Applicable) |
|event_session_test3  |  3_EVENT_ACTION |         sqlserver.collect_system_time |   (Not_Applicable) |
|event_session_test3  |  3_EVENT_ACTION |         sqlserver.event_sequence |        (Not_Applicable) |
|event_session_test3  |  4_EVENT_PREDICATES |     (\[sqlserver\].\[equal_i_sql_unicode_string\]\(\[database_name\],N'InMemTest2'\) AND \[package0\].\[counter\]<=\(16\)\) |   (Not_Applicable) |
|event_session_test3  |  5_TARGET |               event_file |                      (Not_Applicable) |
|event_session_test3  |  6_TARGET_SET |           nome do arquivo  |                       C:\Junk\event_session_test3_EF.xel |
|event_session_test3  |  6_TARGET_SET |           max_file_size |                   20 |
|event_session_test3  |  6_TARGET_SET |           max_rollover_files |              2 |
|event_session_test3  |  7_WITH_MAX_MEMORY |      max_memory |                      4096 |
|event_session_test3  |  7_WITH_STARTUP_STATE |   startup_state |                   1 |

Isso conclui a seção sobre exibições do catálogo.



<a name="section_C_DMVs"></a>

## <a name="c-dynamic-management-views-dmvs"></a>C. DMVs (Exibições de gerenciamento dinâmico)


Agora, vamos mudar para DMVs. Esta seção fornece várias instruções Transact-SQL SELECT que servem, cada uma, a uma finalidade de negócios útil específica. Além disso, os SELECTs demonstram como unir as DMVs com JOIN para quaisquer novos usos desejados.


A documentação de referência das DMVs está disponível em [Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)


Neste artigo, todas as linhas saída reais dos SELECTs a seguir são do SQL Server 2016, a menos que esteja especificado de outra forma.


Aqui está a lista de SELECTs nesta seção C de DMV:

- [C.1 Lista de todos os pacotes](#section_C_1_list_packages)
- [C.2 Contagem de cada tipo de objeto](#section_C_2_count_object_type)
- [C.3 SELECT todos os itens disponíveis classificados por tipo](#section_C_3_select_all_available_objects)
- [C.4 Campos de dados disponíveis para seu evento](#section_C_4_data_fields)
- [C.5 *sys.dm_xe_map_values* e campos de evento](#section_C_5_map_values_fields)
- [C.6 Parâmetros para destinos](#section_C_6_parameters_targets)
- [C.7 SELECT de DMV convertendo a coluna target_data para XML](#section_C_7_dmv_select_target_data_column)
- [C.8 SELECT FROM de uma função para recuperar dados de event_file da unidade de disco](#section_C_8_select_function_disk)



<a name="section_C_1_list_packages"></a>

### <a name="c1-list-of-all-packages"></a>C.1 Lista de todos os pacotes


Todos os objetos que você pode usar na área de eventos estendidos são provenientes de pacotes que são carregados no sistema. Esta seção lista todos os pacotes e suas descrições.


```sql
SELECT  --C.1
        p.name         AS [Package],
        p.description  AS [Package-Description]
    FROM
        sys.dm_xe_packages  AS p
    ORDER BY
        p.name;
```


#### <a name="output"></a>Saída

Aqui está a lista de pacotes.

| Pacote        |Package-Description|
|---|---|
|fluxo de arquivos|     Eventos estendidos para SQL Server FILESTREAM e FileTable |
|package0   |    Pacote padrão. Contém todos os tipos, mapas, operadores de comparação, ações e destinos padrão |
|qds         |   Eventos estendidos para Repositório de Consultas |
|SecAudit     |  Eventos de auditoria de segurança |
|sqlclr        | Eventos estendidos para SQL CLR |
|sqlos         | Eventos estendidos para o Sistema Operacional SQL |
|SQLSatellite |  Eventos estendidos para SQL Satellite |
|sqlserver   |   Eventos estendidos para o Microsoft SQL Server |
|sqlserver  |    Eventos estendidos para o Microsoft SQL Server |
|sqlserver  |    Eventos estendidos para o Microsoft SQL Server |
|sqlsni     |    Eventos estendidos para o Microsoft SQL Server |
|ucs        |    Eventos estendidos para Pilha de Comunicações Unificadas |
|XtpCompile |    Eventos estendidos para a Compilação XTP |
|XtpEngine  |    Eventos estendidos para o mecanismo XTP |
|XtpRuntime |    Eventos estendidos para o Runtime XTP |


*Definições dos inicialismos anteriores:*

- clr = Common Language Runtime do .NET
- qds = Armazenamento de Dados de Consulta
- sni = Interface de Rede do Servidor
- ucs = Pilha de Comunicações Unificadas
- xtp = extreme transaction processing


<a name="section_C_2_count_object_type"></a>

### <a name="c2-count-of-every-object-type"></a>C.2 Contagem de cada tipo de objeto


Esta seção informa sobre os tipos de objetos que contêm pacotes de eventos. É exibida uma lista completa de todos os tipos de objeto que estão em *sys.dm\_xe\_objects*, juntamente com a contagem para cada tipo.


```sql
SELECT  --C.2
        Count(*)  AS [Count-of-Type],
        o.object_type
    FROM
        sys.dm_xe_objects  AS o
    GROUP BY
        o.object_type
    ORDER BY
        1  DESC;
```


#### <a name="output"></a>Saída

Aqui está a contagem de objetos por tipo de objeto. Existem aproximadamente 1915 objetos.

|Count-of-Type |   object_type |
|---|---|
|1303|            event |
|351  |           map |
|84    |          message |
|77     |         pred_compare |
|53     |        ação |
|46     |         pred_source |
|28     |         type |
|17     |         destino |

<a name="section_C_3_select_all_available_objects"></a>

### <a name="c3-select-all-available-items-sorted-by-type"></a>C.3 SELECT todos os itens disponíveis classificados por tipo


O SELECT a seguir retorna aproximadamente 1915 linhas, uma para cada objeto.



```sql
SELECT  --C.3
        o.object_type  AS [Type-of-Item],
        p.name         AS [Package],
        o.name         AS [Item],
        o.description  AS [Item-Description]
    FROM
             sys.dm_xe_objects  AS o
        JOIN sys.dm_xe_packages AS p  ON o.package_guid = p.guid
    WHERE
        o.object_type IN ('action' , 'target' , 'pred_source')
        AND
        (
            (o.capabilities & 1) = 0
            OR
            o.capabilities IS NULL
        )
    ORDER BY
        [Type-of-Item],
        [Package],
        [Item];
```


#### <a name="output"></a>Saída

Para aguçar seu apetite, a seguir está uma amostragem arbitrária dos objetos retornados pelo SELECT anterior.


|Type-of-Item|   Pacote|        Item|                          Item-Description|
|---|---|---|---|
|ação|         package0  |     callstack                     |Coletar a pilha de chamadas atual|
|ação |        package0  |     debug_break                   |Interromper o processo no depurador padrão|
|ação |       sqlos      |    task_time                     |Coletar tempo de execução da tarefa atual|
|ação |        sqlserver |     sql_text                     | Coletar texto SQL|
|event  |        qds       |     query_store_aprc_regression  | Acionado quando o Repositório de Consultas detecta regressão no desempenho do plano de consulta|
|event  |        SQLSatellite |  connection_accept            | Ocorre quando uma nova conexão é aceita. Este evento serve para registrar todas as tentativas de conexão.|
|event  |        XtpCompile  |   cgen                          |Ocorre no início da geração de código C.|
|map    |        qds         |   aprc_state                    |Estado de correção de regressão do plano automático do Repositório de Consultas|
|message |       package0    |   histogram_event_required      |É necessário um valor para o parâmetro 'filtering_event_name' quando o tipo de origem é 0.|
|pred_compare |  package0   |    equal_ansi_string             |Operador de igualdade entre dois valores de cadeia de caracteres ANSI|
|pred_compare |  sqlserver  |    equal_i_sql_ansi_string       |Operador de Igualdade entre dois valores de cadeia de caracteres SQL ANSI|
|pred_source |   sqlos      |    task_execution_time           |Obter o tempo de execução da tarefa atual|
|pred_source |   sqlserver  |    client_app_name               |Obter o nome do aplicativo cliente atual|
|destino |        package0   |    etw_classic_sync_target       |Destino Síncrono do ETW (Rastreamento de Eventos para Windows)|
|destino |        package0   |    event_counter                 |Use o destino event_counter para contar o número de ocorrências de cada evento na sessão de evento.|
|destino  |       package0  |     event_file                    |Use o destino event_file para salvar os dados de evento em um arquivo XEL, que pode ser arquivado e usado para análise e revisão posteriores. Você pode mesclar vários arquivos XEL para ver os dados combinados de sessões de evento separadas.|
|destino  |       package0   |    histogram                     |Use o destino de histograma para agregar dados de evento com base em um campo de dados de evento específico ou ação associada ao evento. O histograma permite que você analise a distribuição dos dados do evento durante o período da sessão de evento.|
|destino   |      package0  |     pair_matching                 |Destino de emparelhamento|
|destino   |      package0  |     ring_buffer                   |Destino de buffer de anéis assíncrono|
|type     |      package0  |     Xml                           |Fragmento XML bem formado|

<a name="section_C_4_data_fields"></a>

### <a name="c4-data-fields-available-for-your-event"></a>C.4 Campos de dados disponíveis para seu evento


A instrução SELECT a seguir retorna todos os campos de dados que são específicos para seu tipo de evento.

- Observe o item de cláusula WHERE: *column_type = 'data'* .
- Além disso, você precisa editar o valor da cláusula WHERE *o.name =* .


```sql
SELECT  -- C.4
        p.name         AS [Package],
        c.object_name  AS [Event],
        c.name         AS [Column-for-Predicate-Data],
        c.description  AS [Column-Description]
    FROM
              sys.dm_xe_object_columns  AS c
        JOIN  sys.dm_xe_objects         AS o

            ON  o.name = c.object_name

        JOIN  sys.dm_xe_packages        AS p

            ON  p.guid = o.package_guid
    WHERE
        c.column_type = 'data'
        AND
        o.object_type = 'event'
        AND
        o.name        = '\<EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Event],
        [Column-for-Predicate-Data];
```


#### <a name="output"></a>Saída

As linhas a seguir foram retornadas pelo SELECT, WHERE `o.name = 'lock_deadlock'`anterior:

- Cada linha representa um filtro opcional para o evento *sqlserver.lock_deadlock* .
- A coluna *\[Column-Description\]* é omitida da exibição a seguir. Geralmente, seu valor é NULL.
- Essa é a saída real, exceto pela coluna de descrição omitida, que costuma ser nula.
- Essas são as linhas em que object_type = 'lock_deadlock'.

|Pacote|     Evento|           Column-for-Predicate-Data|
|---|---|---|
|sqlserver|   lock_deadlock|   associated_object_id|
|sqlserver|  lock_deadlock |  database_id|
|sqlserver|  lock_deadlock |  database_name|
|sqlserver|   lock_deadlock|   deadlock_id|
|sqlserver|   lock_deadlock|   duration|
|sqlserver|   lock_deadlock|   lockspace_nest_id|
|sqlserver|   lock_deadlock|   lockspace_sub_id|
|sqlserver|   lock_deadlock|   lockspace_workspace_id|
|sqlserver|   lock_deadlock|   mode|
|sqlserver|   lock_deadlock|   object_id|
|sqlserver|   lock_deadlock|   owner_type|
|sqlserver|   lock_deadlock|   resource_0|
|sqlserver|   lock_deadlock|  resource_1|
|sqlserver|   lock_deadlock|   resource_2|
|sqlserver|   lock_deadlock|   resource_description|
|sqlserver|   lock_deadlock|   resource_type|
|sqlserver|   lock_deadlock|   transaction_id|




<a name="section_C_5_map_values_fields"></a>

### <a name="c5-sysdm_xe_map_values-and-event-fields"></a>C.5 *sys.dm_xe_map_values* e campos de evento


A instrução SELECT a seguir inclui um JOIN para a exibição complicada chamada *sys.dm_xe_map_values*.

A finalidade do SELECT é mostrar os vários campos que podem ser selecionados para sua sessão de eventos. Os campos de evento podem ser usados de duas maneiras:

- Para escolher quais valores do campo serão gravados para o destino para cada ocorrência do evento...
- Para filtrar quais ocorrências do evento serão enviadas para versus mantidas fora de seu destino.


```sql
SELECT  --C.5
        dp.name         AS [Package],
        do.name         AS [Object],
        do.object_type  AS [Object-Type],
        'o--c'     AS [O--C],
        dc.name         AS [Column],
        dc.type_name    AS [Column-Type-Name],
        dc.column_type  AS [Column-Type],
        dc.column_value AS [Column-Value],
        'c--m'     AS [C--M],
        dm.map_value    AS [Map-Value],
        dm.map_key      AS [Map-Key]
    FROM
              sys.dm_xe_objects         AS do
        JOIN  sys.dm_xe_object_columns  AS dc

            ON  dc.object_name = do.name

        JOIN  sys.dm_xe_map_values      AS dm

            ON  dm.name = dc.type_name

        JOIN  sys.dm_xe_packages        AS dp

            ON  dp.guid = do.package_guid
    WHERE
        do.object_type = 'event'
        AND
        do.name        = '\<YOUR-EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Object],
        [Column],
        [Map-Value];
```


#### <a name="output"></a>Saída

<a name="resource_type_dmv_actual_row"></a>

A seguir, há uma amostragem das 153 linhas reais da saída do T-SQL SELECT anterior. A linha de **resource_type** é [relevante](#resource_type_PAGE_cat_view) para a filtragem de predicado usada no exemplo **event_session_test3** em outro lugar nesse artigo.


```
/***  5 sampled rows from the actual 153 rows returned.
    NOTE:  'resource_type' under 'Column'.

Package     Object          Object-Type   O--C   Column          Column-Type-Name     Column-Type   Column-Value   C--M   Map-Value        Map-Key
-------     ------          -----------   ----   ------          ----------------     -----------   ------------   ----   ---------        -------
sqlserver   lock_deadlock   event         o--c   CHANNEL         etw_channel          readonly      2              c--m   Operational      4
sqlserver   lock_deadlock   event         o--c   KEYWORD         keyword_map          readonly      16             c--m   access_methods   1024
sqlserver   lock_deadlock   event         o--c   mode            lock_mode            data          NULL           c--m   IX               8
sqlserver   lock_deadlock   event         o--c   owner_type      lock_owner_type      data          NULL           c--m   Cursor           2
sqlserver   lock_deadlock   event         o--c   resource_type   lock_resource_type   data          NULL           c--m   PAGE             6

Therefore, on your CREATE EVENT SESSION statement, in its ADD EVENT WHERE clause,
you could put:
    WHERE( ... resource_type = 6 ...)  -- Meaning:  6 = PAGE.
***/
```


<a name="section_C_6_parameters_targets"></a>

### <a name="c6-parameters-for-targets"></a>C.6 Parâmetros para destinos


A instrução SELECT a seguir retorna todos os parâmetros para o seu destino. Cada parâmetro está marcado para indicar se é obrigatório. Os valores que você atribui a parâmetros afetam o comportamento do destino.

- Observe o item de cláusula WHERE: *object_type = 'customizable'* .
- Além disso, você precisa editar o valor da cláusula WHERE *o.name =* .


```sql
SELECT  --C.6
        p.name        AS [Package],
        o.name        AS [Target],
        c.name        AS [Parameter],
        c.type_name   AS [Parameter-Type],

        CASE c.capabilities_desc
            WHEN 'mandatory' THEN 'YES_Mandatory'
            ELSE 'Not_mandatory'
        END  AS [IsMandatoryYN],

        c.description AS [Parameter-Description]
    FROM
              sys.dm_xe_objects   AS o
        JOIN  sys.dm_xe_packages  AS p

            ON  o.package_guid = p.guid

        LEFT OUTER JOIN  sys.dm_xe_object_columns  AS c

            ON  o.name        = c.object_name
            AND c.column_type = 'customizable'  -- !
    WHERE
        o.object_type = 'target'
        AND
        o.name     LIKE '%'    -- Or '\<YOUR-TARGET-NAME-HERE!>'.
    ORDER BY
        [Package],
        [Target],
        [IsMandatoryYN]  DESC,
        [Parameter];
```


#### <a name="output"></a>Saída

As linhas de parâmetros a seguir são um subconjunto daquelas retornadas pela instrução SELECT anterior, no SQL Server 2016.


```
/***  Actual output, all rows, where target name = 'event_file'.
Package    Target       Parameter            Parameter-Type       IsMandatoryYN   Parameter-Description
-------    ------       ---------            --------------       -------------   ---------------------
package0   event_file   filename             unicode_string_ptr   YES_Mandatory   Specifies the location and file name of the log
package0   event_file   increment            uint64               Not_mandatory   Size in MB to grow the file
package0   event_file   lazy_create_blob     boolean              Not_mandatory   Create blob upon publishing of first event buffer, not before.
package0   event_file   max_file_size        uint64               Not_mandatory   Maximum file size in MB
package0   event_file   max_rollover_files   uint32               Not_mandatory   Maximum number of files to retain
package0   event_file   metadatafile         unicode_string_ptr   Not_mandatory   Not used
***/
```


<a name="section_C_7_dmv_select_target_data_column"></a>

### <a name="c7-dmv-select-casting-target_data-column-to-xml"></a>C.7 SELECT de DMV convertendo a coluna target_data para XML


Esse SELECT de DMV retorna linhas de dados do destino de sua sessão de eventos ativa. Os dados são convertidos em XML, o que torna sua célula retornada clicável para a exibição fácil no SSMS.

- Se sua sessão de evento for interrompida, este SELECT retornará zero linhas.
- Você precisa editar o valor da cláusula WHERE para *s.name =* .


```sql
SELECT  --C.7
        s.name,
        t.target_name,
        CAST(t.target_data AS XML)  AS [XML-Cast]
    FROM
              sys.dm_xe_session_targets  AS t
        JOIN  sys.dm_xe_sessions         AS s

            ON s.address = t.event_session_address
    WHERE
        s.name = '\<Your-Session-Name-Here!>';
```


#### <a name="output-the-only-row-including-its-xml-cell"></a>Saída, a única linha, incluindo sua célula XML

Aqui está a única linha resultante do SELECT anterior. A coluna *XML-Cast* contém uma cadeia de caracteres de XML que o SSMS entende que é XML. Portanto, o SSMS compreende que ele deve tornar a célula de XML-Cast clicável.


Para esta execução:

- O valor *s.name =* foi definido para uma sessão de evento para o evento *checkpoint_begin* .
- O destino era um *ring_buffer*.


```XML
name                              target_name   XML-Cast
----                              -----------   --------
checkpoint_session_ring_buffer2   ring_buffer   <RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104"><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event></RingBufferTarget>
```


#### <a name="output-xml-displayed-pretty-when-cell-is-clicked"></a>Saída, XML exibido formatado quando a célula é clicada


Quando a célula XML-CAST é clicada, a seguinte exibição formatada aparece.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104">
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
</RingBufferTarget>
```


<a name="section_C_8_select_function_disk"></a>

### <a name="c8-select-from-a-function-to-retrieve-event_file-data-from-disk-drive"></a>C.8 SELECT FROM de uma função para recuperar dados de event_file da unidade de disco


Suponha que sua sessão de eventos coletou alguns dados e foi parada posteriormente. Se sua sessão tiver sido definida para usar o destino event_file, você ainda poderá recuperar os dados chamando a função *sys.fn_xe_target_read_file*.

- Você deve editar o caminho e o nome de arquivo no parâmetro da chamada de função, antes de executar este SELECT.
    - Não dê atenção aos dígitos extra que o sistema SQL integra nos nomes de arquivo .XEL reais sempre que você reinicia a sessão. Apenas dê o nome raiz e a extensão normais.


```sql
SELECT  --C.8
        f.module_guid,
        f.package_guid,
        f.object_name,
        f.file_name,
        f.file_offset,
        CAST(f.event_data AS XML)  AS [Event-Data-As-XML]
    FROM
        sys.fn_xe_file_target_read_file(

            '\<YOUR-PATH-FILE-NAME-ROOT-HERE!>*.xel',
            --'C:\Junk\Checkpoint_Begins_ES*.xel',  -- Example.

            NULL, NULL, NULL
        )  AS f;
```


#### <a name="output-rows-returned-by-select-from-the-function"></a>Saída, linhas retornadas pelo SELECT FROM da função


A seguir estão as linhas retornadas pelo SELECT FROM da função anterior. A coluna do XML mais à direita contém os dados que são especificamente sobre a ocorrência do evento.


```
module_guid                            package_guid                           object_name        file_name                                                           file_offset   Event-Data-As-XML
-----------                            ------------                           -----------        ---------                                                           -----------   -----------------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:14.025Z"><data name="database_id"><value>5</value></data></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:17.704Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:17.709Z"><data name="database_id"><value>5</value></data></event>
```


#### <a name="output-one-xml-cell"></a>Saída, uma célula XML


Aqui está o conteúdo da primeira célula XML, do conjunto de linhas retornado anterior.


```xml
<event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z">
  <data name="database_id">
    <value>5</value>
  </data>
  <action name="session_id" package="sqlserver">
    <value>60</value>
  </action>
  <action name="database_id" package="sqlserver">
    <value>5</value>
  </action>
</event>
```


