---
title: Corrigir máscara de afinidade e entrada de saída de afinidade sobreposição de máscara | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1f58246e4bef80c4cca26e40ba83fcacec753ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123017"
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
  
  
