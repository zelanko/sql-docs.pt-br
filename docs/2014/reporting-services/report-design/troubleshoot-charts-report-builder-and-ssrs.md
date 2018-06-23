---
title: Solução de problemas de gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b5369ef0fd3f96345e0fc7e0c688f1230bfe41c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115370"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solução de problemas de gráficos (Construtor de Relatórios e SSRS)
  Esses problemas podem ser úteis durante o trabalho com gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Por que meu gráfico conta, e não soma, os valores no eixo de valores?  
 A maior parte dos tipos de gráfico exigem valores numéricos ao longo do eixo de valor, que normalmente é o eixo y, para que o gráfico seja desenhado corretamente. Se o tipo de dados do seu campo de valor for `String`, o gráfico não pode exibir um valor numérico, mesmo que haja numerais nos campos. Em vez disso, o gráfico exibirá uma contagem do número total de linhas que contêm um valor nesse campo. Para evitar esse comportamento, verifique se os campos usados para a série de valores têm tipos de dados numéricos, em vez de cadeias de caracteres que contêm números formatados.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;SSRS e construtor de relatórios&#41;](charts-report-builder-and-ssrs.md)  
  
  