---
title: Criar POOL de recursos EXTERNOS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32c33076f26332f2a8510c4660696106bef824b5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-resource-pool-transact-sql"></a>Criar POOL de recursos EXTERNOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cria um pool externo usado para definir recursos para processos externos. Para R Services controla o pool externo `rterm.exe`, `BxlServer.exe`e outros processos gerados por eles. Um pool de recursos representa um subconjunto dos recursos físicos (memória e CPUs) de uma instância do mecanismo de banco de dados. O Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
## <a name="arguments"></a>Argumentos  
 *nome_do_pool*  
 É o nome definido pelo usuário para o pool de recursos externos. *nome_do_pool* é alfanumérico, pode ter até 128 caracteres, deve ser exclusivo dentro de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e deve estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
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
 A instrução a seguir define um pool externo que restringe o uso de CPU para 75% e a memória máxima para 30 por cento da memória disponível no computador.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Opção de configuração de servidor External scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conhecidos do SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [ALTERAR o POOL de recursos EXTERNOS &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.DM resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  


