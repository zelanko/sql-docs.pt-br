---
title: Solução de problemas de gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65dac70a2b3eebc090cf282d650aff3840d00e89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738664"
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
  
  
