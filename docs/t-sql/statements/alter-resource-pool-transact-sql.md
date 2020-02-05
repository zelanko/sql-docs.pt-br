---
title: ALTER RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57849c8d99700f61c251177c3c3195b2277163ae
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982082"
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera uma configuração do pool de recursos do Administrador de Recursos existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,...n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 { *pool_name* |  **"default"** }  
 É o nome de um pool de recursos definido pelo usuário existente ou do pool de recursos padrão criado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado.  
  
 "default" deve estar entre aspas duplas ("") ou colchetes ([]) quando usado com ALTER RESOURCE POOL para evitar conflito com DEFAULT, que é uma palavra reservada de sistema. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Os grupos de carga de trabalho predefinidos e os pools de recursos usam nomes de letras minúsculas, como "padrão". Isso deve ser levado em consideração nos servidores que usam ordenação com diferenciação de maiúsculas e minúsculas. Os servidores com ordenação sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.  
  
 MIN_CPU_PERCENT =*value*  
 Especifica a média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. *value* é um inteiro com uma configuração padrão de 0. O intervalo permitido para *value* é de 0 a 100.  
  
 MAX_CPU_PERCENT =*value*  
 Especifica a média máxima de largura de banda de CPU que todas as solicitações do pool de recursos receberão quando houver contenção de CPU. *value* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *value* é de 1 a 100.  
  
 CAP_CPU_PERCENT =*value*  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Especifica a capacidade máxima da de CPU de destino para solicitações no pool de recursos. *value* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *value* é de 1 a 100.  
  
> [!NOTE]  
>  Devido à natureza estatística da governança de CPU, você poderá notar picos ocasionais que excedem o valor especificado em CAP_CPU_PERCENT.  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Anexe o pool de recursos a agendadores específicos. O valor padrão é AUTO.  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) mapeia o pool de recursos para as agendas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas pelos IDs especificados. Essas IDs são mapeadas para os valores na coluna scheduler_id em [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).  
  
 Quando você usar AFFINITY NAMANODE = (NUMA_node_range_spec), o pool de recursos terá uma afinidade com os agendadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeados para CPUs físicas que correspondem ao nó NUMA especificado ou ao intervalo de nós. Você pode usar a seguinte consulta Transact-SQL para descobrir o mapeamento entre a configuração NUMA física e as IDs de agendador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
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
  
 Especifica o mínimo de operações de E/S por segundo (IOPS) por volume de disco para reservar para o pool de recursos. O intervalo permitido para *value* é de 0 a 2^31-1 (2.147.483.647). Especifique 0 para indicar nenhum limite mínimo para o pool.  
  
 MAX_IOPS_PER_VOLUME =*value*  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.  
  
 Especifica o máximo de operações de E/S por segundo (IOPS) por volume de disco para permitir para o pool de recursos. O intervalo permitido para *value* é de 0 a 2^31-1 (2.147.483.647). Especifique 0 para definir um limite ilimitado para o pool. O padrão é 0.  
  
 Se o MAX_IOPS_PER_VOLUME para um pool for definido como 0, o pool não será controlado e pode utilizar todos os IOPS no sistema mesmo se outros pools tiverem MIN_IOPS_PER_VOLUME definido. Para esses casos, é recomendável definir o valor de MAX_IOPS_PER_VOLUME para esse pool para um número alto (por exemplo, o valor máximo 2^31-1) se você quiser que esse pool seja controlado para E/S.  
  
## <a name="remarks"></a>Comentários  
 MAX_CPU_PERCENT e MAX_MEMORY_PERCENT devem ser maior que ou igual a MIN_CPU_PERCENT e MIN_MEMORY_PERCENT, respectivamente.  
  
 MAX_CPU_PERCENT poderá usar a capacidade da CPU acima do valor de MAX_CPU_PERCENT, se essa capacidade estiver disponível. Embora possa haver picos periódicos acima de CAP_CPU_PERCENT, as cargas de trabalho não devem exceder CAP_CPU_PERCENT por longos períodos de tempo, mesmo quando a capacidade de CPU adicional está disponível.  
  
 A porcentagem total de CPU para cada componente de afinidade (agendador(es) ou nó(s) NUMA) não deve exceder 100%.  
  
 Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Ao alterar um plano que afeta a configuração, a nova configuração só terá efeito nos planos armazenados em cache anteriormente após a execução de DBCC FREEPROCCACHE (*pool_name*), em que *pool_name* é o nome de um pool de recursos do Resource Governor.  
  
-   Se você estiver alterando a AFFINITY de vários agendadores para um único agendador, a execução de DBCC FREEPROCCACHE não será necessária porque os planos paralelos podem ser executados em modo serial. No entanto, isso pode não ser tão eficiente quanto um plano compilado como um plano serial.  
  
-   Se você estiver alterando a AFFINITY de um único agendador para vários agendadores, a execução de DBCC FREEPROCCACHE não será necessária. No entanto, os planos seriais não podem ser executados em paralelo, portanto, limpar o respectivo cache permitirá que novos planos sejam possivelmente compilados usando paralelismo.  
  
> [!CAUTION]  
>  A limpeza de planos armazenados em cache de um pool de recursos que está associado a mais de um grupo de carga de trabalho afetará todos os grupos de cargas de trabalho com o pool de recursos definido pelo usuário identificado por *pool_name*.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mantém todas as configurações padrão de pool de recursos no pool `default`, exceto para `MAX_CPU_PERCENT`, que é alterado para `25`.  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 No exemplo a seguir, o `CAP_CPU_PERCENT` define a extremidade rígida como 80% e `AFFINITY SCHEDULER` é definido como um valor individual 8 e um intervalo de 12 a 16.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
