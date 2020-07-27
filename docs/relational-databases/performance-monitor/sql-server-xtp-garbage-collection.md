---
title: Coleta de lixo de SQL Server XTP | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho XTP Garbage Collection do SQL Server, que contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8575295948b5560f25dc0e967fa419699587af7b
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457958"
---
# <a name="sql-server-xtp-garbage-collection"></a>Coleta de Lixo de XTP do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O objeto de desempenho Coleta de Lixo de XTP do SQL Server contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.  
  
 Esta tabela descreve os contadores de **Coleta de Lixo de XTP do SQL Server** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Tentativas de verificação de canto sujo/s (emitido pelo GC)**|O número de tentativas de digitalização devido a conflitos de gravação durante as varreduras de canto sujo emitidas pelo coletor de lixo (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Itens principais do trabalho do GC/s**|O número de itens de trabalho processados pelo thread principal do GC.|  
|**Item de trabalho do GC em paralelo/s**|O número de vezes que um thread paralelo executou um item de trabalho do GC.|  
|**Linhas processadas/s**|O número de linhas processadas pelo coletor de lixo (em média), por segundo|  
|**Linhas processadas/s (primeiro no bucket e removidas)**|O número de linhas processadas pelo coletor de lixo que estavam primeiro no bucket de hash correspondente e podiam ser removidas imediatamente (em média), por segundo.|  
|**Linhas processadas/s (primeiro no bucket)**|O número de linhas processadas pelo coletor de lixo que estavam primeiro no bucket de hash correspondente (em média), por segundo.|  
|**Linhas processadas/s (marcadas para desvinculação)**|O número de linhas processadas pelo coletor de lixo que já estavam marcadas para desvinculação (em média), por segundo.|  
|**Linhas processadas/s (sem varredura necessária)**|O número de linhas processadas pelo coletor de lixo que não exigirão uma varredura de canto sujo (em média), por segundo.|  
|**Linhas expiradas varridas removidas/s**|O número de linhas expiradas removidas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas expiradas varridas tocadas/s**|O número de linhas expiradas tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas expirando varridas tocadas/s**|O número de linhas expirando tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas varridas tocadas/s**|O número de linhas tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Verificações de varredura iniciadas/s**|O número de verificações de varredura de canto sujo iniciadas (em média), por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
