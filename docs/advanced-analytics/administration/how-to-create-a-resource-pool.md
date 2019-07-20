---
title: Como criar um pool de recursos para R e Python
description: Defina um pool de recursos SQL Server para processos de R ou Python em uma instância do mecanismo de banco de dados SQL Server 2016 ou SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5b58c2a42334352d64aa2cea61a75585f29996c3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344074"
---
# <a name="how-to-create-a-resource-pool-for-machine-learning-in-sql-server"></a>Como criar um pool de recursos para aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como você pode criar e usar um pool de recursos especificamente para gerenciar cargas de trabalho de aprendizado de máquina R e Python no SQL Server. Ele pressupõe que você já instalou e habilitou os recursos de Machine Learning e deseja reconfigurar a instância para dar suporte ao gerenciamento mais refinado dos recursos usados por processo externo, como R ou Python.

O processo inclui várias etapas:

1.  Status da revisão de todos os pools de recursos existentes. É importante entender quais serviços estão usando recursos existentes.
2.  Modificar pools de recursos de servidor.
3.  Crie um novo pool de recursos para processos externos.
4.  Crie uma função de classificação para identificar solicitações de script externo.
5.  Verifique se o novo pool de recursos externos está capturando trabalhos de R ou Python dos clientes ou contas especificados.

##  <a name="bkmk_ReviewStatus"></a> Verificar o status dos pools de recursos existentes
  
1.  Use uma instrução como a seguinte para verificar os recursos alocados para o pool padrão para o servidor.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Resultados de exemplo**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|default|0|100|0|100|100|0|0|

2.  Verifique os recursos alocados ao pool de recursos **externo** padrão.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Resultados de exemplo**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|padrão|100|20|0|2|
 
3.  Nessas configurações padrão do servidor, o tempo de execução externo provavelmente terá recursos insuficientes para concluir a maioria das tarefas. Para alterar isso, você deve modificar o uso de recursos de servidor da seguinte maneira:
  
    -   Reduza a memória máxima do computador que pode ser usada pelo mecanismo de banco de dados.
  
    -   Aumente a memória máxima do computador que pode ser usada pelo processo externo.

## <a name="modify-server-resource-usage"></a>Modificar o uso de recursos do servidor

1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução para limitar o uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **60%** do valor na configuração de 'memória máxima do servidor'.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  Da mesma forma, execute a seguinte instrução para limitar o uso de memória por processos externos para **40%** dos recursos totais do computador.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  Para aplicar essas alterações, você deve reconfigurar e reiniciar o Resource Governor da seguinte maneira:
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  Essas são apenas configurações sugeridas para começar; Você deve avaliar suas tarefas de aprendizado de máquina em relação a outros processos de servidor para determinar o equilíbrio correto para seu ambiente e carga de trabalho.

## <a name="create-a-user-defined-external-resource-pool"></a>Criar um pool de recursos externo definido pelo usuário
  
1.  Quaisquer alterações na configuração do Resource Governor são impostas em todo o servidor e afetam as cargas de trabalho que usam os pools padrão para o servidor, bem como as cargas de trabalho que usam os pools externos.
  
     Portanto, para fornecer um controle mais refinado sobre quais cargas de trabalho devem ter precedência, você pode criar um novo pool de recursos externos definido pelo usuário. Você também deve definir uma função de classificação e atribuí-la ao pool de recursos externos. A palavra-chave **external** é nova.
  
     Comece criando um novo *pool de recursos externos definido pelo usuário*. No exemplo a seguir, o pool é denominado **ds_ep**.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  Crie um grupo de carga de trabalho chamado `ds_wg` para usar em solicitações de sessão de gerenciamento. Para consultas SQL, você usará o pool padrão. Para todos as consultas de processos externos você usará o pool `ds_ep`.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     As solicitações são atribuídas ao grupo padrão sempre que a solicitação não puder ser classificada ou se houver qualquer outra falha de classificação.
  
     Para obter mais informações, consulte [Grupo de carga de trabalho do Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md) e [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).
  
## <a name="create-a-classification-function-for-machine-learning"></a>Criar uma função de classificação para o Machine Learning
  
Uma função de classificação examina tarefas recebidas e determina se a tarefa é do tipo que pode ser executada usando o pool de recursos atual. As tarefas que não atendem aos critérios da função de classificação são atribuídas de volta ao pool de recursos padrão do servidor.
  
1. Comece especificando que uma função de classificação deve ser usada por Resource Governor para determinar os pools de recursos. Você pode atribuir um **NULL** como um espaço reservado para a função de classificação.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  Na função de classificação para cada pool de recursos, defina o tipo de instruções ou solicitações de entrada que devem ser atribuídas ao pool de recursos.
  
     Por exemplo, a função a seguir retorna o nome do esquema atribuído ao pool de recursos externo definido pelo usuário se o aplicativo que enviou a solicitação for 'Microsoft R Host' ou 'RStudio'. Caso contrário, ela retorna o pool de recursos padrão.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Quando a função tiver sido criada, reconfigure o grupo de recursos para atribuir a nova função de classificação para o grupo de recursos externos que você definiu anteriormente.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Verificar os novos pools de recursos e a afinidade

Para verificar se as alterações foram feitas, você deve verificar a configuração da memória do servidor e da CPU para cada um dos grupos de cargas de trabalho associados a esses pools de recursos de instância:

+ o pool padrão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servidor
+ o pool de recursos padrão para processos externos
+ o pool definido pelo usuário para processos externos

1. Execute a seguinte instrução para exibir todos os grupos de carga de trabalho:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Resultados de exemplo**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|interno|Média|25|0|0|0|0|1|2|
    |2|default|Média|25|0|0|0|0|2|2|
    |256|ds_wg|Média|25|0|0|0|0|2|256|
  
2.  Use a nova exibição de catálogo, [Sys. &#40;resource_governor_external_resource_pools Transact-&#41;SQL](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para exibir todos os pools de recursos externos.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Resultados de exemplo**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|padrão|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Para obter mais informações, consulte [Exibições de catálogo do Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).
  
3.  Execute a seguinte instrução para retornar informações sobre os recursos do computador que são relacionados para o pool de recursos externos, se aplicável:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     Nesse caso, como os grupos foram criados com uma afinidade de AUTO, nenhuma informação será exibida. Para obter mais informações, consulte [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="see-also"></a>Confira também

Para obter mais informações sobre como gerenciar recursos de servidor, consulte:

+  [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor exibições &#40;de gerenciamento dinâmico relacionadas ao TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Para obter uma visão geral da governança de recursos para o aprendizado de máquina, consulte:

+  [Governança de recursos para Serviços de Machine Learning](../../advanced-analytics/r/resource-governance-for-r-services.md)
