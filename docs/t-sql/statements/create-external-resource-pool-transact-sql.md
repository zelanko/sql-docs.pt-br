---
description: CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
title: CREATE EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 59a754655eff7c701a91013e686e7ff1105a4cfe
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283697"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Cria um pool externo para definir recursos para processos externos. Um pool de recursos representa um subconjunto dos recursos físicos (memória e CPUs) de uma instância do Mecanismo de Banco de Dados. O Resource Governor pode distribuir recursos de servidor entre pools de recursos até um máximo de 64 pools.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Para o [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], o pool externo controla `rterm.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], o pool externo controla `rterm.exe`, `python.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
 

## <a name="syntax"></a>Sintaxe  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"

```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*pool_name*  
É o nome definido pelo usuário para o pool de recursos externo. *pool_name* é alfanumérico e pode ter até 128 caracteres. Esse argumento deve ser exclusivo dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve estar de acordo com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
MAX_CPU_PERCENT =*value*  
A média máxima de largura de banda de CPU que todas as solicitações no pool de recursos podem receber quando há contenção de CPU. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.


MAX_MEMORY_PERCENT =*value*  
Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos externos. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

MAX_PROCESSES =*value*  
O número máximo de processos permitidos para o pool de recursos externo. 0 = um limite ilimitado para o pool, que é associado posteriormente apenas pelos recursos do computador.
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
MAX_CPU_PERCENT =*value*  
A média máxima de largura de banda de CPU que todas as solicitações no pool de recursos podem receber quando há contenção de CPU. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

AFFINITY {CPU = AUTO | ( <CPU_range_spec>) | NUMANODE = (\<NUMA_node_range_spec>)} Anexa o pool de recursos externos a CPUs específicas.

AFFINITY CPU = **(** <CPU_range_spec> **)** mapeia o pool de recursos externos para as CPUs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas pelas CPU_IDs fornecidas.

Quando você usa AFFINITY NUMANODE = **(\<NUMA_node_range_spec> **)** , o pool de recursos externos é relacionado por afinidade com as CPUs físicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que correspondem ao nó NUMA ou ao intervalo de nós fornecido. 

MAX_MEMORY_PERCENT =*value*  
Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos externos. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

MAX_PROCESSES =*value*  
O número máximo de processos permitidos para o pool de recursos externo. 0 = um limite ilimitado para o pool, que é associado posteriormente apenas pelos recursos do computador.
::: moniker-end

## <a name="remarks"></a>Comentários

O [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa o pool de recursos quando você executa a instrução [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md).

Para obter informações gerais sobre pools de recursos, consulte [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).

Para obter informações específicas ao gerenciamento de pools de recursos externos usado para o aprendizado de máquina, confira [Governança de recursos para o aprendizado de máquina no SQL Server](../../machine-learning/administration/resource-governor.md). 

## <a name="permissions"></a>Permissões

Requer a permissão `CONTROL SERVER`.

## <a name="examples"></a>Exemplos

O pool externo restringiu o uso da CPU a 75%. O máximo de memória é de 30% da memória disponível no computador.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

## <a name="see-also"></a>Confira também

+ [Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)
+ [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)
+ [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
