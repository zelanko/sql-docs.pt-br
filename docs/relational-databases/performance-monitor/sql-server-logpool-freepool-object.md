---
title: SQL Server, objeto LogPool FreePool | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:LogPool FreePool
ms.assetid: 8ffd569b-045f-4c3f-a473-4a491d6a1d80
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 2843933d1a8a04ecf0cb2cbaf7a969c5decd5af1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677517"
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

