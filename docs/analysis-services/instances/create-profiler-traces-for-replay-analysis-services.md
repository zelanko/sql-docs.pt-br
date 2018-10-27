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
ms.openlocfilehash: 36ae9263a6ce5f92e144b34c232dd1c096a6609d
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147331"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>Criar rastreamentos do Profiler para reprodução (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Para repetir consultas, identificações e comandos enviados pelos usuários ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve reunir os eventos necessários. Para iniciar a coleta desses eventos, as classes de evento adequadas devem ser selecionadas na guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** . Por exemplo, se a classe de evento Query Begin for selecionada, os eventos que contêm consultas serão coletados e usados para repetição. Além disso, o arquivo de rastreamento contém informações suficientes para oferecer suporte à repetição das transações de servidor em um ambiente distribuído na sequência original das transações.  
  
## <a name="replay-for-queries"></a>Repetição de consultas  
 Para repetir consultas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A identificação do processo do servidor (SPID) fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   Classe de evento Query Begin com todas as suas colunas de dados. Essa classe de evento fornece informações sobre a consulta que foi enviada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A coluna Event Subclass fornece informações sobre o tipo de consulta. A coluna TextData fornece o texto real da consulta. A coluna RequestParameters fornece os parâmetros para consultas parametrizadas, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA (XML para análise). Para obter mais informações, consulte [Colunas de dados de eventos de consultas](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
-   Classe de evento Query End com todas as suas colunas de dados. Essa classe de evento verifica o status da execução de consulta. Para obter mais informações, consulte [Colunas de dados de eventos de consultas](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
## <a name="replay-for-discovers"></a>Repetição de identificações  
 Para repetir descobertas, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Audit Login com todas as suas colunas de dados. Essa classe de evento fornece informações sobre qual usuário está conectado e sobre as configurações de sessão. A SPID fornece a referência para a sessão de usuário. Para obter mais informações, consulte [Colunas de dados de auditoria de segurança](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   Classe de evento Discover Begin com todas as suas colunas de dados. A coluna TextData fornece o \<RequestType > parte da solicitação de descoberta e a coluna RequestProperties fornece a \<Propriedades > parte da solicitação discover. A coluna EventSubclass fornece o tipo de descoberta. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
-   Descobrir a classe de evento de Término com todas as suas colunas de dados. Essa classe de evento verifica o status da solicitação de identificação. Para obter mais informações, consulte [Colunas de dados de eventos de descoberta](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
## <a name="replay-for-commands"></a>Repetição de comandos  
 Para repetir comandos, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve capturar os seguintes eventos:  
  
-   Classe de evento Command Begin com todas as suas colunas de dados. A coluna TextData fornece os detalhes do comando, como o tipo de processo, a ID do banco de dados e a ID do cubo. A coluna RequestParameters fornece os parâmetros para comando parametrizado, e a coluna RequestProperties fornece as propriedades de uma solicitação XMLA. Para obter mais informações, consulte [Colunas de dados de eventos de comando](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
-   Classe de evento Command End com todas as suas colunas de dados. Essa classe de evento verifica o status do comando. Para obter mais informações, consulte [Colunas de dados de eventos de comando](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
