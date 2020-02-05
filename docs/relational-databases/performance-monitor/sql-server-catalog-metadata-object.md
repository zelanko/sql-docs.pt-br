---
title: SQL Server, objeto Metadados de Catálogo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3b408951b0a1f32bda0920260aae18ab93350fdd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67986720"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, objeto Metadados de Catálogo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O objeto de desempenho **SQL Server:Metadados de Catálogo** fornece contadores para metadados de catálogo do SQL Server.

A tabela a seguir descreve os objetos de desempenho **Metadados de Catálogo** do SQL Server.


|**Contadores Metadados de Catálogo do SQL Server**|DESCRIÇÃO|  
|-------------|-----------------|  
|**Contagem de Entradas do Cache**|Número de entradas no cache de metadados de catálogo.|
|**Contagem de Entradas de Cache Fixadas**|Número de entradas no cache de metadados de catálogo que estão fixadas.|
|**Taxa de Acertos do Cache**|Taxa entre pesquisas e ocorrências no cache de metadados de catálogo.|
|**Base do Índice de Ocorrência no Cache**|Apenas para uso interno.|

Há uma instância do contador para cada banco de dados.

## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
