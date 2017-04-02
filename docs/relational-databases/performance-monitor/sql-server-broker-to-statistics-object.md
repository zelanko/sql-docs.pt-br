---
title: "SQL Server, objeto Broker TO Statistics | Microsoft Docs"
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
  - "Objeto de Transmissão do Service Broker"
  - "SQL Server: Objeto de Transmissão do Service Broker"
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server, objeto Broker TO Statistics
  O objeto de desempenho SQLServer:Broker TO Statistics informa quantas vezes os diálogos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] requerem objetos de transmissão, e com que frequência os objetos de transmissão são gravados no **tempdb**.  
  
 Objetos de transmissão registram o estado de transmissões de mensagem para um diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Eles são armazenados na memória. Para liberar a memória, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] grava lotes de objetos de transmissão inativos periodicamente em tabelas de trabalho no **tempdb**.  
  
 A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server Broker TO Statistics|Descrição|  
|----------------------------------------------|-----------------|  
|**Média Médio de Gravações em Lotes**|O número médio de objetos de transmissão salvo em um lote.|  
|**Média Médio de Gravação de Lote (ms)**|O número médio de milissegundos exigido para salvar um lote de objetos de transmissão.|  
|**Média Tempo de Gravação de Lote Base**|Somente para uso interno.|
|**Média Médio entre os Lotes (ms)**|O número médio de milissegundos entre gravações de lotes de objetos de transmissão.|  
|**Média Tempo entre os lotes base**|Somente para uso interno.| 
|**Obtenções de Objeto de Transmissão/s**|O número de vezes por segundo que os diálogos solicitaram objetos de transmissão.|  
|**Objetos de Transmissão Marcados como Sujos/s**|O número de vezes por segundo que objetos de transmissão foram marcados como sujos. Os objetos de transmissão são marcados como sujos pela primeira modificação que faz com que a cópia na memória se diferencie da cópia armazenada no **tempdb**. Objetos de transmissão são modificados quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] precisa registrar uma alteração no estado das transmissões das mensagens para o diálogo.|  
|**Gravações de Objetos de Transmissão/s**|O número de vezes por segundo que um lote de objetos de transmissão foi gravado nas tabelas de trabalho do **tempdb**. Gravações em grande número podem indicar que a memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo pressionada.|  
  
## Consulte também  
 [SQL Server, Objeto Métodos de Acesso](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [SQL Server, objeto Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  