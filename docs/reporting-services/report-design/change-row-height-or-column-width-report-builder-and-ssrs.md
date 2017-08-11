---
title: "Alterar a altura da linha ou a largura de coluna (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aef6ef0fe1f32f015abe3b48177f6e4d3e45648d
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Alterar a altura da linha ou a largura da coluna (Construtor de Relatórios e SSRS)
  Quando você define a altura de uma linha, você está especificando a altura máxima da linha no relatório renderizado. No entanto, por padrão, as caixas de texto na linha são definidas para crescer na vertical para acomodar seus dados em tempo de execução e isso pode fazer com que uma linha seja expandida além da altura especificada. Para definir uma altura de linha fixa, você deve alterar as propriedades da caixa de texto para que elas não se expandam automaticamente.  
  
 Quando você define a largura de coluna, você está especificando a largura máxima da coluna no relatório renderizado. As colunas não se ajustam automaticamente na horizontal para acomodar o texto.  
  
 Se uma célula em uma linha ou coluna contém um retângulo ou uma região de dados, a altura e largura mínimas da célula são determinadas pela altura e largura do item contido. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>Para alterar a altura da linha movendo os indicadores de linha  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da linha que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da linha e movê-la para cima ou para baixo para ajustar a altura da linha.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>Para alterar a altura da linha definindo as propriedades de célula  
  
1.  Na exibição Design, clique em uma célula na linha da tabela.  
  
     ![Selecionou a célula em uma tabela](../../reporting-services/report-design/media/table-selectcell.png "selecionado célula em uma tabela")  
  
2.  No painel **Propriedades** exibido, modifique a propriedade **Altura** , e clique em qualquer lugar fora do painel **Propriedades** .  
  
     ![Painel de propriedades de célula da tabela selecionada](../../reporting-services/report-design/media/cell-propertiespane.png "painel de propriedades de célula da tabela selecionada")  
  
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
 [Região de dados Tablix (Construtor de Relatórios e SSRS)](https://msdn.microsoft.com/library/dd220587.aspx)   
 [Células da região de dados Tablix, linhas e colunas (construtor de relatórios) e SSRS](https://msdn.microsoft.com/library/dd220511.aspx)   
 [Tabelas (construtor de relatórios e SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes (construtor de relatórios e SSRS)](https://msdn.microsoft.com/library/dd207149.aspx)   
 [Listas (construtor de relatórios e SSRS)](https://msdn.microsoft.com/library/dd239330.aspx)   
 [Tabelas, matrizes e listas (construtor de relatórios e SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
