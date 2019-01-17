---
title: Uma referência para o monitoramento e a solução de problemas de grupos de disponibilidade Always On
description: Este guia funciona como uma página de referência para ajudá-lo a começar a monitorar e solucionar alguns dos problemas comuns encontrados com grupos de disponibilidade Always On.
ms.custom: ag-guide, seodec18
ms.date: 05/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 8d6d9954-ff6b-4e58-882e-eff0174f0d07
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 59ca941e6588f00140b4b57fa3a73904b6ad8f35
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215615"
---
# <a name="always-on-availability-groups-troubleshooting-and-monitoring-guide"></a>Guia de solução de problemas e monitoramento dos Grupos de Disponibilidade Always On
 Este guia ajuda você a começar a monitorar Grupos de Disponibilidade Always On e solucionar alguns dos problemas comuns em grupos de disponibilidade. Ele fornece o conteúdo original, bem como uma página inicial com informações úteis que são publicadas em outros lugares. Embora este guia não aborde completamente todos os problemas que podem ocorrer no vasto campo dos grupos de disponibilidade, ele pode indicar a direção correta para sua análise de causa raiz e para a solução de problemas. 
 
 Como os grupos de disponibilidade são uma tecnologia integrada, muitos problemas encontrados podem ser sintomas de outros problemas do seu sistema de banco de dados. Alguns problemas são causados por configurações em um grupo de disponibilidade, como um banco de dados de disponibilidade que está sendo suspenso. Outros problemas podem estar relacionados com outros aspectos do SQL Server, como configurações do SQL Server, implantações de arquivos de banco de dados e problemas de desempenho sistêmicos não relacionados à disponibilidade. Além disso, pode haver outros problemas fora do SQL Server, como problemas de E/S de rede, de TCP/IP, de Active Directory e de WSFC (Cluster de Failover do Windows Server). Muitas vezes, os problemas que rondam um grupo de disponibilidade, uma réplica ou um banco de dados exigem a solução de problemas de várias tecnologias para identificar a causa raiz.  
  
  
##  <a name="BKMK_SCENARIOS"></a> Cenários de solução de problemas  
 A tabela a seguir contém links para os cenários de solução de problemas comuns de grupos de disponibilidade. Eles são categorizados por tipo de cenário, como configuração, conectividade de cliente, failover e desempenho.  
  
|Cenário|Tipo de cenário|Descrição|  
|--------------|-------------------|-----------------|  
|[Solucionar problemas de configuração de Grupos de Disponibilidade Always On &#40;SQL Server&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)|Configuração|Fornece informações para ajudar a solucionar problemas típicos com a configuração de instâncias de servidor de grupos de disponibilidade. Os problemas de configuração típicos incluem grupos de disponibilidade desabilitados, contas configuradas incorretamente, ponto de extremidade de espelhamento de banco de dados inexistente, ponto de extremidade inacessível (Erro 1418 do SQL Server), acesso à rede inexistente e falha no comando de junção de banco de dados (Erro 35250 do SQL Server).|  
|[Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de Disponibilidade Always On&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|Configuração|Uma operação de adição de arquivo fez com que o banco de dados secundário fosse suspenso e entrasse no estado NOT SYNCHRONIZING.|  
|[Não é possível conectar-se ao ouvinte do grupo de disponibilidade em um ambiente de várias sub-redes](https://support.microsoft.com/kb/2792139/en-us)|Conectividade de cliente|Depois de configurar o ouvinte do grupo de disponibilidade, não será possível fazer ping do ouvinte ou se conectar a ele por meio de um aplicativo.|  
|[Solução de problemas de failovers automáticos com falha](https://support.microsoft.com/kb/2833707)|Failover|Um failover automático não foi concluído com êxito.|  
|[Solução de problemas: o grupo de disponibilidade excedeu o RTO](troubleshoot-availability-group-exceeded-rto.md)|Desempenho|Após um failover automático ou um failover manual planejado sem perda de dados, o tempo de failover excede o RTO. Ou, quando você calcula o tempo de failover de uma réplica secundária de confirmação síncrona (como um parceiro de failover automático), você descobre que ele excede o RTO.|  
|[Solução de problemas: o grupo de disponibilidade excedeu o RPO](troubleshoot-availability-group-exceeded-rpo.md)|Desempenho|Depois de executar um failover manual forçado, a perda de dados é maior que o RPO. Ou, ao calcular a possível perda de dados de uma réplica secundária de confirmação assíncrona, você descobre que ela excede o RPO.|  
|[Solução de problemas: as alterações na réplica primária não são refletidas na réplica secundária](troubleshoot-primary-changes-not-reflected-on-secondary.md)|Desempenho|O aplicativo cliente conclui uma atualização na réplica primária com êxito, mas uma consulta à réplica secundária mostra que a alteração não foi refletida.|  
|[Solução de problemas: tipo de espera HADR_SYNC_COMMIT alto com Grupos de Disponibilidade Always On](https://blogs.msdn.microsoft.com/sql_server_team/troubleshooting-high-hadr_sync_commit-wait-type-with-always-on-availability-groups/)|Desempenho|Se HADR_SYNC_COMMIT é muito longo, há um problema de desempenho no fluxo de movimentação de dados ou na proteção de logs da réplica secundária.|  

##  <a name="BKMK_TOOLS"></a> Ferramentas úteis para solução de problemas  
 Ao configurar ou executar grupos de disponibilidade, diversas ferramentas podem ajudá-lo a diagnosticar diferentes tipos de problemas. A tabela a seguir fornece links para informações úteis sobre as ferramentas.  
  
|Ferramenta|Descrição|  
|----------|-----------------|  
|[Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)|Oferece relatório em uma exibição resumida da integridade de seu grupo de disponibilidade com uma interface fácil de usar.|  
|[Políticas Always On](always-on-policies.md)|Usado pelo Painel Always On.|  
|[Log de erros do SQL Server &#40;Grupos de Disponibilidade Always On&#41;](sql-server-error-log-always-on-availability-groups.md)|Registra eventos de transição de estado de grupos, réplicas e bancos de dados de disponibilidade, status de outros componentes Always On e erros do Always On.|  
|[CLUSTER.LOG &#40;Grupos de Disponibilidade Always On&#41;](cluster-log-always-on-availability-groups.md)|Registra eventos de cluster, inclusive transições de estado do recurso do grupo de disponibilidade, bem como eventos e erros de DLL de recurso do SQL Server.|  
|[Log de diagnóstico de integridade do Always On](always-on-health-diagnostics-log.md)|Registra diagnóstico de integridade do SQL Server conforme relatado para o cluster WSFC (DLL de recurso do SQL Server) por [sp_server_diagnostics &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).|  
|[Exibições de gerenciamento dinâmico e exibições de catálogo do sistema &#40;Grupos de Disponibilidade Always On&#41;](dynamic-management-views-and-system-catalog-views-always-on-availability-groups.md)|Fornece informações sobre os grupos de disponibilidade como métricas de desempenho, configuração e status de integridade.|  
|[Eventos estendidos de Always On](always-on-extended-events.md)|Fornecem um diagnóstico detalhado dos grupos de disponibilidade e são úteis para análise de causa raiz.|  
|[Tipos de espera de Always On](always-on-wait-types.md)|Fornecem estatísticas de espera específicas de grupos de disponibilidade e são úteis para ajuste de desempenho.|  
|Contadores de desempenho do Always On|Monitoram a atividade de grupos de disponibilidade, são refletidos no Monitor do Sistema e são úteis para ajuste de desempenho. Para obter mais informações, veja [SQL Server, réplica de disponibilidade](~/relational-databases/performance-monitor/sql-server-availability-replica.md) e [SQL Server, réplica de banco de dados](~/relational-databases/performance-monitor/sql-server-database-replica.md).|  
|[Buffers de anéis do Always On](always-on-ring-buffers.md)|Registram alertas no sistema do SQL Server para diagnósticos internos e podem ser usados para depurar problemas relacionados aos grupos de disponibilidade.|  
  
##  <a name="BKMK_MONITOR"></a> Monitorando grupos de disponibilidade  
 O momento ideal para solucionar problemas de um grupo de disponibilidade é antes que o problema exija um failover automático ou manual. Isso pode ser feito pelo monitoramento de métricas de desempenho do grupo de disponibilidade e pelo envio de alertas quando as réplicas de disponibilidade estiverem com um desempenho fora dos limites do SLA (Contrato de Nível de Serviço). Por exemplo, se uma réplica secundária síncrona tiver problemas de desempenho que causam aumento no tempo estimado de failover, não será interessante esperar até que um failover automático ocorra e você descubra que o tempo de failover é maior que sua meta de tempo de recuperação.  
  
 Como os grupos de disponibilidade são uma solução alta disponibilidade e recuperação de desastre, as métricas de desempenho mais importantes para monitorar são o tempo estimado de failover, que afeta o seu RTO (objetivo de tempo de recuperação), e a potencial perda de dados em um desastre, que afeta seu RPO (objetivo de ponto de recuperação). Você pode reunir essas métricas com os dados que o SQL Server expõe a qualquer momento, para ser alertado a respeito de um problema nos recursos de HADR (recuperação de desastres de alta disponibilidade) do seu sistema antes da ocorrência real de eventos de falha. Portanto, é importante se familiarizar com o processo de sincronização de dados dos grupos de disponibilidade e coletar as métricas de maneira adequada.  
  
 A tabela abaixo aponta para tópicos que podem ajudá-lo a monitorar a integridade da solução de grupos de disponibilidade.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Monitorar o desempenho de Grupos de Disponibilidade Always On](monitor-performance-for-always-on-availability-groups.md)|Descreve o processo de sincronização de dados para grupos de disponibilidade, os portões de controle de fluxo e as métricas úteis ao monitorar um grupo de disponibilidade; também mostra como coletar métricas de RTO e RPO.|  
|[Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)|Fornece informações sobre ferramentas para monitorar um grupo de disponibilidade.|  
|[The Always On health model, part 1: Health model architecture](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx) (O modelo de integridade do Always On, parte 1: arquitetura do modelo de integridade)|Fornece uma visão geral do modelo de integridade do Always On.|  
|[The Always On health model, part 2: Extending the health model](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (O modelo de integridade do Always On, parte 2: estendendo o modelo de integridade)|Mostra como personalizar o modelo de integridade Always On e personalizar o Painel Always On para mostrar informações adicionais.|  
|[Monitoring Always On health with PowerShell, part 1: Basic cmdlet overview](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 1: visão geral básica de cmdlet)|Fornece uma visão geral básica de cmdlets do PowerShell para o Always On que podem ser usados para monitorar a integridade de um grupo de disponibilidade.|  
|[Monitoring Always On health with PowerShell, part 2: Advanced cmdlet usage](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 2: uso avançado de cmdlet)|Fornece informações sobre o uso avançado dos cmdlets do PowerShell para o Always On para monitorar a integridade de um grupo de disponibilidade.|  
|[Monitoring Always On health with PowerShell, part 3: A simple monitoring application](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 3: um aplicativo de monitoramento simples)|Mostra como monitorar automaticamente um grupo de disponibilidade com um aplicativo.|  
|[Monitoring Always On health with PowerShell, part 4: Integration with SQL Server Agent](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 4: integração ao SQL Server Agent)|Fornece informações sobre como integrar o monitoramento do grupo de disponibilidade com o SQL Server Agent e configurar notificações para as pessoas apropriadas quando surgirem problemas.|  

## <a name="next-steps"></a>Próximas etapas  
 [Blog da equipe do Always On do SQL Server](https://blogs.msdn.com/b/sqlalwayson/)   
 [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
  
