---
title: "SQL Server, objeto Metadados de Catálogo | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
caps.latest.revision: "4"
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d1f9ca9e984a06fb35921123c34a49ff2221491
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, objeto Metadados de Catálogo
O objeto de desempenho **SQL Server:Metadados de Catálogo** fornece contadores para metadados de catálogo do SQL Server.

A tabela a seguir descreve os objetos de desempenho **Metadados de Catálogo** do SQL Server.


|**Contadores Metadados de Catálogo do SQL Server**|Description|  
|-------------|-----------------|  
|**Contagem de Entradas do Cache**|Número de entradas no cache de metadados de catálogo.|
|**Contagem de Entradas de Cache Fixadas**|Número de entradas no cache de metadados de catálogo que estão fixadas.|
|**Taxa de Acertos do Cache**|Taxa entre pesquisas e ocorrências no cache de metadados de catálogo.|
|**Base do Índice de Ocorrência no Cache**|Somente para uso interno.|

Há uma instância do contador para cada banco de dados.

## <a name="see-also"></a>Consulte também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
