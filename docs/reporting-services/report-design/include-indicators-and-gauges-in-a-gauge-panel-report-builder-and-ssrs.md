---
title: "Incluir indicadores e medidores em um painel de medidores (Construtor de Relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4597b87876b52b41810f62423a59fef7b45394b8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>Incluir indicadores e medidores em um painel de medidores (Construtor de Relatórios e SSRS)
  O painel de medidores é o contêiner de nível superior que mantém um ou mais medidores e indicadores. Os indicadores podem ser inseridos em medidores ou colocados ao lado deles no painel de medidores.  
  
 Se o indicador e o medidor forem adjacentes no painel de medidores e mostrarem dados de campos diferentes, talvez você queira adicionar rótulos para esclarecer quais dados são transmitidos pelo medidor e pelo indicador.  
  
 As opções de indicador e medidor podem ser definidas com o uso de expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>Para inserir um indicador em um medidor  
  
1.  Abra um relatório existente ou crie um novo relatório que contenha uma tabela e matriz com os dados a serem exibidos.   
  
2.  Insira uma coluna em sua tabela ou matriz. Para obter mais informações, consulte [Inserir ou excluir uma coluna &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Na guia **Inserir** , no grupo **Regiões de Dados** , clique em **Medidor**e clique em uma célula na nova coluna. A caixa de diálogo **Selecionar Tipo de Medidor** é exibida.  
  
4.  Clique em **Radial**. O primeiro medidor radial é selecionado.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Clique no medidor. O painel **Dados do Medidor** é exibido.  
  
7.  Na área **Valores** , na caixa de listagem **(Não Especificado)** , clique no campo cujos valores você deseja exibir no medidor. Se desejar, arraste o campo a ser usado a partir do conjunto de dados de relatório.  
  
8.  Clique com o botão direito do mouse no medidor, clique em **Adicionar Indicador**e em **Filho**. A caixa de diálogo **Selecionar Estilo de Indicador** é aberta.  
  
9. Na caixa de diálogo **Selecionar Estilo de Indicador** , no painel esquerdo, clique no tipo de indicador desejado e no conjunto de indicadores.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. Clique no indicador. O painel **Dados do Medidor** é exibido.  
  
12. Na área **Valores** , na caixa de listagem **(Não Especificado)** , clique no campo cujos valores você deseja exibir como indicador. Se desejar, arraste o campo a ser usado a partir do conjunto de dados de relatório.  
  
     O campo pode ser o mesmo ou um campo diferente daquele usado no medidor.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>Para mostrar um indicador e um medidor lado a lado  
  
1.  Abra um relatório existente ou crie um novo relatório que contenha uma tabela e matriz com os dados a serem exibidos.  
  
2.  Insira uma coluna em sua tabela ou matriz. Para obter mais informações, consulte [Inserir ou excluir uma coluna &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Na guia **Inserir** , no grupo **Regiões de Dados** , clique em **Medidor**e clique em uma célula na coluna inserida. A caixa de diálogo **Selecionar Tipo de Medidor** é exibida.  
  
4.  Clique em **Radial**. O primeiro medidor radial é selecionado.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Clique no medidor. O painel **Dados do Medidor** é exibido.  
  
7.  Na área **Valores** , na caixa de listagem **(Não Especificado)** , clique no campo cujos valores você deseja exibir no medidor. Se desejar, arraste o campo a ser usado a partir do conjunto de dados de relatório.  
  
8.  Clique com o botão direito do mouse no medidor, clique em **Adicionar Indicador**e em **Adjacente**. A caixa de diálogo **Selecionar Estilo de Indicador** é aberta.  
  
9. Na caixa de diálogo **Selecionar Estilo de Indicador** , no painel esquerdo, clique no tipo de indicador desejado e no conjunto de indicadores.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. Clique no indicador. O painel **Dados do Medidor** é exibido.  
  
12. Na área **Valores** , na caixa de listagem **(Não Especificado)** , clique no campo cujos valores você deseja exibir como indicador. Se desejar, arraste o campo a ser usado a partir do conjunto de dados de relatório.  
  
     O campo pode ser o mesmo ou um campo diferente daquele usado no medidor.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
14. Clique com o botão direito do mouse no painel de medidores e clique em **Adicionar Rótulo**. Um rótulo é adicionado ao painel de medidores. Repita uma mais vez.  
  
     O painel de medidores tem dois rótulos.  
  
15. Arraste cada rótulo para um local perto do medidor ou do indicador.  
  
16. Clique com o botão direito do mouse no rótulo ao lado do medidor, clique em **Propriedades do Rótulo**e digite o texto desejado na caixa **Texto** .  
  
17. Clique com o botão direito do mouse no rótulo ao lado do indicador, clique em **Propriedades do Rótulo**e digite o texto desejado na caixa **Texto** .  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
