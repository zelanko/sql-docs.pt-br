---
title: ALTERAR o POOL de recursos EXTERNOS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d85123a34de6dea6b76c1dd4ad8dc6af3117764d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTERAR o POOL de recursos EXTERNOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Alterações Resource Governor pool externo que foi definido de recursos para processos externos. Para R Services controla o pool externo `rterm.exe`, `BxlServer.exe`e outros processos gerados por eles.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
## <a name="arguments"></a>Argumentos  
 { *nome_do_pool* | "default"}  
 É o nome de um pool de recursos externos definida pelo usuário existente ou o pool de recursos externos padrão que é criado quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
"default" deve estar entre aspas ("") ou colchetes ([]) quando usado com `ALTER EXTERNAL RESOURCE POOL` para evitar conflito com `DEFAULT`, que é um sistema palavra reservada.  
  
 MAX_CPU_PERCENT =*valor*  
 Especifica a média da CPU largura de banda máxima que todas as solicitações no pool de recursos externos receberão quando houver contenção de CPU. *valor* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *valor* é de 1 a 100.  
  
AFINIDADE {CPU = AUTO | ( \<CPU_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} anexar o pool de recursos externos para CPUs específicas. O valor padrão é AUTO.  
  
AFINIDADE de CPU = **(** \<CPU_range_spec > **)** mapeia o pool de recursos externos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPUs identificados pelo CPU_IDs determinado.
  
Quando você usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, o pool de recursos externos terá uma afinidade com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPUs físicas que correspondem à determinado NUMA nó ou um intervalo de nós.
  
 MAX_MEMORY_PERCENT =*valor*  
 Especifica a memória total do servidor que pode ser usada pelas solicitações nesse pool de recursos externos. *valor* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *valor* é de 1 a 100.  
  
 MAX_PROCESSES =*valor*  
 Especifica o número máximo de processos permitidos para o pool de recursos externos. Especifique 0 para definir um limite ilimitado para o pool que será associado somente ser recursos do computador. O padrão é 0.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa o pool de recursos quando você executar o [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) instrução.  
  
 Para obter mais informações sobre pools de recursos, consulte [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys. resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), e [sys.DM resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
## <a name="examples"></a>Exemplos  
 A instrução a seguir altera um pool externo restringir o uso da CPU para 50% e a memória máxima para 25 por cento da memória disponível no computador.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Opção de configuração de servidor External scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conhecidos do SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

