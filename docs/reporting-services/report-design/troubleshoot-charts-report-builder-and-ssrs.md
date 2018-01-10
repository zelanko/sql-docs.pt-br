---
title: "Solução de problemas de gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 76e6a49e935ea5744686be628f6a7138d6feed91
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solução de problemas de gráficos (Construtor de Relatórios e SSRS)
  Esses problemas podem ser úteis durante o trabalho com gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Por que meu gráfico conta, e não soma, os valores no eixo de valores?  
 A maior parte dos tipos de gráfico exigem valores numéricos ao longo do eixo de valor, que normalmente é o eixo y, para que o gráfico seja desenhado corretamente. Se o tipo de dados do campo de valor for **String**, o gráfico não poderá exibir um valor numérico, mesmo que haja numerais nos campos. Em vez disso, o gráfico exibirá uma contagem do número total de linhas que contêm um valor nesse campo. Para evitar esse comportamento, verifique se os campos usados para a série de valores têm tipos de dados numéricos, em vez de cadeias de caracteres que contêm números formatados.  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
