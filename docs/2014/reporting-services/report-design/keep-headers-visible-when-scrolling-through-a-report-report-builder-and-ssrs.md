---
title: Manter os cabeçalhos visíveis ao rolar por um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37c3dc20ab537e7cb8bf69099dbd6d24ff384731
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105596"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>Manter os cabeçalhos visíveis ao rolar por um relatório (Construtor de Relatórios e SSRS)
  Para impedir que os rótulos de linha e coluna rolem para fora da exibição depois da renderização de um relatório, você pode congelar os títulos de linha ou coluna.  
  
 O modo de controlar as linhas e colunas depende se você tem uma tabela ou matriz. Se você tiver uma tabela, configure os membros estáticos (linhas e cabeçalhos de coluna) para permanecerem visíveis. Se você tiver uma matriz, configure as linhas e cabeçalhos de grupos de coluna para permanecerem visíveis.  
  
 Se você exportar o relatório para Excel, o cabeçalho não será congelado automaticamente. Você pode congelar o painel no Excel. Para obter mais informações, consulte a seção **Cabeçalhos e rodapés de página** de [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Mesmo se uma tabela tiver grupos de linhas e de coluna, você não conseguirá manter esses cabeçalhos de grupo visíveis durante a rolagem  
  
 A imagem a seguir mostra uma tabela.  
  
 ![Table](../media/table.png "Tabela")  
  
 A imagem a seguir mostra uma matriz.  
  
 ![Matriz](../media/matrix.png "Matriz")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>Para manter os cabeçalhos de grupo de matriz visíveis ao rolar  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Na guia **Geral** , em **Cabeçalhos de Linha** ou **Cabeçalhos de Coluna**, selecione **O cabeçalho deve permanecer visível ao rolar**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>Para manter um membro tablix estático (linha ou coluna) visível ao rolar  
  
1.  Na superfície de design, clique em qualquer lugar na tabela para exibir membros estáticos, bem como grupos, no painel de agrupamento.  
  
     ![Painel Agrupamento](../media/grouppane-updated.png "painel Agrupamento")  
  
     O painel Grupos de Linhas exibe os membros hierárquicos estáticos e dinâmicos para a hierarquia de grupos de linhas, e o painel Grupos de colunas mostra uma exibição semelhante para a hierarquia de grupos de coluna.  
  
2.  À direita do painel de agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**.  
  
3.  Clique no membro estático (linha ou coluna) que deverá permanecer visível durante a rolagem. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
     ![Propriedades do membro Tablix](../media/grouppane-tablixmember-updated.png "Propriedades do membro Tablix")  
  
4.  No painel Propriedades, defina **FixedData** como `True`.  
  
5.  Repita essa etapa para todos os membros adjacentes que você deseja manter visíveis durante a rolagem.  
  
6.  Visualize o relatório.  
  
 À medida que você pagina para baixo ou pelo relatório, os membros tablix estáticos permanecem na exibição.  
  
## <a name="see-also"></a>Consulte Também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos de linha e coluna em várias páginas &#40;Construtor de Relatórios e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [Painel Agrupamento &#40;Construtor de Relatórios&#41;](grouping-pane-report-builder.md)  
  
  
