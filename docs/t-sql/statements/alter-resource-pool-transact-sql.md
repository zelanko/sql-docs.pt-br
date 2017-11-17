---
title: ALTERAR o POOL de recursos (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 662686f08e370f3d3ee4dee3211f28df58e3b171
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera uma configuração do pool de recursos do Administrador de Recursos existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
{SCHED_ID | SCHED_ID TO SCHED_ID}[,…n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,…n]  
```  
  
## <a name="arguments"></a>Argumentos  
 { *nome_do_pool* | **"padrão"** }  
 É o nome de um pool de recursos definido pelo usuário existente ou do pool de recursos padrão criado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado.  
  
 "default" deve estar entre aspas duplas ("") ou colchetes ([]) quando usado com ALTER RESOURCE POOL para evitar conflito com DEFAULT, que é uma palavra reservada de sistema. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Grupos de cargas de trabalho predefinidos e pools de recursos usam nomes de letras minúsculas, como "padrão". Isso deve ser levado em consideração nos servidores que usam agrupamento com diferenciação de maiúsculas e minúsculas. Os servidores com agrupamento sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.  
  
 MIN_CPU_PERCENT =*valor*  
 Especifica a média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. *valor* é um inteiro com uma configuração padrão de 0. O intervalo permitido para *valor* é de 0 a 100.  
  
 MAX_CPU_PERCENT =*valor*  
 Especifica a média máxima de largura de banda de CPU que todas as solicitações do pool de recursos receberão quando houver contenção de CPU. *valor* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *valor* é de 1 a 100.  
  
 CAP_CPU_PERCENT =*valor*  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica a capacidade de CPU máxima do destino para solicitações no pool de recursos. *valor* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *valor* é de 1 a 100.  
  
> [!NOTE]  
>  Devido à natureza estatística de governança de CPU, você pode perceber picos ocasionais exceder o valor especificado em CAP_CPU_PERCENT.  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Anexe o pool de recursos a agendadores específicos. O valor padrão é AUTO.  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) mapeia o pool de recursos para as agendas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas pelos IDs especificados. Essas IDs são mapeadas para os valores na coluna de scheduler_id em [sys.DM os_schedulers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).  
  
 Quando você usar AFFINITY NAMANODE = (NUMA_node_range_spec), o pool de recursos terá uma afinidade com os agendadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeados para CPUs físicas que correspondem ao nó NUMA especificado ou ao intervalo de nós. Você pode usar a seguinte consulta Transact-SQL para descobrir o mapeamento entre a configuração NUMA física e as IDs de agendador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*valor*  
 Especifica a quantidade mínima de memória reservada para esse pool de recursos que não pode ser compartilhada com outros pools de recursos. *valor* é um inteiro com uma configuração padrão de 0. O intervalo permitido para *valor* é de 0 a 100.  
  
 MAX_MEMORY_PERCENT =*valor*  
 Especifica a memória total de servidor que pode ser usada por solicitações nesse pool de recursos. *valor* é um inteiro com uma configuração padrão de 100. O intervalo permitido para *valor* é de 1 a 100.  
  
 MIN_IOPS_PER_VOLUME =*valor*  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o mínimo de operações de E/S por segundo (IOPS) por volume de disco para reservar para o pool de recursos. O intervalo permitido para *valor* é de 0 a 2 ^ 31-1 (2.147.483.647). Especifique 0 para indicar nenhum limite mínimo para o pool.  
  
 MAX_IOPS_PER_VOLUME =*valor*  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o máximo de operações de E/S por segundo (IOPS) por volume de disco para permitir para o pool de recursos. O intervalo permitido para *valor* é de 0 a 2 ^ 31-1 (2.147.483.647). Especifique 0 para definir um limite ilimitado para o pool. O padrão é 0.  
  
 Se o MAX_IOPS_PER_VOLUME para um pool for definido como 0, o pool não será controlado e pode utilizar todos os IOPS no sistema mesmo se outros pools tiverem MIN_IOPS_PER_VOLUME definido. Para esses casos, é recomendável definir o valor de MAX_IOPS_PER_VOLUME para esse pool para um número alto (por exemplo, o valor máximo 2^31-1) se você quiser que esse pool seja controlado para E/S.  
  
## <a name="remarks"></a>Comentários  
 MAX_CPU_PERCENT e MAX_MEMORY_PERCENT devem ser maior que ou igual a MIN_CPU_PERCENT e MIN_MEMORY_PERCENT, respectivamente.  
  
 MAX_CPU_PERCENT pode usar a capacidade da CPU acima do valor de MAX_CPU_PERCENT quando ela está disponível. Embora possa haver picos periódicos acima CAP_CPU_PERCENT, cargas de trabalho não devem exceder CAP_CPU_PERCENT por longos períodos de tempo, mesmo quando a capacidade de CPU adicional está disponível.  
  
 A porcentagem total de CPU para cada componente de afinidade (agendador(es) ou nó(s) NUMA) não deve exceder 100%.  
  
 Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Ao alterar um plano que afetam a configuração, a nova configuração só terão efeito em planos em cache anteriormente após a execução de DBCC FREEPROCCACHE (*nome_do_pool*), onde *nome_do_pool* é o nome de um recurso Pool de recursos do administrador.  
  
-   Se você estiver alterando a AFINIDADE de agendadores vários para um único Agendador, execução de DBCC FREEPROCCACHE não é necessária porque planos paralelos podem executar em modo serial. No entanto, não é tão eficiente quanto um plano compilado como um plano serial.  
  
-   Se você estiver alterando a AFINIDADE de um agendador único a vários agendadores, a execução de DBCC FREEPROCCACHE não é necessária. No entanto, os planos seriais não pode ser executado em paralelo, para que limpar o cache do respectivo permitirá novos planos para potencialmente ser compilado usando paralelismo.  
  
> [!CAUTION]  
>  Planos em cache de um pool de recursos que está associado a mais de um grupo de carga de trabalho de limpeza afetará todos os grupos de cargas de trabalho com o pool de recursos definidos pelo usuário identificado pelo *nome_do_pool*.  
  
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
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

