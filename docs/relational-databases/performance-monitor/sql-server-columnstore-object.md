---
title: SQL Server, objeto Columnstore | Microsoft Docs
description: Saiba mais sobre o objeto SQLServer:Columnstore, que fornece contadores para monitorar a execução do índice columnstore no SQL Server.
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 61f950b5322270ce1b72b1734b92474dfb18b2bb
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505781"
---
# <a name="sql-server-columnstore-object"></a>SQL Server, Objeto Columnstore
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O objeto **SQLServer:Columnstore** fornece contadores para monitorar a execução de índice columnstore no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tabela a seguir descreve os contadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore**.  
  
|Contadores de columnstore|Descrição|  
|--------------------------|-----------------|  
|**Rowgroups delta fechados**|Número de rowgroups delta fechados.|  
|**Rowgroups delta compactados**|Número de rowgroups delta compactados.|  
|**Rowgroups delta criados**|Número de rowgroups delta criados.|  
|**Raio de ocorrências do cache do segmento**|Percentual de segmentos da coluna que foram encontrados no pool columnstore sem precisar incorrer em uma leitura do disco.|  
|**Base da taxa de ocorrência do cache do segmento**|Apenas para uso interno.|
|**Leituras de segmento/s**|Número de leituras do segmento físico emitidas.|  
|**Total de buffers de exclusão migrados**|Número de vezes que o motor de tupla limpou o buffer de exclusão.|  
|**Total de avaliações de política de mesclagem**|Número de vezes que a política de mesclagem de columnstore foi avaliada.|  
|**Total de rowgroups compactados**|Número total de rowgroups compactados.|  
|**Total de Rowgroups Ajustados Para Mesclar**|Número de rowgroups de origem ajustados para MERGE após a inicialização do SQL Server.|  
|**Total de mesclagens de rowgroups compactadas**|Número de rowgroups de destino compactados criados com MERGE desde a inicialização do SQL Server.|  
|**Total de rowgroups de origem mesclados**|Número de rowgroups de origem mesclados desde a inicialização do SQL Server.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
