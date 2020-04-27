---
title: Usando SQL Server Profiler para monitorar a mineração de dados (mineração de dados Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3aa29cede2849158162aba27332d5fe7f8f5fae5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082698"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Usando o SQL Server Profiler para monitorar a mineração de dados (Analysis Services - Mineração de dados)
  Se tiver as permissões necessárias, você poderá usar o SQL Server Profiler para monitorar as atividades de mineração de dados emitidas como solicitações enviadas a uma instância do SQL Server Analysis Services. A atividade de mineração de dados pode incluir o processamento de modelos ou estruturas, consultas de previsão ou consultas de conteúdo ou a criação de novos modelos ou estruturas.  
  
 O SQL Server Profiler usa um `trace` para monitorar as solicitações enviadas de vários clientes, incluindo o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o SQL Server Management Studio, serviços da Web ou Suplementos de Mineração de Dados para o Excel, contanto que todas as atividades usem a mesma instância do SQL Server Analysis Services. Você deve criar um rastreamento separado para cada instância do SQL Server Analysis Services que deseja monitorar. Para obter informações gerais sobre rastreamentos e como usar o SQL Server Profiler, consulte [Usar o SQL Server Profiler para monitorar o Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para obter orientações específicas sobre os tipos de eventos capturados, consulte [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Usando rastreamentos para monitorar a mineração de dados  
 Ao capturar informações em um rastreamento, você pode especificar se as informações estão salvas em um arquivo ou em uma tabela em uma instância do SQL Server. Independentemente do método usado para armazenar os dados, você pode usar o SQL Server Profiler para exibir o rastreamento e aplicar filtros por eventos. A tabela a seguir lista alguns eventos e subclasses do rastreamento padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são de interesse para a mineração de dados.  
  
|EventClass|EventSubclass|Descrição|  
|----------------|-------------------|-----------------|  
|**Início da consulta**<br /><br /> **Fim da consulta**|**0 - MDXQuery**|Contém o texto de todas as chamadas para os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Início da consulta**<br /><br /> **Fim da consulta**|**1 - DMXQuery**|Contém o texto e os resultados das instruções DMX.|  
|**Início do relatório de andamento**<br /><br /> **Fim de relatório de andamento**|**34 - DataMiningProgress**|Fornece informações sobre o andamento do algoritmo de mineração de dados: por exemplo, se você estiver criando um modelo de clustering, a mensagem de andamento informará qual cluster candidato está sendo criado|  
|**Início da consulta**<br /><br /> **Fim da consulta**|EXECUTESQL|Contém o texto da consulta Transact-SQL que está sendo executada|  
|**Início da consulta**<br /><br /> **Fim da consulta**|**2-SQLQuery**|Contém o texto de todas as consultas dos conjuntos de linhas de esquema no formulário de tabelas do sistema.|  
|**Início da descoberta**<br /><br /> **Término de DISCOVER**|Vários|Contém o texto das chamadas de função DMX ou das instruções DISCOVER, encapsuladas em XMLA.|  
|**Erro**|(nenhum)|Contém o texto de erros enviados pelo servidor ao cliente.<br /><br /> Mensagens de erro que começam com **Erro (Mineração de Dados):** ou **Informativo (Mineração de Dados):** são geradas especificamente em resposta a solicitações DMX. Porém, não é suficiente exibir só estas mensagens de erro. Outros erros, como os gerados pelo analisador, podem estar relacionados à mineração de dados, mas não ter este prefixo.|  
  
 Exibindo as instruções de comando no log de rastreamento, você também pode ver a sintaxe de instruções complexas enviadas pelo cliente ao servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluindo as chamadas aos procedimentos armazenados do sistema. Essas informações podem ser úteis para depuração ou você pode usar instruções válidas como um modelo para criar novos modelos ou consultas de previsão. Para obter alguns exemplos de chamadas de procedimento armazenado que podem ser capturadas por um rastreamento, consulte [Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar uma instância de Analysis Services](../instances/monitor-an-analysis-services-instance.md)   
 [Usar SQL Server eventos estendidos &#40;&#41; de XEvents para monitorar Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
