---
title: Iniciar valores do gráfico de pizza na parte superior da pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2da5ccaf0fe846a26959970bd9bf3e939b5a2558
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256255"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>Iniciar valores do gráfico de pizza na parte superior da pizza (Construtor de Relatórios e SSRS)
  Por padrão, em gráficos de pizza, o primeiro valor do conjunto de dados inicia a 90 graus da parte superior da pizza. Você pode preferir que o primeiro seja iniciado na parte superior.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>Para iniciar o gráfico de pizza na parte superior da pizza  
  
1.  Clique na própria pizza.  
  
2.  Se o painel **Propriedades** não for aberto, na guia **Exibição** , clique em **Propriedades**.  
  
3.  No painel **Propriedades** , sob **Atributos Personalizados**, altere **PieStartAngle** de **0** para **270**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 O primeiro valor agora inicia na parte superior do gráfico de pizza.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
