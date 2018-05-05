---
title: sys.DM exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_connections_TSQL
- sys.dm_exec_connections_TSQL
- sys.dm_exec_connections
- dm_exec_connections
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_connections dynamic management view
ms.assetid: 6bd46fe1-417d-452d-a9e6-5375ee8690d8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0a603884ce20003248f217031e2bca76a4c2c612
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecconnections-transact-sql"></a>sys.dm_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as conexões estabelecidas com essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os detalhes de cada conexão. Retorna informações de conexão ampla de servidor para o SQL Server. Retorna informações de conexão de banco de dados atual para o banco de dados SQL.  
  
> [!NOTE]
> Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sys.dm_pdw_exec_connections &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|session_id|**Int**|Identifica a sessão associada a esta conexão. Permite valor nulo.|  
|most_recent_session_id|**Int**|Representa a ID de sessão da solicitação mais recente associada a esta conexão. (As conexões SOAP podem ser reutilizadas por outra sessão.) Permite valor nulo.|  
|connect_time|**datetime**|Carimbo de data/hora de quando a conexão foi estabelecida. Não permite valor nulo.|  
|net_transport|**nvarchar(40)**|Sempre retorna **sessão** quando uma conexão tem vários conjuntos de resultados ativos (MARS) habilitados.<br /><br /> **Observação:** descreve o protocolo de transporte físico usado por esta conexão. Não permite valor nulo.|  
|protocol_type|**nvarchar(40)**|Especifica o tipo de protocolo da carga. Atualmente faz distinção entre TDS (TSQL) e SOAP. Permite valor nulo.|  
|protocol_version|**Int**|Versão do protocolo de acesso a dados associada a esta conexão. Permite valor nulo.|  
|endpoint_id|**Int**|Um identificador que descreve qual é o tipo da conexão. Este endpoint_id pode ser usado para consultar a exibição sys.endpoints. Permite valor nulo.|  
|encrypt_option|**nvarchar(40)**|Valor booliano que descreve se a criptografia está habilitada para esta conexão. Não permite valor nulo.|  
|auth_scheme|**nvarchar(40)**|Especifica o esquema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Autenticação do Windows usado com esta conexão. Não permite valor nulo.|  
|node_affinity|**smallint**|Identifica o nó de memória com o qual esta conexão tem afinidade. Não permite valor nulo.|  
|num_reads|**Int**|Número de leituras de bytes que ocorreram essa conexão. Permite valor nulo.|  
|num_writes|**Int**|Número de gravações de bytes que ocorreram essa conexão. Permite valor nulo.|  
|last_read|**datetime**|Carimbo de data/hora de quando a última leitura ocorreu nesta conexão. Permite valor nulo.|  
|last_write|**datetime**|Carimbo de data/hora de quando a última gravação ocorreu nesta conexão. Não permite valor nulo.|  
|net_packet_size|**Int**|Tamanho de pacote de rede usado para transferência de informações e de dados. Permite valor nulo.|  
|client_net_address|**varchar(48)**|Endereço do host do cliente conectado a este servidor. Permite valor nulo.<br /><br /> Antes de V12 no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|client_tcp_port|**Int**|Número da porta no computador cliente que está associado a esta conexão. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|local_net_address|**varchar(48)**|Representa o endereço IP no servidor ao qual esta conexão foi destinada. Disponível apenas para conexões que usam o provedor de transporte TCP. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|local_tcp_port|**Int**|Representa a porta do servidor TCP ao qual esta conexão foi destinada se houver uma conexão que use o transporte TCP. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|connection_id|**uniqueidentifier**|Identifica cada conexão exclusivamente. Não permite valor nulo.|  
|parent_connection_id|**uniqueidentifier**|Identifica a conexão primária que a sessão MARS está usando. Permite valor nulo.|  
|most_recent_sql_handle|**varbinary(64)**|O identificador SQL da última solicitação executada nesta conexão. A coluna most_recent_sql_handle sempre está em sincronia com a coluna most_recent_session_id. Permite valor nulo.|  
|pdw_node_id|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="physical-joins"></a>Junções físicas  
 ![Junções para sys.DM exec_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-exec-connections-1.gif "junções para sys.DM exec_connections")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
||||  
|-|-|-|  
|dm_exec_sessions.session_id|dm_exec_connections.session_id|Um para um|  
|dm_exec_requests.connection_id|dm_exec_connections.connection_id|Muitos para um|  
|dm_broker_connections.connection_id|dm_exec_connections.connection_id|Um para um|  
  
## <a name="examples"></a>Exemplos  
 Consulta típica para reunir informações sobre a própria conexão de consultas.  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>Consulte também  

 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


