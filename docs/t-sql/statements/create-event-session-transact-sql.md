---
title: CREATE EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EVENT SESSION
- SESSION
- EVENT SESSION
- SESSION_TSQL
- EVENT_SESSION_TSQL
- CREATE_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- CREATE EVENT SESSION statement
ms.assetid: 67683027-2b0f-47aa-b223-604731af8b4d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 089725c52c2f65a9e1edb45a6afadd01ff2ace79
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76910189"
---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Cria uma sessão de Eventos Estendidos que identifica a origem dos eventos, os destinos da sessão de evento e as opções da sessão de evento.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```
CREATE EVENT SESSION event_session_name
ON { SERVER | DATABASE }
{  
    <event_definition> [ ,...n]
    [ <event_target_definition> [ ,...n] ]
    [ WITH ( <event_session_options> [ ,...n] ) ]
}
;

<event_definition>::=
{
    ADD EVENT [event_module_guid].event_package_name.event_name
         [ ( {
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]
                 [ WHERE <predicate_expression> ]
        } ) ]
}

<predicate_expression> ::=
{
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]
    [ ,...n ]
}  
  
<predicate_factor>::=
{
    <predicate_leaf> | ( <predicate_expression> )
}

<predicate_leaf>::=
{
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )
}

<predicate_source_declaration>::=
{
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )
}

<value>::=
{
    number | 'string'
}

<event_target_definition>::=
{
    ADD TARGET [event_module_guid].event_package_name.target_name
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]
}

<event_session_options>::=
{  
    [    MAX_MEMORY = size [ KB | MB ] ]
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]
    [ [,] STARTUP_STATE = { ON | OFF } ]
}
```

## <a name="arguments"></a>Argumentos

*nome_de_sessão_de_evento* O nome definido pelo usuário para a sessão de evento. *event_session_name* é alfanumérico, pode ter até 128 caracteres, deve ser exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve obedecer às regras de [Identificadores](../../relational-databases/databases/database-identifiers.md).

ADD EVENT [ *guid_do_módulo_de_evento* ]. *nome_do_pacote_de_evento*.*nome_do_evento* O evento a associar à sessão de evento, onde:

- *event_module_guid* é o GUID do módulo que contém o evento.
- *event_package_name* é o pacote que contém o objeto de ação.
- *event_name* é o objeto de evento.

Eventos aparecem na exibição sys.dm_xe_objects como object_type “evento”.

SET { *atributo_personalizável_de_evento*= \<valor> [ ,...*n*] } Permite atributos personalizáveis para o evento a ser definido. Os atributos personalizáveis são mostrados na exibição sys.dm_xe_object_columns como column_type 'personalizável' e object_name = *event_name*.

ACTION ( { [*guid_do_módulo_de_evento*].*nome_do_pacote_de_evento*.*nome_da_ação* [ **,** ...*n*] }) A ação a ser associada à sessão de evento, onde:

- *event_module_guid* é o GUID do módulo que contém o evento.
- *event_package_name* é o pacote que contém o objeto de ação.
- *action_name* é o objeto de ação.

Ações aparecem na exibição sys.dm_xe_objects como object_type “ação”.

WHERE \<predicate_expression> Especifica a expressão de predicado usada para determinar se um evento deve ser processado. Se \<predicate_expression> for verdadeira, o evento será processado mais detalhadamente pelas ações e pelos destinos da sessão. Se \<predicate_expression> for falsa, o evento será removido pela sessão antes de ser processado pelas ações e pelos destinos da sessão. As expressões de predicado são limitadas a 3.000 caracteres, o que limita os argumentos de cadeia de caracteres.

*nome_do_campo_de_evento* O nome do campo de evento que identifica a origem do predicado.

[*guid_do_módulo_de_evento*].*nome_do_pacote_de_evento*.*nome_da_origem_de_predicado* O nome da origem do predicado global, onde:

- *event_module_guid* é o GUID do módulo que contém o evento.
- *event_package_name* é o pacote que contém o objeto de predicado.
- *predicate_source_name* é definido na exibição sys.dm_xe_objects como object_type 'pred_source'.

[*guid_do_módulo_de_evento*].*nome_do_pacote_de_evento*.*nome_da_comparação_de_predicado* O nome do objeto predicado a associar ao evento, onde:

- *event_module_guid* é o GUID do módulo que contém o evento.
- *event_package_name* é o pacote que contém o objeto de predicado.
- *predicate_compare_name* é uma origem global definida na exibição sys.dm_xe_objects como object_type 'pred_compare'.

*número* é qualquer tipo numérico, incluindo **decimal**. Limitações são a falta de memória física disponível ou um número que é muito grande para ser representado como um inteiro de 64 bits.

'*cadeia de caracteres*' Uma cadeia de caracteres ANSI ou Unicode, conforme requerido pela comparação de predicado. Nenhuma conversão de tipo de cadeia de caracteres implícita é executada para as funções de comparação de predicado. A transferência do tipo incorreto resulta em um erro.

ADD TARGET [*guid_do_módulo_de_evento*].*nome_do_pacote_de_evento*.*nome_do_destino* O destino a ser associado à sessão de evento, onde:

- *event_module_guid* é o GUID do módulo que contém o evento.
- *event_package_name* é o pacote que contém o objeto de ação.
- *target_name* é o destino. Os destinos aparecem na exibição sys.dm_xe_objects como object_type ‘destino’.

SET { *nome_do_parâmetro_de_destino*= \<valor> [, ...*n*] } Define um parâmetro de destino. Os parâmetros de destino são mostrados na exibição sys.dm_xe_object_columns como column_type 'personalizável' e object_name = *target_name*.

> [!IMPORTANT]
> Se você estiver usando o destino de buffer de anel, recomendamos definir o parâmetro de destino max_memory como 2.048 KB (kilobytes) para ajudar a evitar um possível truncamento de dados da saída XML. Para obter mais informações sobre como usar os diferentes tipos de destino, consulte [Destinos de eventos estendidos do SQL Server](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).

WITH ( \<event_session_options> [ ,...*n*] ) Especifica as opções a serem usadas com a sessão de evento.

MAX_MEMORY =*tamanho* [ KB | **MB** ] Especifica a quantidade máxima de memória a ser alocada à sessão para buffer de evento. O padrão é 4 MB. *size* é um número inteiro e pode ser um valor de KB (kilobyte) ou MB (megabyte). A quantidade máxima não pode exceder 2 GB (menos de 2048 MB). No entanto, não é recomendável usar valores de memória na faixa de GB.

EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } Especifica o modo de retenção de evento a usar para tratamento de perda de eventos.

**ALLOW_SINGLE_EVENT_LOSS** Um evento pode ser perdido da sessão. Um único evento será descartado somente quando todos os buffers de evento estiverem cheios. A perda de um único evento quando os buffers de evento estão cheios permite características de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitáveis, enquanto minimiza a perda de dados no fluxo de evento processado.

ALLOW_MULTIPLE_EVENT_LOSS Buffers de evento cheios que contêm vários eventos podem ser perdidos da sessão. O número de eventos perdidos depende do tamanho de memória alocado à sessão, do particionamento da memória e do tamanho dos eventos no buffer. Essa opção minimiza o impacto do desempenho no servidor quando buffers de evento são rapidamente enchidos, mas grandes números de eventos podem ser perdidos da sessão.

NO_EVENT_LOSS Nenhuma perda de evento é permitida. Essa opção assegura que todos os eventos gerados sejam retidos. O uso dessa opção força todas as tarefas que acionam eventos a esperar até que haja espaço disponível em um buffer de evento. Isso pode causar problemas de desempenho detectáveis enquanto a sessão de evento está ativa. As conexões de usuário poderão parar enquanto esperam a liberação de eventos do buffer.

MAX_DISPATCH_LATENCY = { *segundos* SECONDS | **INFINITE** } Especifica a quantidade de tempo em que haverá buffer de eventos na memória antes que sejam enviados para destinos de sessão de evento. Por padrão, este valor é definido como 30 segundos.

*segundos* SECONDS O tempo, em segundos, a esperar antes de liberar buffers para os destinos. *seconds* é um número inteiro. O valor mínimo de latência é 1 segundo. No entanto, o valor 0 pode ser usado para especificar a latência INFINITE.

**INFINITE** Libera buffers para os destinos somente quando estiverem cheios ou quando a sessão de evento for fechada.

> [!NOTE]
> MAX_DISPATCH_LATENCY = 0 SECONDS é equivalente a MAX_DISPATCH_LATENCY = INFINITE.

MAX_EVENT_SIZE =*tamanho* [ KB | **MB** ] especifica o tamanho máximo permitido para eventos. MAX_EVENT_SIZE deverá ser definido apenas para permitir eventos únicos maiores que MAX_MEMORY; sua definição como menos que MAX_MEMORY irá gerar um erro. *size* é um número inteiro e pode ser um valor de KB (kilobyte) ou MB (megabyte). Se *size* for especificado em kilobytes, o tamanho mínimo permitido será de 64 KB. Quando MAX_EVENT_SIZE é definido, dois buffers de *size* são criados, além de MAX_MEMORY. Isso significa que a memória total usada para buffer de evento é MAX_MEMORY + 2 * MAX_EVENT_SIZE.

MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU } especifica o local em que são criados buffers de evento.

**NONE** Um único conjunto de buffers é criado na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

PER NODE Um conjunto de buffers é criado para cada nó NUMA.

PER_CPU um conjunto de buffers é criado para cada CPU.

TRACK_CAUSALITY = { ON | **OFF** } especifica se a causalidade deve ou não ser controlada. Se habilitada, a causalidade permitirá que eventos relacionados em conexões de servidor diferentes sejam correlacionados.

STARTUP_STATE = { ON | **OFF** } especifica se essa sessão de evento deve ser iniciada automaticamente quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia.

> [!NOTE]
> Se `STARTUP_STATE = ON`, a sessão de evento somente será iniciada se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for parado e, em seguida, reiniciado.

ON a sessão de evento é iniciada na inicialização.

**OFF** a sessão de evento não é iniciada na inicialização.

## <a name="remarks"></a>Comentários

A ordem de precedência para operadores lógicos é `NOT` (mais alto), seguido por `AND`, seguido por `OR`.

## <a name="permissions"></a>Permissões

No SQL Server, requer a permissão `ALTER ANY EVENT SESSION`.
No Banco de Dados SQL, requer a permissão `ALTER ANY DATABASE EVENT SESSION` no banco de dados.

## <a name="examples"></a>Exemplos

### <a name="sql-server-example"></a>Exemplo do SQL Server

O exemplo a seguir mostra como criar uma sessão de evento denominada `test_session`. Esse exemplo adiciona dois eventos e usa o destino Rastreamento de Eventos do Windows.

```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')
    DROP EVENT session test_session ON SERVER;
GO
CREATE EVENT SESSION test_session
ON SERVER
    ADD EVENT sqlos.async_io_requested,
    ADD EVENT sqlserver.lock_acquired
    ADD TARGET package0.etw_classic_sync_target
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);
GO
```
### <a name="sql-database-example"></a>Exemplo do Banco de Dados SQL

Para obter um exemplo de Banco de Dados SQL, confira o exemplo em [Código de destino do Arquivo de Evento para eventos estendidos no Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-xevent-code-event-file#transact-sql-code)

### <a name="code-examples-can-differ-for-azure-sql-database"></a>Os exemplos de código podem ser diferentes no Banco de Dados SQL do Azure

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>Consulte Também

- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)
- [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)
- [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)
- [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)
- [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)
