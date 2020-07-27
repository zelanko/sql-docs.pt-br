---
title: Armazenamento XTP do SQL Server | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho XTP Storage do SQL Server, que contém contadores relacionados ao armazenamento em disco para OLTP in-memory no SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a623d68d5d738d773ab479bd0ca24c7454399f58
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457908"
---
# <a name="sql-server-xtp-storage"></a>Armazenamento XTP do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O objeto de desempenho do Armazenamento XTP do SQL Server contém contadores relacionados ao armazenamento em disco para OLTP in-memory do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores do **Armazenamento XTP do SQL Server** .  
  
|Contador|Descrição|  
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
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
