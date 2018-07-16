---
title: Processador fantasma de XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1218f92622f9294c15afe417bcebbe84ad0df5da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37175873"
---
# <a name="xtp-phantom-processor"></a>Processador Fantasma de XTP
  O objeto de desempenho Processador Fantasma de XTP contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo de XTP. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE.  
  
 Esta tabela descreve os contadores do **Processador Fantasma de XTP** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Tentativas de verificação de canto sujo/s (emitido pelo fantasma)**|O número de tentativas de digitalização devido a conflitos de gravação durante as varreduras de canto sujo emitidas pelo processador fantasma (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Linhas fantasma expiradas removidas/s**|O número de linhas expiradas removidas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma expiradas tocadas/s**|O número de linhas expiradas tocadas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma expirando tocadas/s**|O número de linhas expirando tocadas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma tocadas/s**|O número de linhas tocadas por verificações fantasma (em média), por segundo.|  
|**Verificações fantasma iniciadas/s**|O número de verificações fantasma iniciadas (em média), por segundo.|  
  
## <a name="see-also"></a>Consulte também  
 [XTP &#40;OLTP in-memory&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
