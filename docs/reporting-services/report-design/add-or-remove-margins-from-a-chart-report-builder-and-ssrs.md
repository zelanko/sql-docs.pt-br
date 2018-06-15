---
title: Adicionar ou remover margens de um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a42d78cca3bc4835771c2e9fcf30a184232aeb38
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021073"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>Adicionar ou remover margens de um gráfico (Construtor de Relatórios e SSRS)
Para os tipos de gráfico de Colunas e de Dispersão nos relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o gráfico automaticamente adiciona margens laterais nas extremidades do eixo x. Nos tipos de gráfico de Barras, o gráfico adiciona automaticamente margens laterais nas extremidades do eixo y. Em todos os outros tipos de gráfico, as margens laterais não são adicionadas. Não é possível alterar o tamanho da margem.  
  
 Este tópico não se aplica aos tipos de gráfico de pizza, anel, funil ou pirâmide.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-enable-or-disable-side-margins"></a>Para habilitar ou desabilitar as margens laterais  
  
1.  Clique com o botão direito do mouse no eixo e selecione **Propriedades do Eixo**. A caixa de diálogo **Propriedades do Eixo Vertical** ou **Horizontal** é exibida.  
  
2.  Na página **Opções do Eixo** , defina a propriedade **Margens laterais** :  
  
    -   **Automático** O gráfico determinará se deve ser adicionada uma margem lateral com base no tipo de gráfico.  
  
    -   **Desabilitado** Os gráficos de barra, coluna e dispersão não terão nenhuma margem lateral.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções de Eixo &#40;Construtor de Relatórios e SSRS&#41;](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
