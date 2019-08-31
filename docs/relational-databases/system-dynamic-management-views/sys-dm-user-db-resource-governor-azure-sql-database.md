---
title: sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176260"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Retorna configurações de governança de recursos e de capacidade para um banco de dados do banco de dados SQL do Azure.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|int|ID do banco de dados, exclusivo em um servidor de banco de dados SQL do Azure.|
|**logical_database_guid**|uniqueidentifier|GUID lógico do banco de dados de usuário e permanece na vida útil de um banco de dados de usuário.  Renomear ou definir um banco de dados para um SLO diferente não alterará o GUID. |
|**physical_database_guid**|uniqueidentifier|O GUID físico de um banco de dados de usuário que permanece na vida útil da instância física do banco de dados do usuário. A configuração para um SLO diferente fará com que essa coluna seja alterada.|
|**server_name**|nvarchar|Nome do servidor lógico.|
|**database_name**|nvarchar|Nome do banco de dados lógico.|
|**slo_name**|nvarchar|Objetivo de nível de serviço e geração de hardware.|
|**dtu_limit**|int|Limite de DTU do banco de dados (nulo para vCore).|
|**cpu_limit**|int|limite vCore do banco de dados (nulo para bancos de dados de DTU).|
|**min_cpu**|tinyint|Porcentagem mínima de CPU que pode ser usada pela carga de trabalho do usuário.|
|**max_cpu**|tinyint|Porcentagem máxima de CPU que pode ser usada pela carga de trabalho do usuário.|
|**cap_cpu**|tinyint|Limite de porcentagem de CPU para grupos de carga de trabalho do usuário.|
|**min_cores**|smallint|Número de CPUs usadas pelo SQL.|
|**max_dop**|smallint|Grau máximo de paralelismo usado pela carga de trabalho do usuário.|
|**min_memory**|int|Porcentagem mínima de memória que pode ser usada pela carga de trabalho do usuário.|
|**max_memory**|int|Porcentagem máxima de memória que pode ser usada pela carga de trabalho do usuário.|
|**max_sessions**|int|Limite de sessão para o grupo de usuários.|
|**max_memory_grant**|int|Concessão de memória máxima para cada consulta na carga de trabalho do usuário, em porcentagem.|
|**max_db_memory**|int|Limite máximo de memória do pool de buffers para a carga de trabalho do BD do usuário|
|**govern_background_io**|bit|Indica se as gravações em segundo plano são cobradas no grupo de usuários.|
|**min_db_max_size_in_mb**|bigint|Tamanho mínimo máximo do arquivo de banco de dados, em MB.|
|**max_db_max_size_in_mb**|bigint|Máximo de arquivo de banco de dados máx., em MB.|
|**default_db_max_size_in_mb**|bigint|Tamanho máximo do arquivo de banco de dados padrão, em MB.|
|**db_file_growth_in_mb**|bigint|Crescimento padrão do arquivo de banco de dados do Azure, em MB.|
|**initial_db_file_size_in_mb**|bigint|Tamanho do arquivo de banco de dados padrão, em MB.|
|**log_size_in_mb**|bigint|Tamanho do arquivo de log padrão, em MB.|
|**instance_cap_cpu**|int|Limite de CPU no nível de instância.|
|**instance_max_log_rate**|bigint|Limite de taxa de geração de log no nível de instância, em bytes por segundo.|
|**instance_max_worker_threads**|int|Limite de thread de trabalho no nível de instância.|
|**replica_type**|int|Tipo de réplica, em que 0 é primário e 1 é secundário.|
|**max_transaction_size**|bigint|Espaço de log máximo usado por qualquer transação, em KB.|
|**checkpoint_rate_mbps**|int|Largura de banda do ponto de verificação, em Mbps.|
|**checkpoint_rate_io**|int|Taxa de e/s de ponto de verificação no IOs por segundo.|
|**last_updated_date_utc**|datetime|Data e hora da última alteração de configuração ou reconfiguração.|
|**primary_group_id**|int|ID do grupo de carga de trabalho do usuário principal.|
|**primary_group_max_workers**|int|Limite do operador no nível do grupo de carga de trabalho do usuário principal.|
|**primary_min_log_rate**|bigint|Taxa mínima de log (bytes por segundo) no nível de grupo de carga de trabalho do usuário principal.|
|**primary_max_log_rate**|bigint|Taxa máxima de log (bytes por segundo) no nível de grupo de carga de trabalho do usuário principal.|
|**primary_group_min_io**|int|E/s mínima no nível de grupo de carga de trabalho do usuário principal.|
|**primary_group_max_io**|int|E/s máxima no nível do grupo de carga de trabalho do usuário principal.|
|**primary_group_min_cpu**|float|Limite de porcentagem mínima de CPU no nível de grupo de carga de trabalho do usuário principal.|
|**primary_group_max_cpu**|float|Limite de porcentagem máxima de CPU no nível de grupo de carga de trabalho do usuário principal.|
|**primary_log_commit_fee**|int|Taxa de confirmação de governança de taxa de log no nível de grupo de carga de trabalho principal.|
|**primary_pool_max_workers**|int|Limite de trabalho no nível do pool de usuários primário.
|**pool_max_io**|int|Limite máximo de e/s no nível do pool de usuários primário.|
|**govern_db_memory_in_resource_pool**|bit|Indicado se o tamanho máximo do pool de buffers é regido no nível do pool de recursos. Geralmente definido para bancos de dados em pools elásticos.|
|**volume_local_iops**|int|Limite de IOs por segundo para o volume local (por exemplo, C:, D:).|
|**volume_managed_xstore_iops**|int|Limite de IOs por segundo para a conta de armazenamento remoto.|
|**volume_external_xstore_iops**|int|Limite de IOs por segundo para a conta de armazenamento remoto usada pelos backups e telemetria do BD SQL do Azure.|
|**volume_type_local_iops**|int|Limite de IOs por segundo para todos os volumes locais.|
|**volume_type_managed_xstore_iops**|int|Limite de IOs por segundo para todas as contas de armazenamento remoto usadas pela instância.|
|**volume_type_external_xstore_iops**|int|Limite de IOs por segundo para todas as contas de armazenamento remoto usadas pelos backups e telemetria do BD SQL do Azure para a instância.|
|**volume_pfs_iops**|int|Limite de IOs por segundo para o armazenamento de arquivos premium.|
|**volume_type_pfs_iops**|int|Limite de IOs por segundo para todo o armazenamento de arquivos Premium usado pela instância.|
|||

## <a name="permissions"></a>Permissões

Essa exibição exige a permissão VIEW DATABASE STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar essa exibição de gerenciamento dinâmico para configuração de governança de recursos e configurações de capacidade para um banco de dados do banco de dados SQL do Azure. 

> [!IMPORTANT]
> A maioria dos dados exibidos por essa DMV destina-se ao consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna dados de taxa de log máximos de instância ordenados pelo nome do banco de dado no servidor de banco de dados para um banco de dados único ou em pool

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Consulte também

- [Governança de taxa de log de transações](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos de DTU de banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Limites de recursos vCore de banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
