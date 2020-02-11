---
title: Armazenamento XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 50e62a9232690deb368096723f428118e9de7aa2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151149"
---
# <a name="xtp-storage"></a>Armazenamento de XTP
  O objeto de desempenho do Armazenamento de XTP contém os contadores relacionados ao Armazenamento de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores de **Armazenamento de XTP** .  
  
|Contador|DESCRIÇÃO|  
|-------------|-----------------|  
|**Pontos de verificação fechados**|Contagem de pontos de verificação fechados feita pelo agente online.|  
|**Pontos de verificação concluídos**|Contagem de pontos de verificação processados pelo thread de ponto de verificação offline.|  
|**Mesclagens de núcleo concluídas**|O número de mesclagens de núcleo concluídas pelo thread de trabalho de mesclagem. Essas mesclagens ainda precisam ser instaladas.|  
|**Avaliações de política de mesclagem**|O número de avaliações de política de mesclagem desde que o servidor foi iniciado.|  
|**Solicitações de mesclagem pendentes**|O número de solicitações de mesclagem pendentes desde que o servidor foi iniciado.|  
|**Mesclagens abandonadas**|O número de mesclagens abandonadas devido à falha.|  
|**Mesclagens instaladas**|O número de mesclagens instaladas com êxito.|  
|**Total de arquivos mesclados**|O número total de arquivos de origem mesclados. Esta contagem pode ser usada para localizar o número médio de arquivos de origem na mesclagem.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de OLTP na memória&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
