---
title: SQL Server, objeto Columnstore | Microsoft Docs
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb0f5a1872802fc5f623650902ab7a92fe72c6e0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-columnstore-object"></a>SQL Server, Objeto Columnstore
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto **SQLServer:Columnstore** fornece contadores para monitorar a execução de índice columnstore no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tabela a seguir descreve as colunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** counters.  
  
|Contadores de columnstore|Descrição|  
|--------------------------|-----------------|  
|**Rowgroups delta fechados**|Número de rowgroups delta fechados.|  
|**Rowgroups delta compactados**|Número de rowgroups delta compactados.|  
|**Rowgroups delta criados**|Número de rowgroups delta criados.|  
|**Raio de ocorrências do cache do segmento**|Percentual de segmentos da coluna que foram encontrados no pool columnstore sem precisar incorrer em uma leitura do disco.|  
|**Base da taxa de ocorrência do cache do segmento**|Somente para uso interno.|
|**Leituras de segmento/s**|Número de leituras do segmento físico emitidas.|  
|**Total de buffers de exclusão migrados**|Número de vezes que o motor de tupla limpou o buffer de exclusão.|  
|**Total de avaliações de política de mesclagem**|Número de vezes que a política de mesclagem de columnstore foi avaliada.|  
|**Total de rowgroups compactados**|Número total de rowgroups compactados.|  
|**Total de Rowgroups Ajustados Para Mesclar**|Número de rowgroups de origem ajustados para MERGE após a inicialização do SQL Server.|  
|**Total de mesclagens de rowgroups compactadas**|Número de rowgroups de destino compactados criados com MERGE desde a inicialização do SQL Server.|  
|**Total de rowgroups de origem mesclados**|Número de rowgroups de origem mesclados desde a inicialização do SQL Server.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
