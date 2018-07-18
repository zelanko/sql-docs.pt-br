---
title: Criar rastreamentos do Profiler para reprodução (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d5928325ffe5b0b98da2058529b1cbb036a445be
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031634"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>Criar rastreamentos do Profiler para reprodução (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Para repetir consultas, identificações e comandos enviados pelos usuários ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve reunir os eventos necessários. Para iniciar a coleta desses eventos, as classes de evento adequadas devem ser selecionadas na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** . Por exemplo, se a classe de evento Query Begin for selecionada, os eventos que contêm consultas serão coletados e usados para repetição. Além disso, o arquivo de rastreamento contém informações suficientes para oferecer suporte à repetição das transações de servidor em um ambiente distribuído na sequência original das transações.  
  
## <a name="replay-for-queries"></a>Repetição de consultas  
 Para repetir consultas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A identificação do processo do servidor (SPID) fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   Classe de evento Query Begin com todas as suas colunas de dados. Essa classe de evento fornece informações sobre a consulta que foi enviada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A coluna Event Subclass fornece informações sobre o tipo de consulta. A coluna TextData fornece o texto real da consulta. A coluna RequestParameters fornece os parâmetros para consultas parametrizadas, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA (XML para análise). Para obter mais informações, consulte [Colunas de dados de eventos de consultas](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
-   Classe de evento Query End com todas as suas colunas de dados. Essa classe de evento verifica o status da execução de consulta. Para obter mais informações, consulte [Colunas de dados de eventos de consultas](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
## <a name="replay-for-discovers"></a>Repetição de identificações  
 Para repetir descobertas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A SPID fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   Classe de evento Discover Begin com todas as suas colunas de dados. A coluna TextData fornece o \<RequestType > parte da solicitação de descoberta e a coluna RequestProperties fornece a \<Propriedades > parte da solicitação discover. A coluna EventSubclass fornece o tipo de descoberta. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
-   Descobrir a classe de evento de Término com todas as suas colunas de dados. Essa classe de evento verifica o status da solicitação de identificação. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
## <a name="replay-for-commands"></a>Repetição de comandos  
 Para repetir comandos, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Command Begin com todas as suas colunas de dados. A coluna TextData fornece os detalhes do comando, como o tipo de processo, a ID do banco de dados e a ID do cubo. A coluna RequestParameters fornece os parâmetros para comando parametrizado, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA. Para obter mais informações, consulte [Colunas de dados de eventos de comando](../../analysis-services/trace-events/command-events-data-columns.md).  
  
-   Classe de evento Command End com todas as suas colunas de dados. Essa classe de evento verifica o status do comando. Para obter mais informações, consulte [Colunas de dados de eventos de comando](../../analysis-services/trace-events/command-events-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
