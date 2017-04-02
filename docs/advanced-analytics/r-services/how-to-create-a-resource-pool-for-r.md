---
title: "Como: Criar um Pool de recursos para R | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Como: Criar um Pool de recursos para R
  Este tópico descreve como você pode criar um pool de recursos especificamente para gerenciar cargas de trabalho de R no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Ele presume que você já tiver instalado os serviços de R (no banco de dados) e deseja reconfigurar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instância para dar suporte ao gerenciamento mais refinado dos recursos usados por R.  
  
 Para obter mais informações sobre como gerenciar recursos do servidor, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) e [Resource Governor relacionados exibições de gerenciamento dinâmico e 40; O Transact-SQL e 41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
 **Etapas**  
  
1.  Verificar o status dos pools de recursos existente  
  
2.  Modificar grupos de recursos do servidor  
  
3.  Criar um novo pool de recursos para processos externos  
  
4.  Crie uma função de classificação para identificar solicitações de R  
  
5.  Verifique se que o novo pool de recursos externo está capturando trabalhos em R  
  
##  <a name="bkmk_ReviewStatus"></a> Verificar o status dos pools de recursos existente  
  
1.  Primeiro, verifique os recursos alocados para o pool padrão para o servidor.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **Resultados**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|padrão|0|100|0|100|100|0|0|  

2.  Verifique os recursos alocados para o padrão **externo** pool de recursos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **Resultados**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|padrão|100|20|0|2|  
 
3.  Essas configurações padrão do servidor, o tempo de execução de R provavelmente terão recursos insuficientes para concluir a maioria das tarefas. Para alterar isso, você deve modificar o uso de recursos de servidor da seguinte maneira:  
  
    -   Reduzir a memória máxima do computador que pode ser usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   Aumente a memória máxima do computador que pode ser usada por um processo externo  
  
## Modificar o uso de recursos do servidor  
  
1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução para limitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilização de memória para **60%** do valor na configuração de 'memória máxima do servidor'.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  Da mesma forma, execute a seguinte instrução para limitar o uso de memória por processos externos para **40%** dos recursos do computador total.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  Para aplicar essas alterações, você deve reconfigurar e reiniciar o Resource Governor da seguinte maneira:  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  Essas são configurações sugeridas apenas para iniciar; Você deve avaliar os requisitos de R em relação a outros processos do servidor para determinar o equilíbrio correto para seu ambiente e a carga de trabalho.  
  
## Criar um pool de recursos externo definido pelo usuário  
  
1.  Quaisquer alterações na configuração do administrador de recursos são impostas em todo o servidor e afetam as cargas de trabalho que usam os pools padrão para o servidor, bem como cargas de trabalho que usam os grupos externos.  
  
     Portanto, para fornecer um controle mais refinado sobre quais cargas de trabalho devem ter precedência, você pode criar um novo pool de recursos externos definida pelo usuário. Você também deve definir uma função de classificação e atribuí-lo ao pool de recursos externos.  
  
     Comece criando um novo *pool de recursos externos definidos pelo usuário*. No exemplo a seguir, o pool é denominado **ds_ep**.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     Observe o novo **EXTERNO** palavra-chave.  
  
2.  Crie um grupo de carga de trabalho chamado `ds_wg` para usar no gerenciamento de solicitações de sessão. Para consultas SQL, você usará o pool padrão; para todos os processos externos consultas usará o `ds_ep` pool.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     As solicitações são atribuídas ao grupo padrão sempre que a solicitação não pode ser classificada, ou se houver qualquer outra falha de classificação.  
  
     Para obter mais informações, consulte [grupo de carga de trabalho do administrador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md) e [CRIAR GRUPO de cargas de TRABALHO & #40. O Transact-SQL e 41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## Criar uma função de classificação para R  
  
1.  Uma função de classificação examina tarefas recebidas e determina se a tarefa é aquele que podem ser executadas usando o pool de recursos atual. Tarefas que não atendem aos critérios da função de classificação são atribuídas para o pool de recursos padrão do servidor.  
  
     Para começar, especificando que uma função de classificação deve ser usada pelo administrador de recursos para determinar os pools de recursos. Você pode atribuir um valor nulo como um espaço reservado para a função de classificação.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
2.  Na função de classificação para cada pool de recursos, você deve definir o tipo de instruções ou solicitações de entrada devem ser atribuídas ao pool de recursos.  
  
     Por exemplo, a função a seguir retorna o nome do esquema atribuído ao pool de recursos externo definido pelo usuário se o aplicativo que enviou a solicitação é 'Microsoft R Host' ou 'RStudio'; Caso contrário, ele retorna o pool de recursos padrão.  
  
    ```  
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
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## Verifique se a afinidade e novos grupos de recursos  
  
1.  Para verificar se as alterações foram feitas, verifique a configuração de memória do servidor e da CPU para cada um dos grupos de carga de trabalho associados a todos os pools de recursos de instância: o pool padrão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server, pool de recursos padrão para processos externos e o pool definido pelo usuário para processos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **Resultados**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|internal|Média|25|0|0|0|0|1|2|  
    |2|padrão|Média|25|0|0|0|0|2|2|  
    |256|ds_wg|Média|25|0|0|0|0|2|256|  
  
2.  Você pode usar a nova exibição de catálogo, [sys.resource_governor_external_resource_pools & #40. O Transact-SQL e 41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para exibir todos os pools de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **Resultados**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|padrão|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     Para obter mais informações, consulte [exibições de catálogo do administrador de recursos & #40. O Transact-SQL e 41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
3.  A instrução a seguir retorna informações sobre os recursos de computador são relacionados ao pool de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     Nesse caso, porque os grupos foram criados com uma afinidade de AUTO, nenhuma informação será exibida. Para obter mais informações, consulte [sys.dm_resource_governor_resource_pool_affinity & #40. O Transact-SQL e 41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).  
  
## Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Governança de recursos para serviços de R](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  