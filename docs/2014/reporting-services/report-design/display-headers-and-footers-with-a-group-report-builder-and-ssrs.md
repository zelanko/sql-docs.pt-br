---
title: Exibir cabeçalhos e rodapés com um grupo (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 72b8eda95def001cbb97bc6a91401a7765a6b8cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020321"
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>Exibir cabeçalhos e rodapés com um grupo (Construtor de Relatórios e SSRS)
  Você pode ajudar a controlar se uma linha estática, como um cabeçalho ou rodapé de grupo, será renderizada com linhas dinâmicas associadas a um grupo de uma região de dados tablix.  
  
 Para repetir todos os títulos de linha ou coluna em várias páginas, você pode definir as propriedades da região de dados tablix. Para obter informações, consulte [Exibir cabeçalhos de linhas e colunas em várias páginas &#40;Construtor de Relatórios e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Para controlar o comportamento de renderização de linhas e colunas dinâmicas associadas a grupos aninhados ou de linhas e colunas estáticas associadas a rótulos ou subtotais, você deve definir as propriedades do membro tablix. Um membro tablix representa uma linha ou coluna estática ou dinâmica. Um membro estático ocorre uma vez. Por exemplo, uma linha de total geral é uma linha estática. Um membro dinâmico ocorre uma vez para cada instância do grupo. Por exemplo, uma linha associada a um grupo com a expressão de grupo [Território] ocorre uma vez para cada valor exclusivo de território. Para obter mais informações sobre os membros do Tablix, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Você pode definir um membro tablix no painel Agrupamento e as propriedades **KeepWithGroup**, **KeepTogether**e **RepeatOnNewPage** no painel Propriedades. Use **KeepWithGroup** para ajudar a exibir cabeçalhos de grupo e rodapés na mesma página como o grupo. Use **KeepTogether** para ajudar a exibir os membros estáticos com as linhas ou colunas de um grupo. Use **RepeatOnNewPage** para repetir o cabeçalho de grupo ou rodapé em toda página que exibe uma instância completa do membro de grupo de linhas designado pelo valor **KeepWithGroup** . **RepeatOnNewPage** não tem suporte para membros de grupo de colunas.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether**e **RepeatOnNewPage** são propriedades do membro de grupo que podem ser definidas usando o **Modo Avançado** do painel Agrupamento. Para obter mais informações, consulte [Painel Agrupamento &#40;Construtor de Relatórios&#41;](grouping-pane-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>Para manter uma linha estática com um conjunto de linhas dinâmicas associado a um grupo de linhas  
  
1.  Na superfície de design, clique em qualquer lugar na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Linhas exibe os membros estáticos e dinâmicos hierárquicos da hierarquia de grupos de linhas.  
  
3.  Clique no membro estático que corresponde ao cabeçalho ou rodapé de linha que você deseja manter com as linhas do grupo. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
4.  No painel Propriedades, clique em **KeepWithGroup**e, em seguida, escolha um dos valores seguintes da lista suspensa:  
  
    -   **Nenhum** Selecione essa opção para não indicar nenhuma preferência para manter esse membro com os membros do grupo de linhas selecionado.  
  
    -   **Antes de** Selecione essa opção para manter esse membro com os membros do grupo anterior. Você pode usar isso para linhas de rodapé de grupo.  
  
    -   **Depois de** Selecione essa opção para manter esse membro com os membros do grupo seguinte. Você pode usar isso para linhas de cabeçalho de grupo.  
  
5.  (Opcional) Visualize o relatório. Sempre que possível, o processador de relatório manterá esse membro com os membros de grupo de linhas especificados.  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>Para manter uma coluna estática com um conjunto de colunas dinâmicas associado a um grupo de colunas  
  
1.  Na superfície de design, clique em qualquer lugar na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Colunas exibe os membros estáticos e dinâmicos hierárquicos da hierarquia de grupos de colunas.  
  
3.  Clique no membro estático que corresponde à coluna estática que você deseja manter com as colunas de grupo. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
4.  No painel Propriedades, clique em **KeepWithGroup**e, em seguida, escolha um dos valores seguintes da lista suspensa:  
  
    -   **Nenhum** Selecione essa opção para não indicar nenhuma preferência para manter esse membro com os membros do grupo de colunas selecionado.  
  
    -   **Antes de** Selecione essa opção para manter esse membro com os membros do grupo anterior. Você pode usar isso para rótulos de coluna exibidos antes dos membros de grupo de coluna especificados.  
  
    -   **Depois de** Selecione essa opção para manter esse membro com os membros do grupo seguinte. Você pode usar isso para totais de coluna exibidos depois dos membros de grupo de coluna especificados.  
  
5.  (Opcional) Visualize o relatório. Sempre que possível, o processador de relatório manterá esse membro com os membros de grupo de colunas especificados.  
  
## <a name="see-also"></a>Consulte também  
 [Colunas, linhas e células da região de dados Tablix &#40;construtor de relatórios&#41; e o SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [Áreas da região de dados Tablix &#40;relatórios e SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
