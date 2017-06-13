---
title: "Painel agrupamento (construtor de relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0f8017dd30a085519f9dd5d3593aaa3d59329f8c
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="grouping-pane-report-builder"></a>Painel Agrupamento (Construtor de Relatórios)
  O painel Agrupamento exibe os grupos de linhas e de colunas referentes à região de dados Tablix selecionada no momento. O painel Agrupamento não está disponível para as regiões de dados Gráfico e Medidor. O painel Agrupamento contém os painéis Grupos de Linhas e Grupos de Colunas. Ele tem dois modos: padrão e Avançado. O modo padrão exibe uma exibição hierárquica dos membros dinâmicos dos grupos de linhas e de colunas. O modo Avançado exibe os membros dinâmicos e estáticos dos grupos de linhas e de colunas. Um grupo é um conjunto nomeado de dados de um conjunto de dados de relatório exibido em uma região de dados. Os grupos são organizados em hierarquias que incluem membros estáticos e dinâmicos. Para obter mais informações, consulte [Compreendendo grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Caso não veja o painel Agrupamento, na guia **Exibir**, no grupo **Mostrar/Ocultar**, clique em **Agrupamento**.  
  
 As células nas áreas dos grupos de linhas e de colunas podem ser membros estáticos ou dinâmicos de um grupo de linhas ou colunas tablix. Os membros estáticos repetem-se uma vez por grupo e normalmente contêm rótulos ou totais. Já os membros dinâmicos se repetem uma vez por instância de grupo e normalmente contêm os valores exclusivos da expressão de grupo. À medida que você seleciona células Tablix nas áreas dos grupos de linhas ou de colunas, o membro do grupo correspondente é selecionado no painel Grupos de Linhas ou Grupos de Colunas. Por outro lado, caso você selecione grupos no painel Agrupamento, a célula correspondente associada ao membro do grupo é selecionada na superfície de design. Para obter mais informações sobre as áreas dos grupos de linhas e de colunas Tablix, consulte [Áreas da região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 O painel Agrupamento oferece suporte aos seguintes modos:  
  
-   **Padrão.** Use o modo padrão para adicionar, editar ou excluir grupos. É possível adicionar grupos pai, filho e detalhados, arrastando campos do painel de dados do relatório e os inserindo na hierarquia de grupo. Para adicionar um grupo adjacente, você deve usar o atalho **Adicionar Grupo** . Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Avançado**. Use o **modo Avançado** para exibir todos os membros dos grupos de linhas e de colunas e definir propriedades em membros estáticos. Quando você cria grupos ou adiciona totais, as propriedades que controlam a forma como a região de dados Tablix processa linhas e colunas em todas as páginas de relatório são definidas automaticamente. Para ajustar essas propriedades manualmente, você deve defini-las no membro Tablix. Para obter mais informações, consulte [Controlando a exibição da região de dados Tablix em uma página do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Modo Padrão  
 No modo padrão, os painéis Grupos de Linhas e Grupos de Colunas mostram uma exibição hierárquica em todos os grupos pai, filho e adjacentes. Um grupo filho é exibido recuado sob o grupo pai. Um grupo adjacente é exibido no mesmo nível de recuo dos grupos irmãos. A seguinte figura mostra uma região de dados Tablix com grupos de linhas aninhados e grupos de colunas aninhados e adjacentes.  
  
 ![Linha aninhada e adjacente e grupos de colunas Tablix](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, linha aninhada e adjacente e grupos de colunas")  
  
 O painel Agrupamento exibe os grupos de linhas e colunas correspondentes. Na seguinte figura, o grupo baseado na subcategoria foi selecionado no painel Grupos de Linhas e a célula de agrupamento [Subcat] está selecionada na região de dados Tablix:  
  
 ![Painel de agrupamento para grupos de linhas e colunas aninhados](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "painel de agrupamento para grupos de linhas e colunas aninhados")  
  
 No painel Grupos de Linhas, o grupo baseado na subcategoria é filho do grupo baseado em categoria. No painel Grupos de Colunas, o grupo de país/região é filho do grupo de geografia. O grupo de ano e os grupos de país/região são grupos adjacentes.  
  
 Para obter mais informações, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>modo Avançado  
 No modo Avançado, os painéis Grupos de Linhas e Grupos de Colunas mostram uma exibição hierárquica de todos os grupos, incluindo membros estáticos e dinâmicos. Quando você selecionar um membro, o painel Propriedades exibirá as propriedades do membro Tablix selecionado.  
  
> [!NOTE]  
>  Para ativar/desativar o **Modo Avançado**, clique com o botão direito do mouse na seta para baixo ao lado do painel Grupos de Colunas e clique em **Modo Avançado**.  
  
 Na maior parte dos casos, as propriedades que controlam a exibição das linhas e das colunas dos grupos estáticos e dinâmicos são definidas automaticamente quando você cria um grupo ou adiciona totais. Para editar os valores padrão, você deve selecionar o membro do grupo no painel Grupos de Linhas ou Grupos de Colunas e alterar os valores da propriedade na janela Propriedades. As seguintes propriedades estão disponíveis:  
  
-   **FixedData**. Booliano. Para cabeçalhos de linha e coluna externos. Congele a área do grupo de linhas durante a rolagem vertical ou a área do grupo de colunas durante a rolagem horizontal em um processador como, por exemplo, HTML.  
  
-   **HideIfNoRows**. Booliano. Somente para membros estáticos. Se definido, Hidden e ToggleItem serão ignorados. Oculte esse membro caso a região de dados Tablix não contenha nenhuma linha de dados.  
  
-   **KeepTogether**. Booliano. Indica que o membro tablix inteiro e todos os membros aninhados devem ser mantidos em conjunto em uma página, se possível.  
  
-   **KeepWithGroup**. Booliano. Somente para membros de linha estáticos. Sempre que possível, mantenha a linha com o membro dinâmico irmão anterior ou seguinte, caso não esteja oculto. Para manter um cabeçalho de linha com seu grupo associado, defina KeepWithGroup como **After**.  
  
-   **RepeatOnNewPage**. Booliano. Somente para membros de linhas estáticas e nas quais KeepWithGroup não for None. Quando possível, repita essa linha estática em todas as páginas que tenham pelo menos uma instância do membro dinâmico especificado por KeepWithGroup. Para manter um cabeçalho de linha com seu grupo associado, defina RepeatOnNewPage como **True**.  
  
-   **Oculto**. Booliano. Indica se a linha ou a coluna deve permanecer oculta inicialmente.  
  
-   **ToggleItem.** Cadeia de caracteres. O nome da caixa de texto à qual adicionar a imagem de alternância. A caixa de texto deve estar no mesmo escopo de grupo ou um escopo contentor.  
  
 Para obter mais informações, consulte [Controlando a exibição da região de dados Tablix em uma página do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md), [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md) e [Exibir cabeçalhos de linhas e de colunas em várias páginas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Nem todos os membros estáticos têm um cabeçalho correspondente a uma célula na superfície de design. No painel Agrupamento, a seguinte convenção indica se um membro estático não tem nenhum cabeçalho:  
  
-   **Estático** Indica um membro estático com uma célula de cabeçalho.  
  
-   **(Estático)** Indica um membro estático sem uma célula de cabeçalho, conhecido como estático oculto.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
