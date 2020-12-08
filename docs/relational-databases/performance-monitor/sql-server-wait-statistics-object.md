---
title: SQL Server, objeto Estatística de espera | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho SQLServer:Wait Statistics, que contém contadores de desempenho que relatam informações sobre o status de espera.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: df97bc68487d6113857fa0d9c6a56bdc7a2871b9
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505545"
---
# <a name="sql-server-wait-statistics-object"></a>SQL Server, Objeto Wait Statistics
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto de desempenho **SQLServer:Wait Statistics** contém contadores de desempenho que relatam informações sobre o status de espera.  
  
 A tabela a seguir lista os contadores contidos no objeto Wait Statistics (Estatísticas de Espera).  
  
|Contadores de Estatísticas de Espera do SQL Server|Descrição|  
|-----------------------------------------|-----------------|  
|**Esperas de bloqueio**|Estatísticas dos processos que esperam por um bloqueio.|  
|**Esperas de buffer de log**|Estatísticas dos processos que esperam pela disponibilização de buffer de log.|  
|**Esperas de gravação de log**|Estatísticas dos processos que esperam por buffer de log para serem gravados.|  
|**Tempo de espera em fila para concessão de memória**|Estatísticas dos processos que esperam por concessão de memória para ficarem disponíveis.|  
|**Esperas de E/S de rede**|Estatísticas pertinentes às esperas de E/S de rede.|  
|**Esperas de travas sem-página**|Estatísticas pertinentes a travas sem-página.|  
|**Esperas de travas de E/S de página**|Estatísticas pertinentes a travas de E/S de página.|  
|**Esperas de trava de página**|Estatísticas pertinentes a travas de página, excluindo-se travas de E/S.|  
|**Espera de objetos de memória isenta de threads**|Estatísticas dos processos que esperam alocadores de memória isenta de threads.|  
|**Esperas de propriedade de transação**|Estatísticas pertinentes a processos de sincronização de acesso à transação.|  
|**Espera pelo trabalhador**|Estatísticas pertinentes a processos que esperam pela disponibilização do trabalhador.|  
|**Esperas da sincronização do workspace**|Estatísticas pertinentes a processos de sincronização de acesso ao workspace.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Descrição|  
|----------|-----------------|  
|**Tempo de espera médio (ms)**|Tempo médio do tipo de espera selecionado.|  
|**Tempo de espera cumulativo (ms) por segundo**|Tempo de espera agregado, por segundo, do tipo de espera selecionado.|  
|**Esperas em andamento**|Número de processos que esperam atualmente pelo tipo seguinte.|  
|**Esperas iniciadas por segundo**|Número de esperas iniciadas, por segundo, do tipo de espera selecionado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
