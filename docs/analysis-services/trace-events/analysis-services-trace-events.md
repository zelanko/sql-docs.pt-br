---
title: Eventos de rastreamento do Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- events [Analysis Services]
- event classes [Analysis Services], about event classes
- Profiler [SQL Server Profiler], Analysis Services
- event classes [Analysis Services]
ms.assetid: 6fb219cc-f37e-437a-a544-01cec0953571
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 98e15a75b97eae9c4b2fa4093f03f9c8ccf92000
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="analysis-services-trace-events"></a>Eventos de rastreamento do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Você pode acompanhar a atividade de uma instância do Microsoft SQL Server Analysis Services (SSAS) capturando e analisando os eventos de rastreamento gerados pela instância.  Os eventos de rastreamento são agrupados de forma que você possa localizar facilmente eventos de rastreamento relacionados.  Cada evento de rastreamento contém um conjunto de dados relevantes para o evento; nem todos os dados são relevantes para todos os eventos.  
  
 Eventos de rastreamento podem ser iniciados e capturados usando **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**, consulte [Usar o SQL Server Profiler para monitorar o Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md), ou podem ser iniciados de um comando XMLA como **Eventos Estendidos do SQL Server** e, depois, analisados. Consulte [Monitorar o Analysis Services com os Eventos Estendidos do SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
 As tabelas a seguir descrevem cada categoria de evento e os eventos nessa categoria. Cada tabela contém as seguintes colunas:  
  
**ID do evento**  
 Um valor inteiro que identifica o tipo de evento. Este valor é útil sempre que você está lendo rastreamentos convertidos em tabelas ou arquivos XML para filtrar o tipo de evento.  
  
**Nome do evento**  
 O nome fornecido ao evento em aplicativos cliente do Analysis Services.  
  
**Descrição do evento**  
 Uma breve descrição do evento  
  
 **[Categoria de evento Eventos de Comando](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 Coleção de eventos para comandos.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|15|Command Begin|Início do comando.|  
|16|Command End|Término do comando.|  
  
 **[Categoria de eventos de identificação](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 Coleção de eventos para solicitações de identificação.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|36|Discover Begin|Início da solicitação de descoberta.|  
|38|Discover End|Final da solicitação de descoberta.|  
  
 **[Categoria de evento de identificação do estado do servidor](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 Coleção de eventos para descobertas de estado de servidor.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|Início do Server State Discover.|  
|34|Server State Discover Data|Conteúdo do Server State Discover Response.|  
|35|Server State Discover End|Final do Server State Discover.|  
  
 **[Categoria de evento de erros e de avisos](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 Coleção de eventos para erros de servidor.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|17|Erro|Erro do servidor.|  
  
 **[Categoria de evento File Load and Save](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 Coleção de eventos para relato de operações de armazenamento e salva de arquivo.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|90|File Load Begin|Início do carregamento do arquivo.|  
|91|File Load End|Término do carregamento do arquivo.|  
|92|File Save Begin|Início do salvamento do arquivo.|  
|93|File Save End|File Save End|  
|94|PageOut Begin|Início de PageOut.|  
|95|PageOut End|PageOut End|  
|96|PageIn Begin|Início de PageIn.|  
|97|PageIn End|PageIn End|  
  
 **[Categoria de eventos de bloqueio](../../analysis-services/trace-events/lock-events-category.md)**  
  
 Coleção de eventos relacionados de bloqueio.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|50|Deadlock|Deadlock de bloqueios de metadados.|  
|51|Tempo limite de bloqueio|Tempo limite de bloqueio de metadados.|  
|52|Lock Acquired|Lock Acquired|  
|53|Lock Released|Lock Released|  
|54|Espera de bloqueio|Espera de bloqueio|  
  
 **[Categoria Notification Events](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 Coleção de eventos de notificação.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|39|Notification|Evento de notificação.|  
|40|User Defined|Evento definido pelo usuário.|  
  
 **[Categoria de evento de relatórios de andamento](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 Coleção de eventos para relatórios de andamento.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|Início do relatório de andamento.|  
|6|Progress Report End|Progress report end.|  
|7|Progress Report Current|Relatório de andamento atual.|  
|8|Progress Report Error|Erro do relatório de andamento.|  
  
 **[Categoria Queries Events](../../analysis-services/trace-events/queries-events-category.md)**  
  
 Coleção de eventos para consultas.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Início da consulta.|  
|10|Query End|Término da consulta.|  
  
 **[Categoria de eventos de processamento de consultas](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 Coleção de eventos chave durante o processo de execução de uma consulta.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|70|Início do Cubo de Consulta|Início do cubo de consulta.|  
|71|Final do Cubo de Consulta|Término do cubo de consulta.|  
|72|Calculate Non Empty Begin|Início de cálculo de não vazio.|  
|73|Calculate Non Empty Current|Calcular não vazio atual.|  
|74|Calculate Non Empty End|Término de cálculo de não vazio.|  
|75|Serialize Results Begin|Início da serialização de resultados.|  
|76|Serializar Resultados Atuais|Serializar resultados atuais.|  
|77|Serializar Final de Resultados|Serializar final de resultados.|  
|78|Executar Início do Script do MDX|Executar início do script do MDX.|  
|79|Executar Script do MDX Atual|Executar script do MDX atual. Preterido.|  
|80|Execute Final do Script do MDX|Executar final do script do MDX.|  
|81|Dimensão da consulta|Dimensão da consulta.|  
|11|Subcubo de consulta|Subcubo de consulta, a Otimização Baseada em Uso.|  
|12|Subcubo de consulta detalhado|Subcubo de consulta com informações detalhadas. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|60|Obter Dados de Agregação|Responder a consulta obtendo dados de agregação. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|61|Obter Dados de Cache|Responder a consulta obtendo dados de um dos caches. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|82|Início da Consulta VertiPaq SE|Consulta VertiPaq SE|  
|83|Final da Consulta VertiPaq SE|Consulta VertiPaq SE|  
|84|Uso de recurso|Leituras de relatórios, gravações, uso da cpu após final de comandos e consultas.|  
|85|VertiPaq SE Query Cache Match|Uso do cache de consulta VertiPaq SE|  
|98|Direct Query Begin|Início da consulta direta.|  
|99|Direct Query End|Término da consulta direta.|  
  
 **[Categoria de evento de auditoria de segurança](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 Coleção de classes de evento de auditoria do banco de dados.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|1|Audit Login|Coleta todos os novos eventos de conexão desde o início do rastreamento; por exemplo, quando um cliente solicita uma conexão a um servidor executando uma instância do SQL Server.|  
|2|Audit Logout|Coleta todos os novos eventos de desconexão desde o início do rastreamento; por exemplo, quando um cliente emite um comando de desconexão.|  
|4|Audit Server Starts And Stops|Registra as atividades de desligar, iniciar e pausar serviço.|  
|18|Audit Object Permission Event|Registra alterações na permissão do objeto.|  
|19|Evento de Operações de Administração de Auditoria|Registra backup/restore/synchronize/attach/detach/imageload/imagesave do servidor.|  
  
 [Categoria Session Events](../../analysis-services/trace-events/session-events-event-category.md)  
  
 Coleção de eventos de sessão.  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Conexão existente de usuário.|  
|42|Existing Session|Sessão existente.|  
|43|Session Initialize|Inicialização de sessão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o SQL Server Profiler para monitorar o Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  
