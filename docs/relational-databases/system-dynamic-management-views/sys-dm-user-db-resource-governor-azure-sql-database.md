---
title: sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: bb4c43fa4193d9254d7f06f24bd903f974739e87
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567632"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Retorna as configurações de configuração e a capacidade para um banco de dados do banco de dados SQL de governança de recursos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|INT|ID do banco de dados, exclusivo dentro de um servidor de banco de dados SQL.|
|**logical_database_guid**|UNIQUEIDENTIFIER|Guid lógico do banco de dados de usuário e permanece com a vida útil de um banco de dados do usuário.  Renomear ou definindo um banco de dados para outro SLO não alterar o GUID. |
|**physical_database_guid**|UNIQUEIDENTIFIER|Guid de físico para um banco de dados de usuário que permanece com a vida útil da instância física do banco de dados do usuário. Configuração para um SLO diferente fará com que essa coluna para alterar.|
|**server_name**|NVARCHAR|Nome do servidor lógico.|
|**database_name**|NVARCHAR|Nome do banco de dados lógico.|
|**slo_name**|NVARCHAR|Serviço objetivo geração e nível de hardware.|
|**dtu_limit**|INT|Limite de DTU do banco de dados (NULL para vCore).|
|**cpu_limit**|INT|limite de vCore do banco de dados (NULL para bancos de dados DTU).|
|**min_cpu**|TINYINT|Porcentagem mínima de CPU que pode ser usadas por carga de trabalho do usuário.|
|**max_cpu**|TINYINT|Porcentagem máxima de CPU que pode ser usadas por carga de trabalho do usuário.|
|**cap_cpu**|TINYINT|Limite de porcentagem de CPU para grupos de carga de trabalho do usuário.|
|**min_cores**|SMALLINT|Número de CPUs usadas pelo SQL.|
|**max_dop**|SMALLINT|Grau máximo de paralelismo usado pela carga de trabalho do usuário.|
|**min_memory**|INT|Porcentagem mínima de memória que pode ser usada por carga de trabalho do usuário.|
|**max_memory**|INT|Porcentagem máxima de memória que pode ser usada por carga de trabalho do usuário.|
|**max_sessions**|INT|Limite de sessão para o grupo de usuários.|
|**max_memory_grant**|INT|Máximo de memória concedida para cada consulta na carga de trabalho do usuário, em porcentagem.|
|**max_db_memory**|INT|Limite de memória de pool de buffer de máximo para a carga de trabalho de banco de dados do usuário|
|**govern_background_io**|bit|Indica se as gravações em segundo plano são cobradas a grupo de usuários.|
|**min_db_max_size_in_mb**|BIGINT|Tamanho do arquivo de banco de dados Max mínima, em MB.|
|**max_db_max_size_in_mb**|BIGINT|Máximo máx banco de dados do arquivo, em MB.|
|**default_db_max_size_in_mb**|BIGINT|O padrão de tamanho máximo de arquivo de banco de dados, em MB.|
|**db_file_growth_in_mb**|BIGINT|Crescimento do padrão do arquivo de banco de dados do azure, em MB.|
|**initial_db_file_size_in_mb**|BIGINT|Banco de dados arquivo tamanho padrão, em MB.|
|**log_size_in_mb**|BIGINT|Padrão tamanho arquivo de log, em MB.|
|**instance_cap_cpu**|INT|Limite de CPU no nível de instância.|
|**instance_max_log_rate**|BIGINT|Geração de log de limite de taxa no nível de instância, em bytes por segundo.|
|**instance_max_worker_threads**|INT|Limite de thread de trabalho no nível de instância.|
|**replica_type**|INT|Tipo de réplica, onde 0 é primário, e 1 é secundária.|
|**max_transaction_size**|BIGINT|Espaço de log máximo usado por qualquer transação, em KB.|
|**checkpoint_rate_mbps**|INT|Largura de banda de ponto de verificação, em Mbps.|
|**checkpoint_rate_io**|INT|Taxa de e/s de ponto de verificação no IOs por segundo.|
|**last_updated_date_utc**|DATETIME|Data e hora da última alteração de configuração ou reconfiguração.|
|**primary_group_id**|INT|ID do grupo de cargas de trabalho do usuário primário.|
|**primary_group_max_workers**|INT|Limite de trabalho no nível de grupo de carga de trabalho do usuário primário.|
|**primary_min_log_rate**|BIGINT|Taxa de log mínimo (bytes por segundo) no nível do grupo de carga de trabalho de usuário primário.|
|**primary_max_log_rate**|BIGINT|Taxa de log máximo (bytes por segundo) no nível do grupo de carga de trabalho de usuário primário.|
|**primary_group_min_io**|INT|E/s mínima no nível de grupo de carga de trabalho do usuário primário.|
|**primary_group_max_io**|INT|E/s máxima no nível de grupo de carga de trabalho do usuário primário.|
|**primary_group_min_cpu**|FLOAT|Limite mínimo de porcentagem da CPU no nível de grupo de carga de trabalho do usuário primário.|
|**primary_group_max_cpu**|FLOAT|Limite máximo de porcentagem da CPU no nível de grupo de carga de trabalho do usuário primário.|
|**primary_log_commit_fee**|INT|Taxa de confirmação log taxa governança no nível de grupo de carga de trabalho do usuário primário.|
|**primary_pool_max_workers**|INT|Limite de trabalho no nível do pool de usuário primário.
|**pool_max_io**|INT|Limite máximo de e/s no nível do pool de usuário primário.|
|**govern_db_memory_in_resource_pool**|bit|Indicado se o tamanho máximo do pool de buffers é controlado no nível do pool de recursos. Geralmente é definido para bancos de dados em pools elásticos.|
|**volume_local_iops**|INT|Ss por segundo limite do volume local (por exemplo, c:, d).|
|**volume_managed_xstore_iops**|INT|Ss por segundo limite de conta de armazenamento remoto.|
|**volume_external_xstore_iops**|INT|Ss por segundo limite de conta de armazenamento remoto usada pela telemetria e os backups de BD SQL do Azure.|
|**volume_type_local_iops**|INT|Ss por segundo limite para todos os volumes locais.|
|**volume_type_managed_xstore_iops**|INT|Ss por segundo limite para todas as contas de armazenamento remoto usado pela instância.|
|**volume_type_external_xstore_iops**|INT|Ss por segundo limite para todas as contas de armazenamento remoto usado por backups de BD SQL do Azure e telemetria para a instância.|
|**volume_pfs_iops**|INT|Ss por segundo limite premium para armazenamento de arquivos.|
|**volume_type_pfs_iops**|INT|Ss por segundo limite de todos os premium para armazenamento de arquivos usado pela instância.|
|||

## <a name="permissions"></a>Permissões

Essa exibição exige a permissão VIEW DATABASE STATE.

## <a name="remarks"></a>Comentários

Os usuários podem acessar essa exibição de gerenciamento dinâmico para configuração de governança de recursos e configurações de capacidade para um banco de dados do banco de dados SQL. 

> [!IMPORTANT]
> A maioria dos dados apresentados por esta DMV destina-se para consumo interno e está sujeita a alterações.

## <a name="examples"></a>Exemplos

O exemplo a seguir retorna a instância máxima taxa dados de log ordenados por nome de banco de dados dentro do servidor de banco de dados para um banco de dados individual ou em pool.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Consulte também

- [Governança de taxa de log de transação](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos DTU do banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Limites de recursos de vCore do banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
