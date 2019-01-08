---
title: SQL Server, objeto LogPool FreePool | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:LogPool FreePool
ms.assetid: 8ffd569b-045f-4c3f-a473-4a491d6a1d80
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 9039285fa2911d87e19d4a22ec952eaf78811a0b
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380347"
---
# <a name="sql-server-logpool-freepool-object"></a>SQL Server, objeto LogPool FreePool
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O objeto de desempenho **SQLServer:LogPool FreePool** fornece contadores de estatísticas para o pool livre dentro do Pool de Logs.

A tabela a seguir descreve os objetos de desempenho **LogPool FreePool** do SQL Server.

|**Contadores de LogPool FreePool do SQL Server**|Descrição|  
|-------------|-----------------|  
|**Reabastecimentos do Buffer Gratuito/seg**|Número de buffers alocados para reabastecimento por segundo.|
|**Comprimento de lista livre**|Comprimento da lista livre.|

Há uma instância do contador para cada categoria do pool de logs.

## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)

