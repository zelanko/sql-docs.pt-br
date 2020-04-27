---
title: Coleta de lixo XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5796cc1184e862b4e8afe42b4fa5f5babe8358dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63151029"
---
# <a name="xtp-garbage-collection"></a>Coleta de Lixo de XTP
  O objeto de desempenho Coleta de Lixo de XTP contém os contadores relacionados ao coletor de lixo do mecanismo de XTP.  
  
 Esta tabela descreve os contadores de **Coleta de Lixo de XTP** .  
  
|Contador|DESCRIÇÃO|  
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
 [&#40;de OLTP na memória&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
