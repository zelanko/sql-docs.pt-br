---
title: "SQL Server, objeto Estatísticas TO do Agente | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00f291cbcd22622a010cde162cbcd27b866ae4d8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server, objeto Broker TO Statistics
  O objeto de desempenho SQLServer:Broker TO Statistics informa quantas vezes os diálogos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] requerem objetos de transmissão, e com que frequência os objetos de transmissão são gravados no **tempdb**.  
  
 Objetos de transmissão registram o estado de transmissões de mensagem para um diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Eles são armazenados na memória. Para liberar a memória, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] grava lotes de objetos de transmissão inativos periodicamente em tabelas de trabalho no **tempdb**.  
  
 A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contadores do SQL Server Broker TO Statistics|Description|  
|----------------------------------------------|-----------------|  
|**Méd. de gravações em lotes**|O número médio de objetos de transmissão salvo em um lote.|  
|**Méd. de tempo de gravação em lote (ms)**|O número médio de milissegundos exigido para salvar um lote de objetos de transmissão.|  
|**Méd. de tempo de base de gravação em lote**|Somente para uso interno.|
|**Méd. de tempo entre lotes (ms)**|O número médio de milissegundos entre gravações de lotes de objetos de transmissão.|  
|**Méd. de tempo entre as base de lotes**|Somente para uso interno.| 
|**Obtenções de Objeto de Transmissão/s**|O número de vezes por segundo que os diálogos solicitaram objetos de transmissão.|  
|**Objetos de Transmissão Marcados como Sujos/s**|O número de vezes por segundo que objetos de transmissão foram marcados como sujos. Os objetos de transmissão são marcados como sujos pela primeira modificação que faz com que a cópia na memória se diferencie da cópia armazenada no **tempdb**. Objetos de transmissão são modificados quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] precisa registrar uma alteração no estado das transmissões das mensagens para o diálogo.|  
|**Gravações de Objetos de Transmissão/s**|O número de vezes por segundo que um lote de objetos de transmissão foi gravado nas tabelas de trabalho do **tempdb** . Gravações em grande número podem indicar que a memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo pressionada.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server, Objeto Métodos de Acesso](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [SQL Server, objeto Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
