---
title: SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- traces [SQL Server], SQL Server Profiler
- database monitoring [SQL Server], SQL Server Profiler
- tuning databases [SQL Server], SQL Server Profiler
- SQL Server Profiler
- server performance [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler]
- tracing [SQL Server]
- monitoring performance [SQL Server], SQL Server Profiler
- events [SQL Server], SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
- tools [SQL Server], SQL Server Profiler
- database performance [SQL Server], SQL Server Profiler
- trace [SQL Server]
ms.assetid: 3ad5f33d-559e-41a4-bde6-bb98792f7f1a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c9b0bb789dc7571a988c434f526070546d8db454
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211049"
---
# <a name="sql-server-profiler"></a>SQL Server Profiler
  O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é uma interface avançada para criar e gerenciar rastreamentos, e analisar e reproduzir resultados de rastreamento. Os eventos são salvos em um arquivo de rastreamento que posteriormente pode ser analisado ou utilizado para reproduzir uma série específica de etapas na tentativa de diagnosticar um problema.  
  
> [!IMPORTANT]  
>  Estamos anunciando a substituição de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] Trace Capture e o Trace Replay. Esses recursos terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não foi determinada. O namespace *Microsoft.SqlServer.Management.Trace* que contém os objetos Trace and Replay do Microsoft SQL Server também será substituído. Observe que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para as cargas de trabalho do Analysis Services não está sendo substituído e o suporte para ele continuará.  
>   
>  A tabela a seguir mostra os recursos que devem ser usados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para capturar e reproduzir seus dados de rastreamento:  
  
||||  
|-|-|-|  
|**Recurso\carga de trabalho de destino**|**Mecanismo relacional**|**Analysis Services**|  
|**Captura de rastreamento**|Interface gráfica de usuário Eventos Estendidos no SQL Server Management Studio|SQL Server Profiler|  
|**Reprodução de rastreamento**|Distributed Replay|SQL Server Profiler|  
  
## <a name="benefits-of-sql-server-profiler"></a>Benefícios do SQL Server Profiler  
 O Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é uma interface gráfica do usuário que o Rastreamento do SQL usa para monitorar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou do Analysis Services. Você pode capturar e salvar dados sobre cada evento em um arquivo ou tabela para análise posterior. Por exemplo, é possível monitorar um ambiente de produção para observar quais procedimentos armazenados estão afetando o desempenho devido à lentidão na execução. O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é usado para atividades como:  
  
-   Percorrer consultas problemáticas para localizar a causa do problema.  
  
-   Localizar e diagnosticar consultas de execução lenta.  
  
-   Capturar a série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que resultam em um problema. Em seguida, o rastreamento salvo pode ser usado para replicar o problema em um servidor de teste onde o problema pode ser diagnosticado.  
  
-   Monitorar o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ajustar cargas de trabalho. Para obter mais informações sobre como ajustar o design físico do banco de dados para cargas de trabalho do banco de dados, consulte [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
-   Correlacionar contadores de desempenho para diagnosticar problemas.  
  
 O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] também oferece suporte à execução de auditoria das ações executadas em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As auditorias registram ações relacionadas à segurança para análise posterior por um administrador de segurança.  
  
## <a name="sql-server-profiler-concepts"></a>Conceitos do SQL Server Profiler  
 Para usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você precisa compreender os termos que descrevem o modo de funcionamento da ferramenta.  
  
> [!NOTE]  
>  Ao trabalhar com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], é útil compreender o Rastreamento do SQL. Para obter mais informações, consulte [SQL Trace](../../relational-databases/sql-trace/sql-trace.md).  
  
 **Event**  
 Um evento é uma ação gerada dentro de uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. São exemplos:  
  
-   Conexões, falhas e desconexões de logon.  
  
-   Instruções Transact-SQL SELECT, INSERT, UPDATE e DELETE.  
  
-   Status de lote de chamadas de procedimento remoto (RPC).  
  
-   O início ou término de um procedimento armazenado.  
  
-   O início ou término de instruções dentro de procedimentos armazenados.  
  
-   O início ou término de um lote de SQL.  
  
-   Um erro gravado no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Um bloqueio adquirido ou liberado em um objeto de banco de dados.  
  
-   Um cursor aberto.  
  
-   Verificações de permissão de segurança.  
  
 Todos os dados gerados por um evento são exibidos no rastreamento em uma única linha. Esta linha é cruzada por colunas de dados que descrevem o evento em detalhes.  
  
 **EventClass**  
 Uma classe de evento é um tipo de evento que pode ser rastreado. A classe de evento contém todos os dados que podem ser informados por um evento. São exemplos de classes de evento:  
  
-   **SQL:BatchCompleted**  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **Lock:Acquired**  
  
-   **Lock:Released**  
  
 **EventCategory**  
 Uma categoria de evento define o modo pelo qual os eventos são agrupados no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Por exemplo, todas as classes de eventos de bloqueio são agrupadas dentro da categoria de evento **Locks** . Categorias de evento, contudo, só existem dentro do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Este termo não reflete o modo pelo qual são agrupados eventos do Mecanismo.  
  
 **DataColumn**  
 Uma coluna de dados é um atributo de uma classe de evento capturada no rastreamento. Como a classe de evento determina o tipo de dados que pode ser coletado, nem todas as colunas de dados se aplicam a todas as classes de evento. Por exemplo, em um rastreamento que captura a classe de evento **Lock:Acquired** , a coluna de dados **BinaryData** contém o valor da ID de página ou linha bloqueada, mas a coluna de dados **Integer Data** não contém nenhum valor, pois ela não se aplica à classe de evento que está sendo capturada.  
  
 **Modelo**  
 Um modelo define a configuração padrão para um rastreamento. Especificamente, ele contém as classes de evento que se quer monitorar com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Por exemplo, você pode criar um modelo que especifique os eventos, colunas de dados e filtros a usar. Um modelo não é executado, mas, sim, salvo como um arquivo de extensão .tdf. Uma vez salvo, o modelo controla os dados capturados quando um rastreamento que o tem por base é ativado.  
  
 **Rastreamento**  
 Um rastreamento captura dados segundo classes de evento, colunas de dados e filtros selecionados. Por exemplo, você pode criar um rastreamento para monitorar erros de exceção. Para tanto, deve-se selecionar a classe de evento **Exception** e as colunas de dados **Error**, **State**e **Severity** . É preciso coletar os dados dessas três colunas para que os dados produzidos pelo rastreamento façam sentido. Em seguida, você pode executar um rastreamento configurado dessa forma e coletar dados sobre todo evento **Exception** que ocorrer no servidor. O rastreamento pode ser salvo ou utilizado para análise imediata. Rastreamentos podem ser reproduzidos em data posterior, embora certos eventos, como **Exception** , nunca sejam reproduzidos. Você também pode salvar o rastreamento como um modelo, para criar rastreamentos semelhantes no futuro.  
  
 O SQL Server dispõe de duas formas de rastrear uma instância sua: através do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou de procedimentos armazenados do sistema.  
  
 **Filtrar**  
 Ao criar um rastreamento ou modelo, você pode definir critérios para filtrar os dados coletados pelo evento. Para impedir que os rastreamentos se tornem grandes demais, você pode filtrá-los de modo que apenas um subconjunto dos dados do evento sejam coletados. Por exemplo, você pode limitar os nomes de usuário do Windows no rastreamento a usuários específicos, reduzindo, assim, os dados de saída.  
  
 Se não houver um filtro definido, serão retornados todos os eventos das classes de evento selecionadas na saída do rastreamento.  
  
## <a name="sql-server-profiler-tasks"></a>Tarefas do SQL Server Profiler  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Lista os modelos predefinidos que o SQL Server fornece para monitorar determinados tipos de eventos, e as permissões necessárias para reproduzir rastreamentos.|[Modelos e permissões do SQL Server Profiler](sql-server-profiler-templates-and-permissions.md)|  
|Descreve como executar o SQL Server Profiler.|[Permissões necessárias para executar o SQL Server Profiler](permissions-required-to-run-sql-server-profiler.md)|  
|Descreve como criar um rastreamento.|[Criar um rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)|  
|Descreve como especificar eventos e colunas de dados para um arquivo de rastreamento.|[Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)|  
|Descreve como salvar resultados de rastreamento em um arquivo.|[Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)|  
|Descreve como salvar resultados de rastreamento em uma tabela.|[Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)|  
|Descreve como filtrar eventos em um rastreamento.|[Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](filter-events-in-a-trace-sql-server-profiler.md)|  
|Descreve como exibir informações de filtro.|[Exibir informações de filtro &#40;SQL Server Profiler&#41;](view-filter-information-sql-server-profiler.md)|  
|Descreve como modificar um filtro.|[Modificar um filtro &#40;SQL Server Profiler&#41;](modify-a-filter-sql-server-profiler.md)|  
|Descreve como definir um tamanho máximo para um arquivo de rastreamento (SQL Server Profiler).|[Definir um tamanho máximo para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)|  
|Descreve como definir um tamanho máximo para uma tabela de rastreamento.|[Definir um tamanho máximo para uma tabela de rastreamento &#40;SQL Server Profiler&#41;](set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)|  
|Descreve como iniciar um rastreamento.|[Iniciar um rastreamento](start-a-trace.md)|  
|Descreve como iniciar automaticamente um rastreamento após a conexão com um servidor.|[Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)|  
|Descreve como filtrar eventos com base na hora de início do evento.|[Filtrar eventos com base na hora de início do evento &#40;SQL Server Profiler&#41;](filter-events-based-on-the-event-start-time-sql-server-profiler.md)|  
|Descreve como filtrar eventos com base na hora de término do evento.|[Filtrar eventos com base na hora de término do evento &#40;SQL Server Profiler&#41;](filter-events-based-on-the-event-end-time-sql-server-profiler.md)|  
|Descreve como filtrar IDs de processo do servidor de filtro (SPIDs) em um rastreamento.|[Filtrar SPIDs &#40;IDs de processo de servidor&#41; em um rastreamento &#40;SQL Server Profiler&#41;](filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)|  
|Descreve como pausar um rastreamento.|[Pausar um rastreamento &#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)|  
|Descreve como interromper um rastreamento.|[Interromper um rastreamento &#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)|  
|Descreve como executar um rastreamento depois que ele tiver sido pausado ou interrompido.|[Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)|  
|Descreve como limpar uma janela de rastreamento.|[Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)|  
|Descreve como fechar uma janela de rastreamento.|[Fechar uma janela de rastreamento &#40;SQL Server Profiler&#41;](close-a-trace-window-sql-server-profiler.md)|  
|Descreve como definir padrões de definição de rastreamento.|[Definir padrões de definição de rastreamento &#40;SQL Server Profiler&#41;](set-trace-definition-defaults-sql-server-profiler.md)|  
|Descreve como definir padrões de exibição de rastreamento.|[Definir padrões de exibição de rastreamento &#40;SQL Server Profiler&#41;](set-trace-display-defaults-sql-server-profiler.md)|  
|Descreve como abrir um arquivo de rastreamento.|[Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)|  
|Descreve como abrir uma tabela de rastreamento.|[Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)|  
|Descreve como reproduzir uma tabela de rastreamento.|[Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)|  
|Descreve como reproduzir um arquivo de rastreamento.|[Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)|  
|Descreve como reproduzir um único evento de cada vez.|[Reproduzir um único evento de cada vez &#40;SQL Server Profiler&#41;](replay-a-single-event-at-a-time-sql-server-profiler.md)|  
|Descreve como reproduzir até um ponto de interrupção.|[Reproduzir em um ponto de interrupção &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)|  
|Descreve como reproduzir até um cursor.|[Reproduzir para um cursor &#40;SQL Server Profiler&#41;](replay-to-a-cursor-sql-server-profiler.md)|  
|Descreve como reproduzir um script Transact-SQL.|[Reproduzir um script Transact-SQL &#40;SQL Server Profiler&#41;](replay-a-transact-sql-script-sql-server-profiler.md)|  
|Descreve como criar um modelo de rastreamento.|[Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)|  
|Descreve como modificar um modelo de rastreamento.|[Modificar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)|  
|Descreve como definir opções de rastreamento globais.|[Definir opções de rastreamento globais &#40;SQL Server Profiler&#41;](set-global-trace-options-sql-server-profiler.md)|  
|Descreve como localizar um valor ou uma coluna de dados durante um rastreamento.|[Localizar um valor ou coluna de dados durante um rastreamento &#40;SQL Server Profiler&#41;](find-a-value-or-data-column-while-tracing-sql-server-profiler.md)|  
|Descreve como derivar um modelo a partir de um rastreamento em execução.|[Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)|  
|Descreve como derivar um modelo a partir de um arquivo de rastreamento ou uma tabela de rastreamento.|[Derivar um modelo de um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)|  
|Descreve como criar um script Transact-SQL para executar um rastreamento.|[Criar um script Transact-SQL para executar um rastreamento &#40;SQL Server Profiler&#41;](create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)|  
|Descreve como exportar um modelo de rastreamento.|[Exportar um modelo de rastreamento &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)|  
|Descreve como importar um modelo de rastreamento.|[Importar um modelo de rastreamento &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)|  
|Descreve como extrair um script de um rastreamento.|[Extrair um script de um rastreamento &#40;SQL Server Profiler&#41;](extract-a-script-from-a-trace-sql-server-profiler.md)|  
|Descreve como correlacionar um rastreamento com dados de log de desempenho do Windows.|[Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)|  
|Descreve como organizar colunas exibidas em um rastreamento.|[Organizar colunas exibidas em um rastreamento &#40;SQL Server Profiler&#41;](organize-columns-displayed-in-a-trace-sql-server-profiler.md)|  
|Descreve como iniciar o SQL Server Profiler.|[Iniciar o SQL Server Profiler](start-sql-server-profiler.md)|  
|Descreve como salvar rastreamentos e rastrear modelos.|[Salvar rastreamentos e modelos de rastreamento](save-traces-and-trace-templates.md)|  
|Descreve como modificar modelos de rastreamento.|[Modificar modelos de rastreamento](modify-trace-templates.md)|  
|Descreve como correlacionar um rastreamento com dados de log de desempenho do Windows.|[Correlacionar um rastreamento com os dados de log de desempenho do Windows](correlate-a-trace-with-windows-performance-log-data.md)|  
|Descreve como exibir e analisar rastreamentos com o SQL Server Profiler.|[Exibir e analisar rastreamentos com o SQL Server Profiler](view-and-analyze-traces-with-sql-server-profiler.md)|  
|Descreve como analisar deadlocks com o SQL Server Profiler.|[Analisar deadlocks com o SQL Server Profiler](analyze-deadlocks-with-sql-server-profiler.md)|  
|Descreve como analisar consultas com resultados de SHOWPLAN no SQL Server Profiler.|[Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](analyze-queries-with-showplan-results-in-sql-server-profiler.md)|  
|Descreve como filtrar rastreamentos com o SQL Server Profiler.|[Filtrar rastreamentos com o SQL Server Profiler](filter-traces-with-sql-server-profiler.md)|  
|Descreve como usar os recursos de reprodução do SQL Server Profiler.|[Reproduzir rastreamentos](replay-traces.md)|  
|Lista os tópicos de ajuda sensível a contexto do SQL Server Profiler.|[Ajuda de F1 do SQL Server Profiler](sql-server-profiler-f1-help.md)|  
|Lista os procedimentos armazenados do sistema que são usados pelo [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar o desempenho e a atividade.|[Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de eventos Bloqueios](../../relational-databases/event-classes/locks-event-category.md)   
 [Categoria de eventos Sessões](../../relational-databases/event-classes/sessions-event-category.md)   
 [Categoria de eventos Procedimentos armazenados](../../relational-databases/event-classes/stored-procedures-event-category.md)   
 [Categoria de eventos TSQL](../../relational-databases/event-classes/tsql-event-category.md)   
 [Monitoramento de desempenho e atividade de servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)  
  
  
