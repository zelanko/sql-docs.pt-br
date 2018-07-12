---
title: Armazenamento XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b2f18eb1db7ef854b4d982d18374b174ecf65641
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156437"
---
# <a name="xtp-storage"></a>Armazenamento de XTP
  O objeto de desempenho do Armazenamento de XTP contém os contadores relacionados ao Armazenamento de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores de **Armazenamento de XTP** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Pontos de verificação fechados**|Contagem de pontos de verificação fechados feita pelo agente online.|  
|**Pontos de verificação concluídos**|Contagem de pontos de verificação processados pelo thread de ponto de verificação offline.|  
|**Mesclagens de núcleo concluídas**|O número de mesclagens de núcleo concluídas pelo thread de trabalho de mesclagem. Essas mesclagens ainda precisam ser instaladas.|  
|**Avaliações de política de mesclagem**|O número de avaliações de política de mesclagem desde que o servidor foi iniciado.|  
|**Solicitações de mesclagem pendentes**|O número de solicitações de mesclagem pendentes desde que o servidor foi iniciado.|  
|**Mesclagens abandonadas**|O número de mesclagens abandonadas devido à falha.|  
|**Mesclagens instaladas**|O número de mesclagens instaladas com êxito.|  
|**Total de arquivos mesclados**|O número total de arquivos de origem mesclados. Esta contagem pode ser usada para localizar o número médio de arquivos de origem na mesclagem.|  
  
## <a name="see-also"></a>Consulte também  
 [XTP &#40;OLTP in-memory&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
