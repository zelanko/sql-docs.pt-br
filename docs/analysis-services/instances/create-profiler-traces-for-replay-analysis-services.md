---
title: "Criar rastreamentos do Profiler para reprodu&#231;&#227;o (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Profiler, Analysis Services"
  - "monitorando o Analysis Services [SQL Server]"
  - "repetindo consultas"
  - "repetindo identificações"
  - "eventos [Analysis Services]"
  - "repetindo comandos"
  - "Profiler [SQL Server Profiler], Analysis Services"
  - "desempenho [Analysis Services], repetições"
  - "rastreamentos [Analysis Services]"
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 33
---
# Criar rastreamentos do Profiler para reprodu&#231;&#227;o (Analysis Services)
  Para repetir consultas, identificações e comandos enviados pelos usuários ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve reunir os eventos necessários. Para iniciar a coleta desses eventos, as classes de evento adequadas devem ser selecionadas na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento**. Por exemplo, se a classe de evento Query Begin for selecionada, os eventos que contêm consultas serão coletados e usados para repetição. Além disso, o arquivo de rastreamento contém informações suficientes para oferecer suporte à repetição das transações de servidor em um ambiente distribuído na sequência original das transações.  
  
## Repetição de consultas  
 Para repetir consultas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A identificação do processo do servidor (SPID) fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   Classe de evento Query Begin com todas as suas colunas de dados. Essa classe de evento fornece informações sobre a consulta que foi enviada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A coluna Event Subclass fornece informações sobre o tipo de consulta. A coluna TextData fornece o texto real da consulta. A coluna RequestParameters fornece os parâmetros para consultas parametrizadas, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA (XML para análise). Para obter mais informações, consulte [Colunas de dados de eventos de consultas](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
-   Classe de evento Query End com todas as suas colunas de dados. Essa classe de evento verifica o status da execução de consulta. Para obter mais informações, consulte [Colunas de dados de eventos de consultas](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
## Repetição de identificações  
 Para repetir descobertas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A SPID fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   Classe de evento Discover Begin com todas as suas colunas de dados. A coluna TextData fornece a parte \<RequestType> da solicitação de identificação e a coluna RequestProperties fornece a parte \<Properties> da solicitação de identificação. A coluna EventSubclass fornece o tipo de descoberta. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
-   Descobrir a classe de evento de Término com todas as suas colunas de dados. Essa classe de evento verifica o status da solicitação de identificação. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
## Repetição de comandos  
 Para repetir comandos, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Command Begin com todas as suas colunas de dados. A coluna TextData fornece os detalhes do comando, como o tipo de processo, a ID do banco de dados e a ID do cubo. A coluna RequestParameters fornece os parâmetros para comando parametrizado, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA. Para obter mais informações, consulte [Colunas de dados de eventos de comando](../../analysis-services/trace-events/command-events-data-columns.md).  
  
-   Classe de evento Command End com todas as suas colunas de dados. Essa classe de evento verifica o status do comando. Para obter mais informações, consulte [Colunas de dados de eventos de comando](../../analysis-services/trace-events/command-events-data-columns.md).  
  
## Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  