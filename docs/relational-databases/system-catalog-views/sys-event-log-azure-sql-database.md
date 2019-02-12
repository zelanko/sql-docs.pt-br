---
title: sys. event_log (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: afef7b79c10b3d7f72d69dbe9bfca8721f6d13ec
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041527"
---
# <a name="syseventlog-azure-sql-database"></a>sys.event_log (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna bem-sucedida [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] conexões, falhas de conexão e deadlocks de banco de dados. Você pode usar essas informações para controlar ou solucionar problemas da atividade de banco de dados com o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!CAUTION]  
> Para instalações de ter um grande número de bancos de dados ou alto número de logons, atividade em sys. event_log pode causar limitações de desempenho, alto uso da CPU e possivelmente resultar em falhas de logon. Consultas de sys. event_log podem contribuir para o problema. Microsoft está trabalhando para resolver esse problema. Enquanto isso, para reduzir o impacto desse problema, limite as consultas de sys. event_log. Os usuários do plugin NewRelic SQL Server devem visitar [ajustes de desempenho e ajuste de plug-in de banco de dados SQL do Microsoft Azure](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729) para obter informações de configuração adicional.  
  
 A exibição `sys.event_log` contém as seguintes colunas.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nome do banco de dados. Se a conexão falhar e o usuário não especificou um nome de banco de dados, essa coluna ficará em branco.|  
|**start_time**|**datetime2**|Data e hora UTC do início do intervalo de agregação. Para eventos agregados, a hora é sempre um múltiplo de 5 minutos. Por exemplo:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|Data e hora UTC do término do intervalo de agregação. Para eventos agregados, **End_time** é sempre exatamente 5 minutos mais tarde do que o correspondente **start_time** na mesma linha. Para eventos que não são agregados **start_time** e **end_time** igual a data real de UTC e a hora do evento.|  
|**event_category**|**nvarchar(64)**|O componente de alto nível que gerou este evento.<br /><br /> Ver [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) para obter uma lista de valores possíveis.|  
|**event_type**|**nvarchar(64)**|O tipo de evento.<br /><br /> Ver [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) para obter uma lista de valores possíveis.|  
|**event_subtype**|**int**|O subtipo do evento que está ocorrendo.<br /><br /> Ver [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) para obter uma lista de valores possíveis.|  
|**event_subtype_desc**|**nvarchar(64)**|A descrição do subtipo de evento.<br /><br /> Ver [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) para obter uma lista de valores possíveis.|  
|**severity**|**int**|A severidade do erro. Os valores possíveis são:<br /><br /> 0 = Informações<br />1 = Aviso<br />2 = Erro|  
|**event_count**|**int**|O número de vezes que esse evento ocorreu para o banco de dados especificado dentro do intervalo de tempo especificado (**start_time** e **end_time**).|  
|**description**|**nvarchar(max)**|Uma descrição detalhada do evento.<br /><br /> Ver [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) para obter uma lista de valores possíveis.|  
|**additional_data**|**XML**|*Observação: Esse valor é sempre NULL para o V12 de banco de dados SQL do Azure. Ver [exemplos](#Deadlock) seção para saber como recuperar eventos de deadlock para V12.*<br /><br /> Para **Deadlock** eventos, esta coluna contém o gráfico de deadlock. Esta coluna é NULL para outros tipos de evento. |  
  
##  <a name="EventTypes"></a> Tipos de evento

 Os eventos registrados por cada linha nesta exibição são identificados por uma categoria (**event_category**), tipo de evento (**event_type**) e um subtipo (**event_subtype**). A tabela a seguir lista os tipos de eventos que estão coletados nessa exibição.  
  
 Para eventos na **conectividade** categoria, informações de resumo estão disponíveis na exibição sys. database_connection_stats.  
  
> [!NOTE]  
> Essa exibição não inclui todos os eventos possíveis do banco de dados [!INCLUDE[ssSDS](../../includes/sssds-md.md)] que podem acontecer, somente os listados aqui. As categorias, os tipos de evento e os subtipos adicionais podem ser adicionadas em versões futuras do [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**conectividade**|**connection_successful**|0|**connection_successful**|0|Conectado com êxito ao banco de dados.|  
|**conectividade**|**connection_failed**|0|**invalid_login_name**|2|O nome de logon não é válido nesta versão do SQL Server.|  
|**conectividade**|**connection_failed**|1|**windows_auth_not_supported**|2|Logons do Windows não têm suporte nesta versão do SQL Server.|  
|**conectividade**|**connection_failed**|2|**attach_db_not_supported**|2|O usuário solicitou anexar um arquivo de banco de dados sem suporte.|  
|**conectividade**|**connection_failed**|3|**change_password_not_supported**|2|O usuário solicitou alterar a senha de logon do usuário que não tem suporte.|  
|**conectividade**|**connection_failed**|4|**login_failed_for_user**|2|Falha de logon do usuário.|  
|**conectividade**|**connection_failed**|5|**login_disabled**|2|O logon foi desabilitado.|  
|**conectividade**|**connection_failed**|6|**failed_to_open_db**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> O banco de dados não pôde ser aberto. Pode ser causada porque o banco de dados não existe ou falta autenticação para abrir o banco de dados.|  
|**conectividade**|**connection_failed**|7|**blocked_by_firewall**|2|O endereço IP do cliente não tem permissão para acessar o servidor.|  
|**conectividade**|**connection_failed**|8|**client_close**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> O cliente pode ter atingido tempo limite ao estabelecer a conexão. Experimente aumentar o tempo limite da conexão.|  
|**conectividade**|**connection_failed**|9|**reconfiguration**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A conexão falhou porque o banco de dados estava passando por uma reconfiguração no momento.|  
|**conectividade**|**connection_terminated**|0|**idle_connection_timeout**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A conexão ficou ociosa por mais tempo do que o limite definido pelo sistema.|  
|**conectividade**|**connection_terminated**|1|**reconfiguration**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi encerrada devido a uma reconfiguração do banco de dados.|  
|**conectividade**|**throttling**|*\<código de motivo >*|**reason_code**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A solicitação é restrita.  Código de motivo da limitação:  *\<código de motivo >*. Para obter mais informações, consulte [limitação do mecanismo](https://msdn.microsoft.com/library/windowsazure/dn338079.aspx).|  
|**conectividade**|**throttling_long_transaction**|40549|**long_transaction**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi terminada porque você tem uma transação de longa execução. Tente encurtar a transação. Para obter mais informações, consulte [limites de recursos](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**conectividade**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi terminada porque ela adquiriu muitos bloqueios. Tente ler ou modificar menos linhas em uma única transação. Para obter mais informações, consulte [limites de recursos](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**conectividade**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi terminada devido a uso excessivo de TEMPDB. Tente modificar a consulta para reduzir o uso de espaço de tabela temporária. Para obter mais informações, consulte [limites de recursos](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**conectividade**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi terminada devido a uso excessivo de espaço de log de transação. Tente modificar menos linhas em uma única transação. Para obter mais informações, consulte [limites de recursos](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**conectividade**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*Observação: Aplica-se somente a V11 de banco de dados SQL do Azure.*<br /><br /> A sessão foi terminada devido a uso excessivo de memória. Tente modificar a consulta para processar menos linhas. Para obter mais informações, consulte [limites de recursos](https://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**engine**|**deadlock**|0|**deadlock**|2|Ocorreu um deadlock.|  
  
## <a name="permissions"></a>Permissões

 Os usuários com permissão para acessar o **mestre** banco de dados têm acesso somente leitura a essa exibição.  
  
## <a name="remarks"></a>Comentários  
  
### <a name="event-aggregation"></a>Agregação de eventos

 As informações de evento para esta exibição são coletadas e agregadas em intervalos de 5 minutos. O **event_count** coluna representa o número de vezes que um determinado **event_type** e **event_subtype** ocorreu para um banco de dados específico dentro de um intervalo de tempo determinado.  
  
> [!NOTE]  
> Alguns eventos, como deadlocks, não são agregados. Para esses eventos, **event_count** será 1 e **start_time** e **end_time** será igual a real data e hora UTC quando o evento ocorreu.  
  
 Por exemplo, se um usuário não puder se conectar ao banco de dados Database1, devido a um nome de logon inválido, sete vezes entre 11:00 e 11:05 em 5/2/2012 (UTC), essas informações estarão disponíveis em uma única linha nesta exibição:  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-starttime-and-endtime"></a>start_time e end_time do intervalo  
 Um evento é incluído em um intervalo de agregação quando ocorre o evento *na* ou _depois_**start_time** e _antes_  **end_time** para esse intervalo. Por exemplo, um evento que ocorre exatamente em `2012-10-30 19:25:00.0000000` seria incluído somente no segundo intervalo mostrado abaixo:  
  
```
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```

### <a name="data-updates"></a>Atualizações de dados

 Os dados nessa exibição são acumulados com o passar do tempo. Normalmente, os dados são acumulados em uma hora de início do intervalo de agregação, mas pode levar até um máximo de 24 horas para que todos os dados apareçam na exibição. Durante esse período, as informações em uma única linha podem ser atualizadas periodicamente.  
  
### <a name="data-retention"></a>Retenção de Dados

 Os dados nessa exibição são retidos por um máximo de 30 dias, ou possivelmente menor dependendo do número de bancos de dados e o número de eventos exclusivos que cada banco de dados gera. Para reter essas informações por um período mais longo, copie os dados em um banco de dados separado. Depois que você faz uma cópia inicial da exibição, as linhas na exibição podem ser atualizadas à medida que os dados são acumulados. Para manter sua cópia de dados atualizada, periodicamente faça uma verificação da tabela das linhas para procurar um aumento na contagem de eventos de linhas existentes e identificar novas linhas (você pode identificar linhas exclusivas usando a hora de início e de término) e, em seguida, atualize sua cópia dos dados com essas alterações.  
  
### <a name="errors-not-included"></a>Erros não incluídos

 Essa exibição não pode incluir todas as informações de conexão e erro:  
  
- Essa exibição não inclui todos os [!INCLUDE[ssSDS](../../includes/sssds-md.md)] erros que podem ocorrer, somente os especificados no banco de dados [tipos de evento](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) neste tópico.  
- Se não houver uma falha do computador dentro do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] datacenter, uma pequena quantidade de dados pode estar falta na tabela de evento.  
- Se um endereço IP tiver sido bloqueado com DoSGuard, os eventos da tentativa de conexão desse endereço IP não poderão ser coletados e não aparecerão nessa exibição.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="simple-examples"></a>Exemplos simples

 A consulta a seguir retorna todos os eventos ocorridos entre o meio-dia em 25/9/2011 e o meio-dia em 28/9/2011 (UTC). Por padrão, os resultados da consulta são classificados por **start_time** (ordem crescente).  

```sql
SELECT * FROM sys.event_log
WHERE start_time >= '2011-09-25 12:00:00'
    AND end_time <= '2011-09-28 12:00:00';  
```

A consulta a seguir retorna todos os eventos de deadlock para o banco de dados Database1 (aplica-se somente à V11 de banco de dados do SQL Azure).  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'deadlock'
    AND database_name = 'Database1';  
```

<a name="Deadlock"></a> A consulta a seguir retorna todos os eventos de deadlock para o banco de dados Database1 (aplica-se somente a V12 de banco de dados SQL do Azure).  

```sql
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]  
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE  
```

A consulta a seguir retorna a limitação rígida nos eventos de threads de trabalho do SQL que ocorreram entre 10:00 e 11:00 em 25/9/2011 (UTC).  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'throttling'
    AND event_subtype = 4194307
    AND start_time >= '2011-09-25 10:00:00'
    AND end_time <= '2011-09-25 11:00:00';  
```

### <a name="db-scoped-extended-event"></a>Eventos estendidos no escopo do BD

 Use o código de exemplo a seguir para configurar a sessão de eventos estendidos (XEvent) no escopo do banco de dados:  

```sql
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```

### <a name="check-for-deadlock"></a>Verificação de Deadlock

Use a consulta a seguir para verificar se há um deadlock.  

```sql
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```

## <a name="see-also"></a>Consulte também

 [Eventos estendidos no banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
 