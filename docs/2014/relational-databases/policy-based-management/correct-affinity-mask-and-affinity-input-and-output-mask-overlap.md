---
title: Corrigir máscara de afinidade e entrada de saída de afinidade sobreposição de máscara | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3139c864805c7df9220afc9b81d2a242775f4fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856706"
---
# <a name="correct-affinity-mask-and-affinity-input-output-mask-overlap"></a>Corrigir máscara de afinidade e a sobreposição de máscara de entrada e saída de afinidade
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
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
