---
title: Solução de problemas de gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e9bd6c14bcc6157b65d851d25019c8090a8f8485
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solução de problemas de gráficos (Construtor de Relatórios e SSRS)
  Esses problemas podem ser úteis durante o trabalho com gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Por que meu gráfico conta, e não soma, os valores no eixo de valores?  
 A maior parte dos tipos de gráfico exigem valores numéricos ao longo do eixo de valor, que normalmente é o eixo y, para que o gráfico seja desenhado corretamente. Se o tipo de dados do campo de valor for **String**, o gráfico não poderá exibir um valor numérico, mesmo que haja numerais nos campos. Em vez disso, o gráfico exibirá uma contagem do número total de linhas que contêm um valor nesse campo. Para evitar esse comportamento, verifique se os campos usados para a série de valores têm tipos de dados numéricos, em vez de cadeias de caracteres que contêm números formatados.  

## <a name="need-more-help"></a>Precisa de mais ajuda?  
   
  Experimente:  
 * [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services) no Stack Overflow  
 * Registre um problema ou uma sugestão no [UserVoice do Microsoft SQL Server](https://feedback.azure.com/forums/908035-sql-server).  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
