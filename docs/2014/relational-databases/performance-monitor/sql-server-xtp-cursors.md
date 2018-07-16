---
title: Cursores XTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5eab11a0ee57a8545a2d19f8a7472392635e690
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206976"
---
# <a name="xtp-cursors"></a>Cursores de XTP
  O objeto de desempenho Cursores de XTP contém os contadores relacionados aos cursores do mecanismo de XTP interno. Os cursores são os blocos de construção de baixo nível que o mecanismo de XTP usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.  
  
 Esta tabela descreve os **cursores XTP** contadores.  
  
|Contador|Description|  
|-------------|-----------------|  
|**Exclusões de cursor/s**|O número de exclusões de cursor (em média), por segundo.|  
|**Inserções de Cursor/s**|O número de inserções de cursor (em média), por segundo.|  
|**Verificações de cursor iniciadas/s**|O número de verificações de cursor iniciadas (em média), por segundo.|  
|**Violações exclusivas de cursor/s**|O número de violações de restrição exclusiva (em média), por segundo.|  
|**Atualizações de cursor/s**|O número de atualizações de cursor (em média), por segundo.|  
|**Conflitos de gravação de cursor/s**|O número de conflitos de gravação/gravação para a mesma versão de linha (em média), por segundo.|  
|**Tentativas de verificação de canto sujo/s (emitido pelo usuário)**|O número de novas tentativas de verificação devido a conflitos de gravação durante as varreduras de canto sujo emitidas pela verificação de tabela inteira de um usuário (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Linhas expiradas removidas/s**|O número de linhas expiradas removidas por cursores (em média), por segundo.|  
|**Linhas expiradas tocadas/s**|O número de linhas expiradas tocadas por cursores (em média), por segundo.|  
|**Linhas retornadas/s**|O número de linhas retornadas por cursores (em média), por segundo.|  
|**Linhas tocadas/s**|O número de linhas tocadas por cursores (em média), por segundo.|  
|**Linhas excluídas por tentativa tocadas/s**|O número de linhas expirando tocadas por cursores (em média), por segundo. Uma linha está expirando quando a transação que a excluiu ainda está ativa (ou seja, ainda não foi confirmada nem anulada).|  
  
## <a name="see-also"></a>Consulte também  
 [XTP &#40;OLTP in-memory&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
