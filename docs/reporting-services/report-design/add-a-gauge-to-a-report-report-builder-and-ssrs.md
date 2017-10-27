---
title: "Adicionar um medidor a um relatório (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de434ef80732d2a845fb41c972f0118fee357d14
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>Adicionar um medidor a um relatório (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , quando você quer resumir os dados em um formato visual, é possível usar uma região de dados do medidor. Depois de adicionar uma região de dados do medidor à superfície de design, você poderá arrastar campos do conjunto de dados do relatório para um painel de dados no medidor.  
  
## <a name="to-add-a-gauge-to-your-report"></a>Para adicionar um medidor a um relatório  
  
1.  Crie um relatório ou abra um relatório existente.  
  
2.  Na guia Inserir, clique duas vezes em Medidor. A caixa de diálogo **Selecionar Tipo de Medidor** é aberta.  
  
3.  Selecione o tipo de medidor que você deseja adicionar. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Ao contrário dos gráficos, os medidores têm apenas dois tipos: linear e radial. Os medidores disponíveis na caixa de diálogo **Selecionar um Tipo de Medidor** são modelos para esses dois tipos de medidores. Por isso, você não pode alterar o tipo de medidor após adicionar o medidor ao seu relatório. Você deverá excluir e adicionar novamente um medidor para alterar seu tipo.  
  
     Se o relatório não tiver nenhuma fonte de dados, nem conjunto de dados, a caixa de diálogo **Propriedades da Fonte de Dados** será aberta e o orientará durante as etapas para criar esses dois itens. Para obter mais informações, consulte [adicionar e verificar uma Conexão de dados &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
     Se o relatório tiver uma fonte de dados, e nenhum conjunto de dados, a caixa de diálogo **Propriedades do Conjunto de Dados** será aberta e o orientará durante as etapas para criar um conjunto de dados. Para obter mais informações, consulte [Create a Shared Dataset or Embedded Dataset &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
4.  Clique no medidor para exibir o painel de dados. Por padrão, um medidor tem um ponteiro correspondente a um valor. Você também pode adicionar outros ponteiros.  
  
5.  Adicione um campo do conjunto de dados à zona para arrastar e soltar do campo de dados. Você pode adicionar somente um campo. Para exibir vários campos, é necessário adicionar mais ponteiros, um para cada campo.  
  
     Clique com o botão direito do mouse na escala do medidor e selecione **Propriedades da Escala**. Digite um valor para **Mínimo** e **Máximo** da escala. Para obter mais informações, consulte [Definir mínimo ou máximo em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Medidores &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  

