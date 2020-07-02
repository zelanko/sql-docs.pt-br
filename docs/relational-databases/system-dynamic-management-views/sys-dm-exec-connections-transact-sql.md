---
title: sys. dm_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 948feee2b133f7135f753d789cca119af60bd8b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85676665"
---
# <a name="sysdm_exec_connections-transact-sql"></a>sys.dm_exec_connections (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre as conexões estabelecidas com essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os detalhes de cada conexão. Retorna informações de conexão em todo o servidor para SQL Server. Retorna informações de conexão de banco de dados atual para o banco de dados SQL.  
  
> [!NOTE]
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use [sys. Dm_pdw_exec_connections &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Identifica a sessão associada a esta conexão. Permite valor nulo.|  
|most_recent_session_id|**int**|Representa a ID de sessão da solicitação mais recente associada a esta conexão. (As conexões SOAP podem ser reutilizadas por outra sessão.) Permite valor nulo.|  
|connect_time|**datetime**|Carimbo de data/hora de quando a conexão foi estabelecida. Não permite valor nulo.|  
|net_transport|**nvarchar(40)**|Sempre retorna **sessão** quando uma conexão tem Mars (vários conjuntos de resultados ativos) habilitados.<br /><br /> **Observação:** Descreve o protocolo de transporte físico usado por essa conexão. Não permite valor nulo.|  
|protocol_type|**nvarchar(40)**|Especifica o tipo de protocolo da carga. Atualmente faz distinção entre TDS (TSQL) e SOAP. Permite valor nulo.|  
|protocol_version|**int**|Versão do protocolo de acesso a dados associada a esta conexão. Permite valor nulo.|  
|endpoint_id|**int**|Um identificador que descreve qual é o tipo da conexão. Este endpoint_id pode ser usado para consultar a exibição sys.endpoints. Permite valor nulo.|  
|encrypt_option|**nvarchar(40)**|Valor booliano que descreve se a criptografia está habilitada para esta conexão. Não permite valor nulo.|  
|auth_scheme|**nvarchar(40)**|Especifica o esquema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Autenticação do Windows usado com esta conexão. Não permite valor nulo.|  
|node_affinity|**smallint**|Identifica o nó de memória com o qual esta conexão tem afinidade. Não permite valor nulo.|  
|num_reads|**int**|Número de leituras de bytes que ocorreram nesta conexão. Permite valor nulo.|  
|num_writes|**int**|Número de gravações de bytes que ocorreram nesta conexão. Permite valor nulo.|  
|last_read|**datetime**|Carimbo de data/hora de quando a última leitura ocorreu nesta conexão. Permite valor nulo.|  
|last_write|**datetime**|Carimbo de data/hora de quando a última gravação ocorreu nesta conexão. Não permite valor nulo.|  
|net_packet_size|**int**|Tamanho de pacote de rede usado para transferência de informações e de dados. Permite valor nulo.|  
|client_net_address|**varchar(48)**|Endereço do host do cliente conectado a este servidor. Permite valor nulo.<br /><br /> Antes de V12 no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|client_tcp_port|**int**|Número da porta no computador cliente que está associado a esta conexão. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|local_net_address|**varchar(48)**|Representa o endereço IP no servidor ao qual esta conexão foi destinada. Disponível apenas para conexões que usam o provedor de transporte TCP. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|local_tcp_port|**int**|Representa a porta do servidor TCP ao qual esta conexão foi destinada se houver uma conexão que use o transporte TCP. Permite valor nulo.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa coluna sempre retorna NULL.|  
|connection_id|**uniqueidentifier**|Identifica cada conexão exclusivamente. Não permite valor nulo.|  
|parent_connection_id|**uniqueidentifier**|Identifica a conexão primária que a sessão MARS está usando. Permite valor nulo.|  
|most_recent_sql_handle|**varbinary(64)**|O identificador SQL da última solicitação executada nesta conexão. A coluna most_recent_sql_handle sempre está em sincronia com a coluna most_recent_session_id. Permite valor nulo.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="physical-joins"></a>Junções físicas  
 ![Junções para sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-exec-connections-1.gif "Junções para sys.dm_exec_connections")  
  
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
  
## <a name="see-also"></a>Consulte Também  

 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


