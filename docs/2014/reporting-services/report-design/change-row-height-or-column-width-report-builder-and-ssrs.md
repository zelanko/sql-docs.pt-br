---
title: Alterar a altura da linha ou a largura da coluna (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 56d77bdcfe43fd793cf81a91bad007cc300eb7ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227036"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Alterar a altura da linha ou a largura da coluna (Construtor de Relatórios e SSRS)
  Quando você define a altura de uma linha, você está especificando a altura máxima da linha no relatório renderizado. No entanto, por padrão, as caixas de texto na linha são definidas para crescer na vertical para acomodar seus dados em tempo de execução e isso pode fazer com que uma linha seja expandida além da altura especificada. Para definir uma altura de linha fixa, você deve alterar as propriedades da caixa de texto para que elas não se expandam automaticamente.  
  
 Quando você define a largura de coluna, você está especificando a largura máxima da coluna no relatório renderizado. As colunas não se ajustam automaticamente na horizontal para acomodar o texto.  
  
 Se uma célula em uma linha ou coluna contém um retângulo ou uma região de dados, a altura e largura mínimas da célula são determinadas pela altura e largura do item contido. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>Para alterar a altura da linha movendo os indicadores de linha  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da linha que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da linha e movê-la para cima ou para baixo para ajustar a altura da linha.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>Para alterar a altura da linha definindo as propriedades de célula  
  
1.  Na exibição Design, clique em uma célula na linha da tabela.  
  
     ![Célula selecionada em uma tabela](../media/table-selectcell.png "Célula selecionada em uma tabela")  
  
2.  No painel **Propriedades** exibido, modifique a propriedade **Altura** , e clique em qualquer lugar fora do painel **Propriedades** .  
  
     ![Painel de propriedades da célula da tabela selecionada](../media/cell-propertiespane.png "Painel de propriedades da célula da tabela selecionada")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>Para impedir que uma linha se expanda automaticamente na vertical  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Clique na alça da linha para selecioná-la.  
  
3.  No painel Propriedades, defina CanGrow como **False**.  
  
    > [!NOTE]  
    >  Se você não puder ver o painel Propriedades, no menu **Exibir** , clique em **Propriedades**.  
  
### <a name="to-change-column-width"></a>Para alterar a largura da coluna  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de coluna cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da coluna que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da coluna e movê-la para a esquerda ou direita para ajustar a largura da coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Colunas, linhas e células da região de dados Tablix &#40;construtor de relatórios&#41; e o SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
