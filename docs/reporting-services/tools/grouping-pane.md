---
title: Painel Agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10033"
- sql13.rtp.rptdesigner.group.f1
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 8b4bd0b3-ec97-48f8-8bfb-82a53a2f35a1
caps.latest.revision: 22
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: af8410f48f43e656946930df78df2e519dc41154
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="grouping-pane"></a>Painel Agrupamento
Ao projetar relatórios do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o painel Agrupamento exibe os grupos de linhas e de colunas referentes à região de dados tablix selecionada no momento. O painel Agrupamento não está disponível para as regiões de dados Gráfico e Medidor. O painel Agrupamento consiste nos painéis Grupos de Linhas e Grupos de Colunas. Ele tem dois modos: padrão e Avançado. O modo padrão exibe uma exibição hierárquica dos membros dinâmicos dos grupos de linhas e de colunas. O modo Avançado exibe os membros dinâmicos e estáticos dos grupos de linhas e de colunas. Um grupo é um conjunto nomeado de dados de um conjunto de dados de relatório exibido em uma região de dados. Os grupos são organizados em hierarquias que incluem membros estáticos e dinâmicos. Para obter mais informações, consulte [Compreendendo grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Se o painel Agrupamento não estiver visível, no menu **Relatório** , clique em **Agrupamento**.
  
 As células nas áreas dos grupos de linhas e de colunas podem ser membros estáticos ou dinâmicos de um grupo. Os membros estáticos repetem-se uma vez por grupo e normalmente contêm rótulos ou totais. Já os membros dinâmicos se repetem uma vez por instância de grupo e normalmente contêm os valores exclusivos da expressão de grupo. À medida que você seleciona células Tablix nas áreas dos grupos de linhas ou de colunas, o membro do grupo correspondente é selecionado no painel Grupos de Linhas ou Grupos de Colunas. Por outro lado, caso você selecione grupos no painel Agrupamento, a célula correspondente associada ao membro do grupo é selecionada na superfície de design. Para obter mais informações sobre as áreas dos grupos de linhas e de colunas Tablix, consulte [Áreas da região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 O painel Agrupamento oferece suporte aos seguintes modos:  
  
-   **Padrão.** Use o modo padrão para adicionar, editar ou excluir grupos. É possível adicionar grupos pai, filho e detalhados, arrastando campos do painel de dados do relatório e os inserindo na hierarquia de grupo. Para adicionar um grupo adjacente, você deve usar o atalho **Adicionar Grupo** . Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Avançado**. Use o **modo Avançado** para exibir todos os membros dos grupos de linhas e de colunas e definir propriedades em membros estáticos. Quando você cria grupos ou adiciona totais, as propriedades que controlam a forma como a região de dados Tablix processa linhas e colunas em todas as páginas de relatório são definidas automaticamente. Para ajustar essas propriedades manualmente, você deve defini-las no membro Tablix. Para obter mais informações, consulte [Controlando a exibição da região de dados Tablix em uma página do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Modo Padrão  
 No modo padrão, os painéis Grupos de Linhas e Grupos de Colunas mostram uma exibição hierárquica em todos os grupos pai, filho e adjacentes. Um grupo filho é exibido recuado sob o grupo pai. Um grupo adjacente é exibido no mesmo nível de recuo dos grupos irmãos. A seguinte figura mostra uma região de dados Tablix com grupos de linhas aninhados e grupos de colunas aninhados e adjacentes.  
  
 ![Tablix, grupos de linhas e colunas aninhadas e adjacentes](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, grupos de linhas e colunas aninhadas e adjacentes")  
  
 O painel Agrupamento exibe os grupos de linhas e colunas correspondentes. Na seguinte figura, o grupo baseado na subcategoria foi selecionado no painel Grupos de Linhas, e a célula de agrupamento [Subcat] está selecionada na região de dados Tablix:  
  
 ![Painel Agrupamento para grupos de linhas e colunas aninhadas](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "Painel Agrupamento para grupos de linhas e colunas aninhadas")  
  
 No painel Grupos de Linhas, o grupo baseado na subcategoria é filho do grupo baseado em categoria. No painel Grupos de Colunas, o grupo de país/região é filho do grupo de geografia. O grupo de ano e os grupos de país/região são grupos adjacentes.  
  
 Para obter mais informações, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>modo Avançado  
No modo Avançado, é possível exibir todos os membros estáticos e dinâmicos de um grupo. Quando você seleciona um membro, a janela Propriedades exibe as propriedades do **Membro Tablix**selecionado no momento.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Para alternar **Modo Avançado**, clique com o botão direito do mouse na seta para baixo ao lado do painel Grupos de Colunas e clique em **Modo Avançado**.  
  
Na maior parte dos casos, as propriedades que controlam a exibição das linhas e das colunas dos grupos estáticos e dinâmicos são definidas automaticamente quando você cria um grupo ou adiciona totais. 

Para editar os valores padrão, você deve selecionar o membro do grupo no painel Grupos de Linhas ou Grupos de Colunas e alterar os valores da propriedade na janela Propriedades. Se o painel Propriedades não estiver visível, no menu **Exibir** , clique em **Propriedades** ou pressione **F4**.  As seguintes propriedades estão disponíveis:  
  
-   **FixedData**. Booliano. Para cabeçalhos de linha e coluna externos. Congele a área do grupo de linhas durante a rolagem vertical ou a área do grupo de colunas durante a rolagem horizontal em um processador como, por exemplo, HTML.  
  
-   **HideIfNoRows**. Booliano. Somente para membros estáticos. Se definido, Hidden e ToggleItem serão ignorados. Oculte esse membro caso a região de dados Tablix não contenha nenhuma linha de dados.  
  
-   **KeepTogether**.  
  
-   **KeepWithGroup**. Booliano. Somente para membros de linha estáticos. Sempre que possível, mantenha a linha com o membro dinâmico irmão anterior ou seguinte, caso não esteja oculto.  
  
-   **RepeatOnNewPage**. Booliano. Somente para membros de linhas estáticas e nas quais KeepWithGroup não for None. Quando possível, repita essa linha estática em todas as páginas que tenham pelo menos uma instância do membro dinâmico especificado por KeepWithGroup.  
  
-   **Oculto**. Booliano. Indica se a linha ou a coluna deve permanecer oculta inicialmente.  
  
-   **ToggleItem.** Cadeia de caracteres. O nome da caixa de texto à qual adicionar a imagem de alternância. A caixa de texto deve estar no mesmo escopo de grupo ou um escopo contentor.  
  
 Para obter mais informações sobre como esse comportamento pode ser controlado em uma região de dados Tablix, consulte [Controlando a exibição da região de dados Tablix em uma página de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
 Nem todos os membros estáticos têm um cabeçalho correspondente a uma célula na superfície de design. No painel Agrupamento, a seguinte convenção indica se um membro estático não tem nenhum cabeçalho:  
  
-   **Estático** Indica um membro estático com uma célula de cabeçalho.  
  
-   **(Estático)** Indica um membro estático sem uma célula de cabeçalho, conhecido como estático oculto.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
