---
title: Alterar a ordem de um parâmetro de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c87c0226cc79d175933fe01bc0e740eac1583e29
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285214"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>Alterar a ordem de um parâmetro de relatório (Construtor de Relatórios e SSRS)
  Altere a ordem dos parâmetros de relatório quando você tiver um parâmetro dependente que tenha sido listado antes de o parâmetro ser dependente. A ordem do parâmetro é importante quando você tem parâmetros em cascata ou quando você deseja mostrar aos usuários o valor padrão de um parâmetro antes que eles escolham os valores para outros parâmetros. Um parâmetro de relatório dependente contém uma referência, seja a consulta de valores padrão ou na consulta de valores válidos, a um parâmetro de consulta que aponta para um parâmetro de relatório que está depois dele na lista de parâmetros no painel **Dados do Relatório** .  
  
 A ordem em que você vê os parâmetros exibidos na barra de ferramentas do visualizador de relatórios é determinada pela ordem dos parâmetros no painel **Dados do Relatório** e do local dos parâmetros no painel de parâmetros personalizados. Para obter mais informações, consulte [Personalizar o painel de parâmetros em um relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>Para alterar a ordem dos parâmetros de relatório  
  
Você pode alterar a ordem dos parâmetros de relatório seguindo um destes procedimentos:  
  
-   Clique em um parâmetro no painel **Dados do Relatório** e use os botões de seta para cima e para baixo para movê-lo para cima ou para baixo na lista, como mostrado na imagem a seguir.  Quando você altera a ordem do parâmetro no painel **Dados do Relatório** , o local do parâmetro no painel de parâmetros é alterado.  
  
     ![Alterar a ordem dos parâmetros no painel Dados do Relatório](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "Alterar a ordem dos parâmetros no painel Dados do Relatório")  
  
-   No painel de parâmetros, arraste o parâmetro para uma nova coluna ou linha no painel. Quando você altera a localização do parâmetro no painel, a ordem do parâmetro é alterada no painel **Dados do Relatório** . Para obter mais informações sobre como mover parâmetros no painel, consulte [Personalizar o painel de parâmetros em um relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
