---
title: Adicionar locais personalizados a um mapa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e5961a4d4984a4da5abd788903a05789de862db7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020879"
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>Adicionar locais personalizados a um mapa (Construtor de Relatórios e SSRS)
  Depois que adicionar um mapa a um relatório, você poderá adicionar seus próprios locais de ponto.  
  
 As propriedades de exibição de todos os pontos em uma camada são controladas pela definição de opções para as propriedades de ponto da camada. Para um ponto inserido selecionado, você pode substituir as propriedades de exibição.  
  
> [!NOTE]  
>  Quando você substituir as propriedades de exibição da camada para o ponto inserido, as alterações feitas não serão reversíveis.  
  
 Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-point-layer"></a>Para adicionar uma camada de ponto  
  
1.  Na superfície de design de relatório, clique no mapa para selecioná-lo e exibir o painel Mapa.  
  
2.  Na barra de ferramentas, clique em **Adicionar Camada**.  
  
3.  Na lista suspensa, clique em **Adicionar Camada de Ponto**. Uma camada de ponto sem pontos é adicionada ao mapa. Por padrão, a camada de ponto está pronta para pontos inseridos.  
  
### <a name="to-add-a-custom-point"></a>Para adicionar um ponto personalizado  
  
1.  Na superfície de design de relatório, clique no mapa para selecioná-lo e exibir o painel Mapa.  
  
2.  No painel Mapa, clique com o botão direito do mouse em uma camada de ponto que tenha o tipo **Inserido**e clique em **Adicionar Ponto**. O cursor se transforma em uma cruz.  
  
3.  Para adicionar um ponto, clique em um local no mapa. Um ponto inserido é adicionado à camada selecionada no local em que você clica.  
  
### <a name="to-customize-the-display-for-an-embedded-point"></a>Para personalizar a exibição para um ponto inserido  
  
1.  Clique com o botão direito do mouse no ponto e clique em **Propriedades de Ponto**. A caixa de diálogo **Propriedades do Ponto Inserido do Mapa** aparece.  
  
2.  Clique em **Substituir opções de ponto para esta camada**. Várias páginas de propriedades aparecem no painel esquerdo.  
  
3.  Clique nas páginas e defina as propriedades de exibição que você deseja aplicar a esse ponto.  
  
## <a name="see-also"></a>Consulte também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
