---
title: Exibir cabeçalhos de linhas e colunas em várias páginas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 51a549b7fbea2bc4b1c5e41114e831ff3f68550b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010350"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>Exibir cabeçalhos de linhas e colunas em várias páginas (Construtor de Relatórios e SSRS)
  Você pode controlar se é preciso repetir cabeçalhos de linha e coluna em todas as páginas de uma região de dados tablix com várias páginas. Uma região de dados tablix pode ser uma tabela, uma matriz ou uma lista.  
  
 O modo como você controla as linhas e as colunas dependerá se a região de dados de tablix tem cabeçalhos de grupo. Quando você clicar em uma região de dados de tablix que tem cabeçalhos de grupo, uma linha pontilhada mostrará as áreas de tablix, como mostrado na figura seguinte:  
  
 ![Áreas da região de dados Tablix](../media/rs-tablixareas.gif "áreas da região de dados Tablix")  
  
 Cabeçalhos de grupos de linhas e colunas são criados automaticamente quando você adiciona grupos usando o assistente de Nova Tabela ou de Novo Gráfico, adicionando campos ao painel Agrupamento ou usando menus de contexto. Se a região de dados de tablix tiver apenas uma área de corpo de tablix e nenhum cabeçalho de grupo, as linhas e as colunas serão os membros do tablix.  
  
 Para membros estáticos, você pode exibir as linhas adjacentes superiores ou as colunas adjacentes em várias páginas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-row-headers-on-multiple-pages"></a>Para exibir cabeçalhos de linha em várias páginas  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Em **Cabeçalhos de Linha**, selecione **Repetir linhas de cabeçalho em cada página**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-column-headers-on-multiple-pages"></a>Para exibir cabeçalhos de coluna em várias páginas  
  
1.  Clique com o botão direito do mouse na alça de canto, na linha ou na coluna de uma região de dados tablix e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Em **Cabeçalhos de Colunas**, selecione **Repetir colunas de cabeçalho em cada página**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-a-static-tablix-member-row-or-column-on-multiple-pages"></a>Para exibir um membro de tablix estático (linha ou coluna) em várias páginas  
  
1.  Na superfície de design, clique no manipulador de linha ou coluna da região de dados de tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Linhas exibe os membros hierárquicos estáticos e dinâmicos para a hierarquia de grupos de linhas e o painel Grupos de colunas mostra uma exibição semelhante para a hierarquia de grupos de coluna.  
  
3.  Clique no membro estático que corresponde àquele (linha ou coluna) que deverá permanecer visível durante a rolagem. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
     Se você não vir o painel Propriedades, clique na guia **Exibir** na parte superior da janela do Construtor de Relatórios e clique em **Propriedades**.  
  
4.  No painel Propriedades, defina **RepeatOnNewPage** como True.  
  
5.  Defina **KeepWithGroup** como After.  
  
6.  Repita essa etapa para todos os membros adjacentes desejados.  
  
7.  Visualize o relatório.  
  
 À medida que você exibe cada página do relatório que a região de dados do tablix abrange, os membros de tablix se repetem em cada página.  
  
## <a name="see-also"></a>Consulte também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;SSRS e construtor de relatórios&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [Controlando quebras de páginas, títulos, colunas e linhas &#40;SSRS e construtor de relatórios&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;SSRS e construtor de relatórios&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  