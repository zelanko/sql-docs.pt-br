---
title: Exibir cabeçalhos de linhas e colunas em várias páginas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f420f92cf6dd2099244a1f2bd782ee9b72e2aebd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608724"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>Exibir cabeçalhos de linhas e colunas em várias páginas (Construtor de Relatórios e SSRS)
  Você pode controlar se os cabeçalhos de linha e de coluna serão repetidos em cada página de um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] em uma região de dados tablix (uma tabela, matriz ou lista) que abrange várias páginas.
  
 O modo como você controla as linhas e as colunas dependerá se a região de dados de tablix tem cabeçalhos de grupo. Quando você clicar em uma região de dados de tablix que tem cabeçalhos de grupo, uma linha pontilhada mostrará as áreas de tablix, como mostrado na figura seguinte:  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 Cabeçalhos de grupos de linhas e colunas são criados automaticamente quando você adiciona grupos usando o assistente de Nova Tabela ou de Novo Gráfico, adicionando campos ao painel Agrupamento ou usando menus de contexto. Se a região de dados de tablix tiver apenas uma área de corpo de tablix e nenhum cabeçalho de grupo, as linhas e as colunas serão os membros do tablix.  
  
 Para membros estáticos, você pode exibir as linhas adjacentes superiores ou as colunas adjacentes em várias páginas.  
  
## <a name="to-display-row-headers-on-multiple-pages"></a>Para exibir cabeçalhos de linha em várias páginas  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Em **Cabeçalhos de Linha**, selecione **Repetir linhas de cabeçalho em cada página**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-column-headers-on-multiple-pages"></a>Para exibir cabeçalhos de coluna em várias páginas  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Em **Cabeçalhos de Colunas**, selecione **Repetir colunas de cabeçalho em cada página**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-a-static-row-or-column-on-multiple-pages"></a>Para exibir uma linha ou coluna estática em várias páginas  
  
1.  Na superfície de design, clique no manipulador de linha ou coluna da região de dados de tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Linhas exibe os membros hierárquicos estáticos e dinâmicos para a hierarquia de grupos de linhas e o painel Grupos de colunas mostra uma exibição semelhante para a hierarquia de grupos de coluna.  
  
3.  Clique no membro estático que corresponde àquele (linha ou coluna) que deverá permanecer visível durante a rolagem. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
     Se você não vir o painel Propriedades, clique na guia **Exibir** na parte superior da janela do Construtor de Relatórios e clique em **Propriedades**.  
  
4.  No painel Propriedades, defina **RepeatOnNewPage** como True.  
  
5.  Defina **KeepWithGroup** como After.  
  
6.  Repita essa etapa para todos os membros adjacentes desejados.  
  
7.  Visualize o relatório.  
  
 À medida que você exibe cada página do relatório que a região de dados do tablix abrange, os membros de tablix se repetem em cada página.  
  
## <a name="see-also"></a>Consulte Também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Controlando quebras de páginas, títulos, colunas e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
