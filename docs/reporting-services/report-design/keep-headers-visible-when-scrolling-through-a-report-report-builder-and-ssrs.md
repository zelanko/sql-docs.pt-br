---
title: "Manter os cabe&#231;alhos vis&#237;veis ao rolar por um relat&#243;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
caps.latest.revision: 10
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# Manter os cabe&#231;alhos vis&#237;veis ao rolar por um relat&#243;rio (Construtor de Relat&#243;rios e SSRS)
  Para impedir que os rótulos de linha e coluna rolem para fora da exibição depois da renderização de um relatório, você pode congelar os títulos de linha ou coluna.  
  
 O modo de controlar as linhas e colunas depende se você tem uma tabela ou matriz. Se você tiver uma tabela, configure os membros estáticos (linhas e cabeçalhos de coluna) para permanecerem visíveis. Se você tiver uma matriz, configure as linhas e cabeçalhos de grupos de coluna para permanecerem visíveis.  
  
 Se você exportar o relatório para Excel, o cabeçalho não será congelado automaticamente. Você pode congelar o painel no Excel. Para obter mais informações, consulte a seção **Cabeçalhos e rodapés de página** de [Exportação para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Mesmo se uma tabela tiver grupos de linhas e de coluna, você não conseguirá manter esses cabeçalhos de grupo visíveis durante a rolagem  
  
 A imagem a seguir mostra uma tabela.  
  
 ![Tabela](../../reporting-services/report-design/media/table.png "Tabela")  
  
 A imagem a seguir mostra uma matriz.  
  
 ![Matriz](../../reporting-services/report-design/media/matrix.png "Matriz")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para manter os cabeçalhos de grupo de matriz visíveis ao rolar  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Na guia **Geral** , em **Cabeçalhos de Linha** ou **Cabeçalhos de Coluna**, selecione **O cabeçalho deve permanecer visível ao rolar**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para manter um membro tablix estático (linha ou coluna) visível ao rolar  
  
1.  Na superfície de design, clique em qualquer lugar na tabela para exibir membros estáticos, bem como grupos, no painel de agrupamento.  
  
     ![painel Agrupamento](../../reporting-services/report-design/media/grouppane-updated.png "painel Agrupamento")  
  
     O painel Grupos de Linhas exibe os membros hierárquicos estáticos e dinâmicos para a hierarquia de grupos de linhas, e o painel Grupos de colunas mostra uma exibição semelhante para a hierarquia de grupos de coluna.  
  
2.  À direita do painel de agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**.  
  
3.  Clique no membro estático (linha ou coluna) que deverá permanecer visível durante a rolagem. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
     ![Propriedades do membro Tablix](../../reporting-services/report-design/media/grouppane-tablixmember-updated.png "Propriedades do membro Tablix")  
  
4.  No painel Propriedades, defina **FixedData** como **True**.  
  
5.  Repita essa etapa para todos os membros adjacentes que você deseja manter visíveis durante a rolagem.  
  
6.  Visualize o relatório.  
  
 À medida que você pagina para baixo ou pelo relatório, os membros tablix estáticos permanecem na exibição.  
  
## Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos de linhas e colunas em várias páginas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [Painel Agrupamento &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)  
  
  