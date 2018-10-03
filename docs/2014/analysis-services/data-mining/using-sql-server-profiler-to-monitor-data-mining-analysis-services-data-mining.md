---
title: Usando o SQL Server Profiler para monitorar a mineração de dados (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ccf4e335f3b6d700fd47e1073e4f9432cc81cd29
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139896"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Usando o SQL Server Profiler para monitorar a mineração de dados (Analysis Services - Mineração de dados)
  Se tiver as permissões necessárias, você poderá usar o SQL Server Profiler para monitorar as atividades de mineração de dados emitidas como solicitações enviadas a uma instância do SQL Server Analysis Services. A atividade de mineração de dados pode incluir o processamento de modelos ou estruturas, consultas de previsão ou consultas de conteúdo ou a criação de novos modelos ou estruturas.  
  
 SQL Server Profiler usa um `trace` para monitorar as solicitações enviadas de vários clientes, incluindo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], SQL Server Management Studio, serviços da Web ou os Data Mining Add-ins para o Excel, contanto que todas as atividades usam a mesma instância do SQL Server Analysis Services. Você deve criar um rastreamento separado para cada instância do SQL Server Analysis Services que deseja monitorar. Para obter informações gerais sobre rastreamentos e como usar o SQL Server Profiler, consulte [Usar o SQL Server Profiler para monitorar o Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para obter orientações específicas sobre os tipos de eventos capturados, consulte [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Usando rastreamentos para monitorar a mineração de dados  
 Ao capturar informações em um rastreamento, você pode especificar se as informações estão salvas em um arquivo ou em uma tabela em uma instância do SQL Server. Independentemente do método usado para armazenar os dados, você pode usar o SQL Server Profiler para exibir o rastreamento e aplicar filtros por eventos. A tabela a seguir lista alguns eventos e subclasses do rastreamento padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são de interesse para a mineração de dados.  
  
|EventClass|EventSubclass|Description|  
|----------------|-------------------|-----------------|  
|**Query Begin**<br /><br /> **Query End**|**0 - MDXQuery**|Contém o texto de todas as chamadas para os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Query Begin**<br /><br /> **Query End**|**1 - DMXQuery**|Contém o texto e os resultados das instruções DMX.|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|Fornece informações sobre o andamento do algoritmo de mineração de dados: por exemplo, se você estiver criando um modelo de clustering, a mensagem de andamento informará qual cluster candidato está sendo criado|  
|**Query Begin**<br /><br /> **Query End**|EXECUTESQL|Contém o texto da consulta Transact-SQL que está sendo executada|  
|**Query Begin**<br /><br /> **Query End**|**2- SQLQuery**|Contém o texto de todas as consultas dos conjuntos de linhas de esquema no formulário de tabelas do sistema.|  
|**Início de DISCOVER**<br /><br /> **Término de DISCOVER**|Vários|Contém o texto das chamadas de função DMX ou das instruções DISCOVER, encapsuladas em XMLA.|  
|**Erro**|(nenhum)|Contém o texto de erros enviados pelo servidor ao cliente.<br /><br /> Mensagens de erro que começam com **Erro (Mineração de Dados):** ou **Informativo (Mineração de Dados):** são geradas especificamente em resposta a solicitações DMX. Porém, não é suficiente exibir só estas mensagens de erro. Outros erros, como os gerados pelo analisador, podem estar relacionados à mineração de dados, mas não ter este prefixo.|  
  
 Exibindo as instruções de comando no log de rastreamento, você também pode ver a sintaxe de instruções complexas enviadas pelo cliente ao servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluindo as chamadas aos procedimentos armazenados do sistema. Essas informações podem ser úteis para depuração ou você pode usar instruções válidas como um modelo para criar novos modelos ou consultas de previsão. Para obter alguns exemplos de chamadas de procedimento armazenado que podem ser capturadas por um rastreamento, consulte [Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar uma instância do Analysis Services](../instances/monitor-an-analysis-services-instance.md)   
 [Usar eventos estendidos do SQL Server &#40;XEvents&#41; monitorar o Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
