---
title: CREATE RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2830c7ae4166ee0b71b1ddfb9de953c57be2452d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982692"
---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Cria um pool de recursos do Administrador de Recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um pool de recursos representa um subconjunto dos recursos físicos (memória, CPUs e E/S) de uma instância do Mecanismo de Banco de Dados. O Administrador de Recursos permite que um administrador de banco de dados distribua recursos de servidor entre pools de recursos, até um máximo de 64 pools. O Administrador de Recursos não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,...n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,...n]  
```  
  
## <a name="arguments"></a>Argumentos  
*pool_name*  
É o nome definido pelo usuário para o pool de recursos. *pool_name* é alfanumérico, pode ter até 128 caracteres, deve ser exclusivo dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
MIN_CPU_PERCENT =*value*  
Especifica a média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. *value* é um inteiro com uma configuração padrão de 0. O intervalo permitido para *value* é de 0 a 100.  
  
MAX_CPU_PERCENT =*value*  
Especifica a média máxima de largura de banda de CPU que todas as solicitações desse pool de recursos receberão quando houver contenção de CPU. *value* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *value* é de 1 a 100.  
  
CAP_CPU_PERCENT =*value*   
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
Especifica uma extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita o nível de largura de banda de CPU máxima para que ele seja igual ao valor especificado. *value* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *value* é de 1 a 100.  
  
AFFINITY {SCHEDULER = AUTO | ( \<scheduler_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}      
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
Anexe o pool de recursos a agendadores específicos. O valor padrão é AUTO.  
  
O AFFINITY SCHEDULER = **(** \<scheduler_range_spec> **)** mapeia o pool de recursos para as agendas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas pelos IDs especificados. Essas IDs são mapeadas para os valores na coluna scheduler_id em [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 
  
Quando você usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** , o pool de recursos é agrupado com os agendadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são mapeados para as CPUs físicas que correspondem ao nó NUMA ou ao intervalo de nós fornecido. Você pode usar a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para descobrir o mapeamento entre a configuração NUMA física e as IDs de agendador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
```sql  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
MIN_MEMORY_PERCENT =*value*    
Especifica a quantidade mínima de memória reservada para esse pool de recursos que não pode ser compartilhada com outros pools de recursos. *value* é um inteiro com uma configuração padrão de 0. O intervalo permitido para *value* é de 0 a 100.  
  
MAX_MEMORY_PERCENT =*value*    
Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos. *value* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *value* é de 1 a 100.  
  
MIN_IOPS_PER_VOLUME =*value*    
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.  
  
Especifica o mínimo de operações de E/S por segundo (IOPS) por volume de disco para reservar para o pool de recursos. O intervalo permitido para *value* é de 0 a 2^31-1 (2.147.483.647). Especifique 0 para indicar nenhum limite mínimo para o pool. O padrão é 0.  
  
MAX_IOPS_PER_VOLUME =*value*    
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.  
  
Especifica o máximo de operações de E/S por segundo (IOPS) por volume de disco para permitir para o pool de recursos. O intervalo permitido para *value* é de 0 a 2^31-1 (2.147.483.647). Especifique 0 para definir um limite ilimitado para o pool. O padrão é 0.  
  
Se o `MAX_IOPS_PER_VOLUME` para um pool for definido como 0, o pool não será controlado e pode utilizar todos os IOPS no sistema mesmo se outros pools tiverem MIN_IOPS_PER_VOLUME definido. Para esse caso, é recomendável definir o valor de `MAX_IOPS_PER_VOLUME` desse pool para um número alto (por exemplo, o valor máximo 2^31-1) se quiser que esse pool seja controlado para E/S.  
  
## <a name="remarks"></a>Comentários  
`MIN_IOPS_PER_VOLUME` e `MAX_IOPS_PER_VOLUME` especificam as leituras ou gravações mínimas e máximas por segundo. Essas leituras ou gravações podem ser de qualquer tamanho e não indicam a taxa de transferência mínima ou máxima.  
  
Os valores para `MAX_CPU_PERCENT` e `MAX_MEMORY_PERCENT` devem ser maiores que ou iguais aos valores para `MIN_CPU_PERCENT` e `MIN_MEMORY_PERCENT`, respectivamente.  
  
`CAP_CPU_PERCENT` difere de `MAX_CPU_PERCENT` no fato de as cargas de trabalho associadas com o pool poderem usar a capacidade da CPU acima do valor de `MAX_CPU_PERCENT` quando ela está disponível, mas não acima do valor de `CAP_CPU_PERCENT`.  
  
A porcentagem total de CPU para cada componente de afinidade (agendador(es) ou nó(s) NUMA) não deve exceder 100%.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão `CONTROL SERVER`.  
  
## <a name="examples"></a>Exemplos  
### <a name="1-shows-how-to-create-a-resource-pool"></a>1. Mostra como criar um pool de recursos

Este exemplo criou um pool de recursos denominado "bigPool". Esse pool usa as definições padrão do Administrador de Recursos.  
  
```sql  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="2-set-the-cap_cpu_percent-to-a-hard-cap-and-set-affinity-scheduler"></a>2. Definir o CAP_CPU_PERCENT como um limite rígido e definir AFFINITY SCHEDULER

Definir o CAP_CPU_PERCENT para um limite rígido de 30 por cento e define AFFINITY SCHEDULER para um intervalo de 0 a 63, de 128 a 191. 
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
```  
  
### <a name="3-set-min_iops_per_volume-and-max_iops_per_volume"></a>3. Definir MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME   

Definir MIN_IOPS_PER_VOLUME para 20 e MAX_IOPS_PER_VOLUME para 100. Esses valores controlam as operações de leitura e gravação de E/S física que estão disponíveis para o pool de recursos.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)     
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)     
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)     
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)     
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)     
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)     
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)     
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)    
  
