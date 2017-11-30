---
title: "Permitir que uma caixa de texto seja ampliada ou reduzida (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dbc01e78-5993-47e5-af04-34f9e3bbcee1
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 1bdcf9e8abfc51cf514bcc57b8591186a4768ac2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs"></a>Permitir que uma caixa de texto seja ampliada ou reduzida (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , as caixas de texto não são apenas as caixas autônomas na superfície de design do relatório. Todas as células de uma tabela ou matriz (uma região de dados tablix) também contêm uma caixa de texto, que pode ser formatada da mesma maneira que caixas de texto autônomas. Por padrão, as caixas de texto têm tamanho fixo. Você pode definir opções que permitem a expansão ou redução da caixa de texto com base em seu conteúdo. Essas opções correspondem à propriedade **CanGrow** ou **CanShrink** no painel Propriedades.  
  
## <a name="to-allow-a-text-box-to-grow-or-shrink"></a>Para permitir que uma caixa de texto cresça ou seja reduzida  
  
1.  Clique com o botão direito do mouse na caixa de texto e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique na guia **Geral** .  
  
    -   Para permitir a expansão vertical da caixa de texto com base no seu conteúdo, selecione **Permitir aumento da altura**.  
  
    -   Para permitir a redução da caixa de texto com base no seu conteúdo, selecione **Permitir diminuição da altura**.  
  
## <a name="see-also"></a>Consulte também  
 [Caixas de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)  
  
  
