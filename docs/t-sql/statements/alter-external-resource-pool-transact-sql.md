---
description: ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
title: ALTER EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: de8fe4503436963094dde524c7fb65a677e91826
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464137"
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Altera um pool externo do Resource Governor que especifica os recursos que podem ser usados por processos externos. 

::: moniker range="=sql-server-2016"
Para o [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], o pool externo controla `rterm.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
Para [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], o pool externo controla `rterm.exe`, `python.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
```syntaxsql
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
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
::: moniker range="=sql-server-2016||=sql-server-2017"
 ```syntaxsql

ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
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

{ *pool_name* | "default" }  
É o nome de um pool de recursos externo definido pelo usuário existente ou do pool de recursos externo padrão criado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado.
"default" deve estar entre aspas duplas ("") ou colchetes ([]) quando usado com `ALTER EXTERNAL RESOURCE POOL` para evitar conflito com `DEFAULT`, que é uma palavra reservada do sistema.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
MAX_CPU_PERCENT =*value*  
Especifica a média máxima de largura de banda de CPU que todas as solicitações no pool de recursos podem receber quando há contenção de CPU. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

MAX_MEMORY_PERCENT =*value*  
Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos externos. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

MAX_PROCESSES =*value*  
Especifica o número máximo de processos permitidos para o pool de recursos externos. Especifique 0 para definir um limite ilimitado para o pool, que é associado posteriormente apenas pelos recursos do computador.
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"
MAX_CPU_PERCENT =*value*  
Especifica a média máxima de largura de banda de CPU que todas as solicitações no pool de recursos podem receber quando há contenção de CPU. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}  
Anexe o pool de recursos externos a CPUs específicas.

AFFINITY CPU = **(** \<CPU_range_spec> **)** mapeia o pool de recursos externos para as CPUs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas pelas CPU_IDs fornecidas. Quando você usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** , o pool de recursos externos é relacionado por afinidade com as CPUs físicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que correspondem ao nó NUMA ou ao intervalo de nós fornecido.

MAX_MEMORY_PERCENT =*value*  
Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos externos. *value* é um inteiro. O intervalo permitido para *value* é de 1 a 100.

MAX_PROCESSES =*value*  
Especifica o número máximo de processos permitidos para o pool de recursos externos. Especifique 0 para definir um limite ilimitado para o pool, que é associado posteriormente apenas pelos recursos do computador.
::: moniker-end
## <a name="remarks"></a>Comentários

O [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa o pool de recursos quando você executa a instrução [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md).

Para obter informações gerais sobre pools de recursos, consulte [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  

Para obter informações específicas ao uso de pools de recursos externos para controlar trabalhos de aprendizado de máquina, consulte [Governança de recursos para o aprendizado de máquina no SQL Server](../../machine-learning/administration/resource-governor.md)...
## <a name="permissions"></a>Permissões

Requer a permissão `CONTROL SERVER`.

## <a name="examples"></a>Exemplos

A instrução a seguir altera um pool externo restringindo o uso da CPU a 50% e a memória máxima a 25% da memória disponível no computador.
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

## <a name="see-also"></a>Confira também

+ [Governança de recursos para o aprendizado de máquina no SQL Server](../../machine-learning/administration/resource-governor.md)
+ [Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
