---
title: sys. availability_replicas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f3d0e745d2c9f9db062733949134dc66903c93c6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832011"
---
# <a name="sysavailability_replicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Retorna uma linha para cada uma das réplicas de disponibilidade que pertence a um grupo de disponibilidade Always On no cluster de failover WSFC.  
  
Se a instância de servidor local não puder falar com o cluster de failover WSFC, por exemplo, porque o cluster está inativo ou o quorum foi perdido, apenas linhas para réplicas de disponibilidade local são retornadas. Essas linhas conterão apenas as colunas de dados que são armazenados em cache localmente em metadados.  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|ID exclusiva da réplica.|  
|**group_id**|**uniqueidentifier**|A ID exclusiva do grupo de disponibilidade ao qual a réplica pertence.|  
|**replica_metadata_id**|**int**|ID do objeto de metadados local para réplicas de disponibilidade no Mecanismo de Banco de Dados.|  
|**replica_server_name**|**nvarchar(256)**|O nome de servidor da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda essa réplica e, para uma instância não padrão, seu nome de instância.|  
|**owner_sid**|**varbinary (85)**|O SID (identificador de segurança) registrado para essa instância de servidor para o proprietário externo dessa réplica de disponibilidade.<br /><br /> NULL para réplicas de disponibilidade não locais.|  
|**endpoint_url**|**nvarchar(128)**|Representação de cadeia de caracteres do ponto de extremidade de espelhamento de banco de dados especificado pelo usuário usado pelas conexões entre réplicas primária e secundária para sincronização de dados. Para obter informações sobre a sintaxe das URLs de ponto de extremidade, veja [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).<br /><br /> NULL = Não é possível se comunicar com o cluster de failover WSFC.<br /><br /> Para alterar esse ponto de extremidade, use a opção ENDPOINT_URL da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**availability_mode**|**tinyint**|O modo de disponibilidade da réplica. Pode ser:<br /><br /> 0 &#124; confirmação assíncrona. A réplica primária pode confirmar transações sem esperar que a réplica secundária grave o log no disco.<br /><br /> 1 &#124; confirmação síncrona. A réplica primária espera para confirmar uma determinada transação até que a réplica secundária tenha gravado a transação em disco.<br /><br />4 somente &#124; configuração. A réplica primária envia metadados de configuração do grupo de disponibilidade para a réplica de forma síncrona. Os dados do usuário não são transmitidos para a réplica. Disponível no SQL Server 2017 CU1 e posterior.<br /><br /> Para obter mais informações, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).|  
|**availability_mode_desc**|**nvarchar(60)**|Descrição do ** \_ modo de disponibilidade**, um de:<br /><br /> confirmação assíncrona \_<br /><br /> \_confirmação síncrona<br /><br /> \_somente configuração<br /><br /> Para alterar esse modo de disponibilidade de uma réplica de disponibilidade, use a opção AVAILABILITY_MODE da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br/><br>Você não pode alterar o modo de disponibilidade de uma réplica \_ somente para configuração. Você não pode alterar uma \_ réplica somente de configuração para uma réplica secundária ou primária. |  
|**modo de failover \_**|**tinyint**|O [modo de failover](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) da réplica de disponibilidade, um dos:<br /><br /> 0 &#124; failover automático. A réplica é um destino potencial para failovers automáticos.  O failover automático só terá suporte se o modo de disponibilidade estiver definido como confirmação síncrona (** \_ modo de disponibilidade** = 1) e a réplica de disponibilidade estiver sincronizada no momento.<br /><br /> 1 &#124; failover manual. Um failover para um conjunto de réplicas secundário para failover manual deve ser iniciado manualmente pelo administrador de banco de dados. O tipo de failover executado dependerá se a réplica secundária é sincronizada, da seguinte forma:<br /><br /> Se a réplica de disponibilidade não estiver sincronizando ou se ainda estiver sendo sincronizada, somente o failover forçado (com possível perda de dados) poderá ocorrer.<br /><br /> Se o modo de disponibilidade estiver definido como confirmação síncrona **( \_ modo de disponibilidade** = 1) e a réplica de disponibilidade estiver sincronizada no momento, o failover manual sem perda de dados poderá ocorrer.<br /><br /> Para exibir um ROLLUP da integridade da sincronização de banco de dados de cada banco de dados de disponibilidade em uma réplica de disponibilidade, use as colunas ** \_ \_ desc** de integridade de **sincronização \_ ** e de saúde de sincronização da exibição de gerenciamento dinâmico [Sys. dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) . O rollup considera o estado de sincronização de cada banco de dados de disponibilidade e o modo de disponibilidade da réplica de disponibilidade.<br /><br /> **Observação:** Para exibir a integridade da sincronização de um determinado banco de dados de disponibilidade, consulte as colunas ** \_ estado de sincronização** e ** \_ integridade da sincronização** da exibição de gerenciamento dinâmico [Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) .|  
|**modo de failover \_ \_ desc**|**nvarchar(60)**|Descrição do ** \_ modo de failover**, um de:<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> Para alterar o modo de failover, use a \_ opção modo de failover da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**\_tempo limite da sessão**|**int**|O período de tempo limite, em segundos. O período de tempo limite é o tempo máximo que a réplica espera receber uma mensagem de outra réplica antes de considerar que a conexão entre a réplica primária e secundária falhou. O tempo limite da sessão detecta se réplicas secundárias estão conectadas à réplica primária.<br /><br /> Ao detectar uma conexão com falha com uma réplica secundária, a réplica primária considera que a réplica secundária não está \_ sincronizada. Ao detectar uma falha de conexão com a réplica primária, uma réplica secundária simplesmente tenta se conectar outra vez.<br /><br /> **Observação:** Os tempos limite de sessão não causam failovers automáticos.<br /><br /> Para alterar esse valor, use a opção SESSION_TIMEOUT da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**\_função primária \_ permitir \_ conexões**|**tinyint**|Se a disponibilidade permitir todas as conexões ou só conexões de leitura-gravação, um de:<br /><br /> 2 = Todas (padrão)<br /><br /> 3 = Leitura/gravação|  
|**\_função primária \_ permitir \_ conexões \_ desc**|**nvarchar(60)**|Descrição da ** \_ função primária \_ permitir \_ conexões**, uma das:<br /><br /> ALL<br /><br /> LEITURA \_ /gravação|  
|**\_função secundária \_ permitir \_ conexões**|**tinyint**|Se uma réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) pode aceitar conexões de clientes, um dos seguintes:<br /><br /> 0 = Não. Nenhuma conexão é permitida com os bancos de dados na réplica secundária e os bancos de dados não estão disponíveis para acesso de leitura. Essa é a configuração padrão.<br /><br /> 1 = Somente leitura. Somente conexões somente leitura são permitidas com os bancos de dados na réplica secundária. Todos os bancos de dados na réplica estão disponíveis para acesso de leitura.<br /><br /> 2 = Todos. Todas as conexões são permitidas com os bancos de dados na réplica secundária para acesso somente leitura.<br /><br /> Para obter mais informações, confira [Secundárias ativas: Réplicas Secundárias Legíveis &#40;Grupos de Disponibilidade Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|Descrição de **secondary_role_allow_connections**, uma das:<br /><br /> Não<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|A data em que a réplica foi criada.<br /><br /> NULL = Réplica não nesta instância de servidor.|  
|**modify_date**|**datetime**|A data da última modificação da réplica.<br /><br /> NULL = Réplica não nesta instância de servidor.|  
|**backup_priority**|**int**|Representa a prioridade especificada pelo usuário para executar backups nesta réplica em relação às outras réplicas no mesmo grupo de disponibilidade. O valor é um número inteiro no intervalo de 0..100.<br /><br /> Para obter mais informações, confira [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**read_only_routing_url**|**nvarchar(256)**|Ponto de extremidade de conectividade (URL) da réplica de disponibilidade somente leitura. Para obter informações, veja [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION na instância de servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On grupos de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
