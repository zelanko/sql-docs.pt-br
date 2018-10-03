---
title: Solução de problemas de gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 043246a90567bbd0cc2d084e1b2844ef2b79c346
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162056"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solução de problemas de gráficos (Construtor de Relatórios e SSRS)
  Esses problemas podem ser úteis durante o trabalho com gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Por que meu gráfico conta, e não soma, os valores no eixo de valores?  
 A maior parte dos tipos de gráfico exigem valores numéricos ao longo do eixo de valor, que normalmente é o eixo y, para que o gráfico seja desenhado corretamente. Se o tipo de dados do seu campo de valor é `String`, o gráfico não poderá exibir um valor numérico, mesmo que haja numerais nos campos. Em vez disso, o gráfico exibirá uma contagem do número total de linhas que contêm um valor nesse campo. Para evitar esse comportamento, verifique se os campos usados para a série de valores têm tipos de dados numéricos, em vez de cadeias de caracteres que contêm números formatados.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
