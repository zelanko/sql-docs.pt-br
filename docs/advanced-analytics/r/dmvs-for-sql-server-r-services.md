---
title: "DMVs para serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d3c90457c7d55071520546e6362a451427503a52
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="dmvs-for-sql-server-machine-learning-services"></a>DMVs para serviços de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O tópico lista as exibições de catálogo do sistema e DMVs relacionados ao aprendizado de máquina no SQL Server.

Para obter informações sobre eventos estendidos, consulte [eventos estendidos do aprendizado de máquina](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md).

> [!TIP]
> A equipe de produto forneceu personalizar relatórios que você pode usar para monitorar sessões do aprendizado de máquina e a utilização do pacote. Para obter mais informações, consulte [monitorar usando relatórios personalizados no Management Studio de aprendizado de máquina](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="system-configuration-and-system-resources"></a>Configuração do sistema e os recursos do sistema

Você pode monitorar e analisar os recursos usados pelos scripts externos usando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] DMVs e modos de exibição de catálogo de sistema.

+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  Retorna informações de conexões de usuários e de sessões do sistema. Você pode identificar as sessões do sistema, observando a coluna *session_id*. Valores maiores ou iguais a 51 são de conexões de usuário e valores inferiores a 51 são de processos do sistema.

+ [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  Retorna uma linha para cada contador de desempenho do sistema que está sendo usado pelo servidor.  Você pode usar essas informações para ver quantos scripts foram executados, quais scripts foram executados usando o modo de autenticação ou quantas chamadas de R foram emitidas na instância em geral.

  Este exemplo obtém apenas os contadores relacionados ao script de R:

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%External Scripts%'
  ```

  Os contadores a seguir são relatados por esta DMV para scripts externos, por instância:

  + **Total de execuções**: número de processos externos iniciadas por chamadas locais ou remotas
  + **Paralelo execuções**: número de vezes que um script incluiu a  _@parallel_  especificação e que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] foi capaz de gerar e usar um plano de consulta paralela
  + **Execuções de streaming**: número de vezes que o recurso de streaming foi chamado
  + **Execuções de CC do SQL**: número de externos scripts de execução em que a chamada foi instanciada remotamente e do SQL Server foi usado como o contexto de computação
  + **Logons de Autenticação Implícita**: número de vezes que foi feita uma chamada de loopback de ODBC usando a autenticação implícita, ou seja, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] executou a chamada em nome do usuário que estava enviando a solicitação de script
  + **Total de tempo de execução (ms)**: tempo decorrido entre a chamada e a conclusão da chamada
  + **Erros de execução**: número de vezes que os scripts relataram erros. Essa contagem não inclui erros de R.


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  Essa DMV relata uma única linha para cada conta de trabalho que está executando um script externo. Observe que essa conta de trabalho é diferente das credenciais da pessoa que está enviando o script. Se um único usuário do Windows enviasse várias solicitações de script, apenas uma conta de trabalho seria atribuída para manipular todas as solicitações desse usuário. Se um usuário diferente do Windows fizesse logon para executar um script externo, a solicitação seria manipulada por outra conta de trabalho.

  Essa DMV não retornará nenhum resultado se nenhum script estiver em execução no momento, portanto, ela é mais útil para monitorar scripts de execução longa. Ela retorna esses valores:

  + **external_script_request_id**: um GUID, que também é usado como o nome temporário do diretório de trabalho usado para armazenar resultados intermediários e scripts
  + **idioma**: um valor como `R` que indica o idioma do script externo
  + **degree_of_parallelism**: um inteiro que indica o número de paralelo processos que foram usados
  + **external_user_name**: barra inicial de um operador de conta, como **SQLRUser01**

+ [sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  Essa DMV é fornecida para monitoramento internos (telemetria) controlar o número de chamadas de script externo é feito em uma instância. O serviço de telemetria é iniciado quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e um contador com base em disco será incrementado sempre que uma função de aprendizado de máquina específica é chamada.

  O contador é incrementado por chamada para uma função específica de controladas. Por exemplo, se `rxLinMod` for chamado e executado em paralelo, o contador será incrementado em 1.
  
  Em geral, os contadores de desempenho são válidos somente enquanto o processo que os gerou está ativo. Portanto, uma consulta em uma DMV não pode mostrar dados detalhados de serviços que foram interrompidos. Por exemplo, se o Launchpad cria vários trabalhos de R em paralelo que são executados muito rapidamente e, em seguida, são limpos pelo objeto de trabalho do Windows, uma DMV poderá não mostrar nenhum dado.
 
  No entanto, os contadores controlados por esta DMV são mantidos em execução e o estado do contador dm_external_script _execution é preservado através do uso de gravações em disco, mesmo que a instância esteja desligada.
 
 Para obter mais informações sobre contadores de desempenho do sistema usados pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [Usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).

## <a name="resource-governor-views"></a>Modos de exibição do administrador de recursos

Em edições que dão suporte ao administrador de recursos, criar pools de recursos externos para cargas de trabalho de R ou Python pode ser a maneira eficaz en para controlar e gerenciar recursos.

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  Retorna informações sobre o estado, a configuração atual e as estatísticas do pool de recursos.

  > [!IMPORTANT]
  > 
  > Você deve modificar os pools de recursos que se aplicam a outros serviços do servidor antes de alocar recursos adicionais ao R Services.

+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  Uma nova exibição de catálogo que mostra os valores de configuração atuais dos pools de recursos externos.
  Na Enterprise Edition, você pode configurar pools de recursos externos adicionais: por exemplo, você pode decidir lidar com recursos para trabalhos em R em execução no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] separadamente daqueles que se originam em um cliente remoto.

  > [!NOTE]
  > 
  > Standard Edition, todos os trabalhos de script externo executada no mesmo pool de recursos externos padrão.

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  Retorna as estatísticas de grupo de carga de trabalho e a configuração atual do grupo de carga de trabalho. Esta exibição pode ser adicionada a `sys.dm_resource_governor_resource_pools` para obter o nome do pool de recursos.
  Para scripts externos, uma nova coluna foi adicionada, que mostra a ID do pool externo associado ao grupo de carga de trabalho.

+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  Uma nova exibição de catálogo do sistema que permite que você veja os processadores e os recursos que são relacionados a um pool de recursos específico.

  Retorna uma linha por agendador no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], onde cada agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um agendador ou para identificar tarefas sem controle.

  Na configuração padrão, os pools de carga de trabalho são atribuídos automaticamente aos processadores e, portanto, não há valores de afinidade para retornar.

  O agendamento de afinidade mapeia o pool de recursos para os agendamentos do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] identificados pelas IDs especificadas. Essas IDs são mapeadas para os valores de `scheduler_id` coluna `sys.dm_os_schedulers`.


> [!NOTE] 
> 
> Embora a capacidade de configurar e personalizar os pools de recursos esteja disponível apenas nas edições Enterprise e Developer, os pools padrão, bem como as DMVs, estão disponíveis em todas as edições. Portanto, você pode usar esses DMVs na Standard Edition para determinar os limites de recurso para os trabalhos de script externo.

Para obter informações gerais sobre o monitoramento de instâncias [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [Exibição de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) e [Exibições de gerenciamento dinâmico relacionadas ao Resource Governor](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="monitoring-script-execution"></a>A execução do script de monitoramento

Scripts de R e Python que são executados em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] são iniciados pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interface. No entanto, o Launchpad não tem os recursos controlados ou monitorados separadamente, pois ele é considerado como um serviço seguro fornecido pela Microsoft, que gerencia os recursos adequadamente.

Os scripts individuais que são executados sob o serviço Launchpad são gerenciados usando o [o objeto de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). Um objeto de trabalho permite que grupos de processos sejam gerenciados como uma unidade. Cada objeto de trabalho é hierárquico e controla os atributos de todos os processos associados a ele. As operações realizadas em um objeto de trabalho afetam todos os processos associados ao objeto de trabalho.

Portanto, se precisar encerrar um trabalho associado a um objeto, lembre-se de que todos os processos relacionados também serão encerrados. Se você estiver executando um script de R que é atribuído a um objeto de trabalho do Windows e esse script executa um trabalho ODBC relacionado que deve ser encerrado, o processo pai do script de R também será encerrado.

Se você iniciar um script externo que usa o processamento paralelo, um único objeto de trabalho do Windows gerencia todos os processos filho paralelos.

Para determinar se um processo está em execução em um trabalho, use a função `IsProcessInJob`.

## <a name="next-steps"></a>Próximas etapas

[Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
