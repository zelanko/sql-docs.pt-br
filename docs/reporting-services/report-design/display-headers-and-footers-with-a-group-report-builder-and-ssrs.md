---
title: "Exibir cabe&#231;alhos e rodap&#233;s com um grupo (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Exibir cabe&#231;alhos e rodap&#233;s com um grupo (Construtor de Relat&#243;rios e SSRS)
  Você pode ajudar a controlar se uma linha estática, como um cabeçalho ou rodapé de grupo, será renderizada com linhas dinâmicas associadas a um grupo de uma região de dados tablix.  
  
 Para repetir todos os títulos de linha ou coluna em várias páginas, você pode definir as propriedades da região de dados tablix. Para obter informações, consulte [Exibir cabeçalhos de linhas e colunas em várias páginas (Construtor de Relatórios e SSRS)](https://msdn.microsoft.com/library/dd207045.aspx).  
  
 Para controlar o comportamento de renderização de linhas e colunas dinâmicas associadas a grupos aninhados ou de linhas e colunas estáticas associadas a rótulos ou subtotais, você deve definir as propriedades do membro tablix. Um membro tablix representa uma linha ou coluna estática ou dinâmica. Um membro estático ocorre uma vez. Por exemplo, uma linha de total geral é uma linha estática. Um membro dinâmico ocorre uma vez para cada instância do grupo. Por exemplo, uma linha associada a um grupo com a expressão de grupo [Território] ocorre uma vez para cada valor exclusivo de território. Para obter mais informações sobre os membros do tablix, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Você pode definir um membro tablix no painel Agrupamento e as propriedades **KeepWithGroup**, **KeepTogether** e **RepeatOnNewPage** no painel Propriedades. Use **KeepWithGroup** para ajudar a exibir cabeçalhos de grupo e rodapés na mesma página como o grupo. Use **KeepTogether** para ajudar a exibir os membros estáticos com as linhas ou colunas de um grupo. Use **RepeatOnNewPage** para repetir o cabeçalho de grupo ou rodapé em toda página que exibe uma instância completa do membro de grupo de linhas designado pelo valor **KeepWithGroup**. **RepeatOnNewPage** não tem suporte para membros de grupo de colunas.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether** e **RepeatOnNewPage** são propriedades do membro de grupo que você pode definir usando o **Modo Avançado** do painel Agrupamento. Para obter mais informações, consulte [Painel Agrupamento &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para manter uma linha estática com um conjunto de linhas dinâmicas associado a um grupo de linhas  
  
1.  Na superfície de design, clique em qualquer lugar na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Linhas exibe os membros estáticos e dinâmicos hierárquicos da hierarquia de grupos de linhas.  
  
3.  Clique no membro estático que corresponde ao cabeçalho ou rodapé de linha que você deseja manter com as linhas do grupo. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
4.  No painel Propriedades, clique em **KeepWithGroup** e, em seguida, escolha um dos valores seguintes da lista suspensa:  
  
    -   **Nenhum** Selecione essa opção para não indicar nenhuma preferência para manter esse membro com os membros do grupo de linhas selecionado.  
  
    -   **Antes de** Selecione essa opção para manter esse membro com os membros do grupo anterior. Você pode usar isso para linhas de rodapé de grupo.  
  
    -   **Depois de** Selecione essa opção para manter esse membro com os membros do grupo seguinte. Você pode usar isso para linhas de cabeçalho de grupo.  
  
5.  (Opcional) Visualize o relatório. Sempre que possível, o processador de relatório manterá esse membro com os membros de grupo de linhas especificados.  
  
### Para manter uma coluna estática com um conjunto de colunas dinâmicas associado a um grupo de colunas  
  
1.  Na superfície de design, clique em qualquer lugar na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados.  
  
2.  À direita lado do painel Agrupamento, clique na seta para baixo e, em seguida, clique em **Modo Avançado**. O painel Grupos de Colunas exibe os membros estáticos e dinâmicos hierárquicos da hierarquia de grupos de colunas.  
  
3.  Clique no membro estático que corresponde à coluna estática que você deseja manter com as colunas de grupo. O painel Propriedades exibe as propriedades de **Membro de Tablix** .  
  
4.  No painel Propriedades, clique em **KeepWithGroup** e, em seguida, escolha um dos valores seguintes da lista suspensa:  
  
    -   **Nenhum** Selecione essa opção para não indicar nenhuma preferência para manter esse membro com os membros do grupo de colunas selecionado.  
  
    -   **Antes de** Selecione essa opção para manter esse membro com os membros do grupo anterior. Você pode usar isso para rótulos de coluna exibidos antes dos membros de grupo de coluna especificados.  
  
    -   **Depois de** Selecione essa opção para manter esse membro com os membros do grupo seguinte. Você pode usar isso para totais de coluna exibidos depois dos membros de grupo de coluna especificados.  
  
5.  (Opcional) Visualize o relatório. Sempre que possível, o processador de relatório manterá esse membro com os membros de grupo de colunas especificados.  
  
## Consulte também  
 [Células, linhas e colunas da região de dados Tablix (Construtor de Relatórios) e SSRS](https://msdn.microsoft.com/library/dd220587.aspx)   
 
  
  