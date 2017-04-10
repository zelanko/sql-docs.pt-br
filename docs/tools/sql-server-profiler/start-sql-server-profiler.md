---
title: "Iniciar o SQL Server Profiler | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Profiler [SQL Server Profiler], iniciando"
  - "SQL Server Profiler, iniciando"
  - "iniciando o SQL Server Profiler"
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Iniciar o SQL Server Profiler
  É possível iniciar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de várias maneiras diferentes para dar suporte à coleta da saída de rastreamento em vários cenários. Você pode iniciar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no menu **Iniciar** , no menu **Ferramentas** do [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor e em vários locais do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Quando você inicia o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pela primeira vez e seleciona **Novo Rastreamento** no menu **Arquivo** , o aplicativo exibe uma caixa de diálogo **Conectar ao Servidor** onde é possível especificar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual você deseja se conectar.  
  
### Para iniciar o SQL Server Profiler no menu Iniciar  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Ferramentas de Desempenho**e clique em **SQL Server Profiler**.  
  
### Para iniciar o SQL Server Profiler no Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  No menu [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ferramentas **do Orientador de Otimização do** , clique em **SQL Server Profiler**.  
  
## Iniciando o SQL Server Profiler no Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia cada sessão do Profiler em sua própria instância e mantém a execução se você desligar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Você pode iniciar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em vários locais do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conforme ilustrado nos procedimentos a seguir. Quando é iniciado, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] carrega o contexto de conexão, o modelo de rastreamento e o contexto de filtro de seu ponto de inicialização.  
  
#### Para iniciar o SQL Server Profiler no menu Ferramentas  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Ferramentas** , clique em **SQL Server Profiler**.  
  
#### Para iniciar o SQL Server Profiler no Editor de Consultas  
  
1.  Na barra de menus do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **Nova Consulta**.  
  
2.  No Editor de Consultas, clique com o botão direito do mouse e selecione **Rastrear Consulta no SQL Server Profiler**.  
  
    > [!NOTE]  
    >  O contexto de conexão é a conexão do editor, o modelo de rastreamento é TSQL_SPs e o filtro aplicado é SPID = SPID da janela de consulta.  
  
#### Para iniciar o SQL Server Profiler no Monitor de Atividade  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clique em **Monitor de Atividade**.  
  
2.  Clique no painel **Processos**, clique com o botão direito do mouse no processo cujo perfil você deseja criar e clique em **Rastrear Processo no SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Quando um processo é selecionado, o contexto de conexão é a conexão do Pesquisador de Objetos quando o Monitor de Atividade foi aberto. O modelo de rastreamento é o padrão com base no tipo de servidor e o SPID é igual ao SPID do processo selecionado.  
  
## Segurança do .NET Framework  
 No modo de Autenticação do Windows, a conta do usuário que executa o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve ter permissão para conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para executar rastreamento com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], os usuários também devem ter a permissão ALTER TRACE.  
  
## Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Usar o SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  