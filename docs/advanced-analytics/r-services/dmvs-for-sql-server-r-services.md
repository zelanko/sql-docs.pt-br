---
title: "DMVs para servi&#231;os do SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# DMVs para servi&#231;os do SQL Server R

O tópico lista as exibições de catálogo do sistema e DMVs relacionados a [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 


Para obter informações sobre os eventos estendidos, consulte [eventos estendidos do SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).

> [!TIP]
> A equipe de produto fornece relatórios personalizados que você pode usar para monitorar pacotes e sessões de serviços de R. Para obter mais informações, consulte [monitorar serviços de R usando relatórios personalizados no Management Studio](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).
> 

## <a name="system-configuration-and-system-resources"></a>Configuração do sistema e os recursos do sistema

Você pode monitorar e analisar os recursos usados pelos scripts de R usando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] exibições de catálogo do sistema e DMVs.


**Geral**
+ [ DM exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  Retorna informações de conexões de usuários e sessões de sistema. Você pode identificar as sessões de sistema, observando o *session_id* coluna; valores maiores do que ou igual a 51 são conexões de usuário e valores inferiores a 51 são processos do sistema. 



+ [DM os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  Retorna uma linha para cada contador de desempenho do sistema que está sendo usado pelo servidor.  Você pode usar essas informações para ver quantos scripts executados, quais scripts foram executados usando o modo de autenticação ou quantas chamadas R emitidas na instância geral.

  Este exemplo obtém apenas os contadores relacionados ao script R:

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  Os contadores a seguir são relatados por este DMV para scripts externos por instância:

  + **Total de execuções**: número de processos de R iniciados por chamadas locais ou remotas
  + **Paralelo execuções**: número de vezes que um script incluído o @parallel especificação e que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] foi capaz de gerar e usar um plano de consulta paralela
  + **Execuções de streaming**: número de vezes que o recurso de streaming foi invocado. 
  + **Execuções de CC SQL**: número de R scripts executados em que a chamada foi instanciada remotamente e o SQL Server usada como contexto de computação 
  + **AUTH implícita. Logons**: número de vezes que foi feita uma chamada de loopback ODBC usando implícita autenticação; ou seja, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] executou a chamada em nome de usuário que está enviando a solicitação de script
  + **Total de tempo de execução (ms)**: tempo decorrido entre a chamada e a conclusão da chamada.
  + **Erros de execução**: número de vezes que scripts relataram erros. Essa contagem não inclui erros de R.


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  Essa DMV relata uma linha para cada conta de trabalho que está executando um script externo. Observe que essa conta de trabalho é diferente de credenciais da pessoa que está enviando o script. Se um único usuário Windows enviar várias solicitações de script, conta de apenas um trabalho seria atribuída para manipular todas as solicitações do usuário. Se um usuário diferente do Windows fizer logon para executar um script externo, a solicitação seria manipulada por uma conta de trabalho separada. 
  Essa DMV não retornar nenhum resultado se nenhum scripts estão sendo executados no momento; Portanto, é mais útil para monitorar scripts de execução longa. Ele retorna esses valores:
  + **external_script_request_id**: um GUID, que também é usado como o nome temporário do diretório de trabalho usado para armazenar resultados intermediários e scripts.  
  + **idioma**: um valor como `R` que denota a linguagem de script externo.
  + **degree_of_parallelism**: um inteiro que indica o número de paralelo processos que foram usados. 
  + **external_user_name**: uma conta de trabalho barra inicial, como SQLRUser01. 
  

+ [sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  Essa DMV é fornecida para o monitoramento interno (telemetria) controlar o número de chamadas de R é feito em uma instância. O serviço de telemetria é iniciada quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e um contador baseado em disco é incrementado toda vez que uma função específica de R é chamada.

  O contador é incrementado por chamada de uma função. Por exemplo, se `rxLinMod` for chamado e executado em paralelo, o contador será incrementado em 1.
  
  Em geral, os contadores de desempenho são válidos somente enquanto o processo que os gerou está ativo. Portanto, uma consulta em uma DMV não pode mostrar dados detalhados de serviços que foram interrompidos. Por exemplo, se a barra inicial cria vários trabalhos em paralelo R e ainda são executadas muito rapidamente e, em seguida, limpos pelo objeto de trabalho do Windows, um DMV pode não mostrar todos os dados.
 
  No entanto, os contadores rastreados por este DMV são mantidos em execução e estado de dm_external_script _execution contador é preservada usando gravações no disco, mesmo se a instância for desligada.
 
 Para obter mais informações sobre contadores de desempenho do sistema usados pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).

**Modos de exibição do administrador de recursos**

+ [resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  Retorna informações sobre o estado, a configuração atual e as estatísticas do pool de recursos.

  > [!IMPORTANT]
  > 
  > Você deve modificar grupos de recursos que se aplicam a outros serviços do servidor antes de você pode alocar recursos adicionais para os serviços de R.


+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  Uma nova exibição de catálogo que mostra os valores de configuração de pools de recursos externos.
  Na Enterprise Edition, você pode configurar pools de recursos externos adicionais: por exemplo, você pode decidir lidar com recursos para trabalhos em R em execução no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] separadamente daquelas que se originam de um cliente remoto. 

  > [!NOTE]
  > 
  > Standard Edition todos os trabalhos de R são executados no mesmo pool de recursos externo padrão.

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  Retorna estatísticas de grupo de cargas de trabalho e a configuração atual do grupo de carga de trabalho. Esta exibição pode ser unida a sys.dm_resource_governor_resource_pools para obter o nome do pool de recursos.
  Para scripts externos, uma nova coluna foi adicionada que mostra a id do pool externo associado ao grupo de carga de trabalho. 


+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  Uma nova exibição de catálogo do sistema que permite que você veja os processadores e recursos que são relacionados a um pool de recursos específica.

  Retorna uma linha por agendador no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], onde cada agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um agendador ou para identificar tarefas sem controle.

  Nessa configuração, os pools de carga de trabalho são atribuídos automaticamente aos processadores e, portanto, não há nenhum valor de afinidade para retornar.

  O agendamento de afinidade mapeia o pool de recursos para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] agendas identificadas pelos IDs especificados. Essas IDs são mapeadas para os valores na coluna de scheduler_id em DM os_schedulers (Transact-SQL).


> [!NOTE] 
> 
> Embora a capacidade de configurar e personalizar os pools de recursos está disponível apenas no Enterprise e Developer editions, os pools padrão, bem como as DMVs estão disponíveis em todas as edições. Portanto, você pode usar esses DMVs Standard Edition para determinar os limites de recurso para os trabalhos de R. 

Para obter informações gerais sobre o monitoramento de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instâncias, consulte [modos de exibição de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [Resource Governor relacionados exibições de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="r-script-execution-and-monitoring"></a>Monitoramento e execução do Script R

R scripts que são executados em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] são iniciados com o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interface. No entanto, a barra inicial não é recurso controlado ou monitorado separadamente, pois ele é considerado um serviço seguro fornecido pela Microsoft que gerencia os recursos adequadamente.

Scripts de R individuais que são executados sob o serviço Launchpad são gerenciados usando o [objeto de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). Um objeto de trabalho permite que grupos de processos possam ser gerenciados como uma unidade. Cada objeto de trabalho é hierárquico e controla os atributos de todos os processos associados a ele. As operações executadas em um objeto de trabalho afetam todos os processos associados ao objeto de trabalho. 

Portanto, se precisar encerrar um trabalho associado ao objeto, lembre-se de que todos os processos relacionados também serão encerrados. Se você estiver executando um script R que é atribuído a um objeto de trabalho do Windows e esse script executa um trabalho ODBC relacionado que deve ser encerrado, o processo de script R pai também será encerrado. 

Se você iniciar um script R que usa o processamento paralelo, um único objeto de trabalho do Windows gerencia todos os processos filho paralelos.

Para determinar se um processo está em execução em um trabalho, use o `IsProcessInJob` função.

## <a name="see-also"></a>Consulte também
[Gerenciamento e monitoramento](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

