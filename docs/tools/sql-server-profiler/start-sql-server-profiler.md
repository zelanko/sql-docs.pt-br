---
title: Executar o SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 7/7/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 250ea8227a4bd045883322ba2fec3e923336a5e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="run-sql-server-profiler"></a>Executar o SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode executar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de várias maneiras diferentes, para dar suporte à coleta da saída do rastreamento em uma variedade de cenários. Você pode iniciar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] por meio do menu **Iniciar** do Windows 10, do menu **Ferramentas** no [!INCLUDE[ssDE](../../includes/ssde-md.md)] Orientador de Otimização e de vários locais no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Quando você inicia o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pela primeira vez e seleciona **Novo Rastreamento** no menu **Arquivo**, o aplicativo exibe uma caixa de diálogo **Conectar ao Servidor** na qual é possível especificar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual você deseja se conectar.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Para iniciar o SQL Server Profiler no menu Iniciar do Windows 10  
-  Clique em Windows **iniciar** ícone ou pressione as janelas de chave e começam a digitar "SQL Server Profiler 17". Quando o **SQL Server Profiler 17** bloco for exibida, clique nela.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>Para iniciar o SQL Server Profiler no Orientador de Otimização do Mecanismo de Banco de Dados  
-  No menu [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ferramentas **do Orientador de Otimização do** , clique em **SQL Server Profiler**.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>Para iniciar o SQL Server Profiler no SQL Server Management Studio  
 Você pode iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em vários locais do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é iniciado, ele carrega o contexto de conexão, o modelo de rastreamento e o contexto de filtro de seu ponto de inicialização. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia cada sessão do SQL Server Profiler em sua própria instância e o criador de perfil continuará a ser executado se você desligar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>Para iniciar o SQL Server Profiler no menu Ferramentas  
-  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Ferramentas** , clique em **SQL Server Profiler**.  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>Para iniciar o SQL Server Profiler no Editor de Consultas  
- No Editor de Consultas, clique com o botão direito do mouse e selecione **Rastrear Consulta no SQL Server Profiler**.  

  > [!NOTE]  
  >  O contexto de conexão é a conexão do editor, o modelo de rastreamento é TSQL_SPs e o filtro aplicado é SPID = SPID da janela de consulta.  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>Para iniciar o SQL Server Profiler no Monitor de Atividade  
- No Monitor de Atividade, clique no painel **Processos**, clique com o botão direito do mouse no processo cujo perfil você deseja criar e clique em **Rastrear Processo no SQL Server Profiler**.  

    > [!NOTE]  
    >  Quando um processo é selecionado, o contexto de conexão é a conexão do Pesquisador de Objetos quando o Monitor de Atividade foi aberto. O modelo de rastreamento é o padrão com base no tipo de servidor e o SPID é igual ao SPID do processo selecionado.  
    
## <a name="net-framework-security"></a>Segurança do .NET Framework  
- No modo de autenticação do Windows, a conta de usuário que executa o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] precisa ter permissão para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
- Para executar rastreamento com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], os usuários também devem ter a permissão ALTER TRACE.  

## <a name="next-steps"></a>Próximas etapas  
 [Visão geral do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Usar o SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
