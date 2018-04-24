---
title: Corrigir a sobreposição de máscara de afinidade e máscara de afinidade de entrada e saída | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa7d301ff0c19a4c087a5a46928863ae1ad46913
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>Corrigir a sobreposição de máscara de afinidade e máscara de afinidade de entrada e saída
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possui um ou mais processadores atribuídos para serem usados com as opções de máscara de afinidade e máscara de E/S de afinidade. Em um computador com mais de um processador, as opções de máscara de afinidade e máscara de E/S de afinidade são empregadas para designar quais CPUs o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]utiliza. Ao habilitar uma CPU com a máscara de afinidade e a máscara de E/S de afinidade você poderá reduzir o desempenho forçando o uso excessivo do processador.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Ao especificar a opção de máscara de afinidade ou de máscara de E/S de afinidade, você deve especificar as duas, mas cada CPU só pode ser habilitada uma vez.  
  
 Não habilite a mesma CPU na opção de máscara de afinidade e na opção de máscara de E/S de afinidade. Os bits que correspondem a cada CPU devem estar em um dos seguintes estados:  
  
-   0 na opção de máscara de afinidade e na opção de máscara de afinidade de E/S  
  
-   0 na opção de máscara de afinidade e 1 na opção de máscara de E/S de afinidade  
  
-   1 na opção de máscara de afinidade e 0 na opção de máscara de E/S de afinidade  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [Opção de configuração do servidor de máscara de Entrada-Saída de afinidade](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [Opção affinity64 mask de configuração de servidor](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [Opção de configuração do servidor affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
