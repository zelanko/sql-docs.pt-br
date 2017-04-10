---
title: "Alterar a altura da linha ou a largura da coluna (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Alterar a altura da linha ou a largura da coluna (Construtor de Relat&#243;rios e SSRS)
  Quando você define a altura de uma linha, você está especificando a altura máxima da linha no relatório renderizado. No entanto, por padrão, as caixas de texto na linha são definidas para crescer na vertical para acomodar seus dados em tempo de execução e isso pode fazer com que uma linha seja expandida além da altura especificada. Para definir uma altura de linha fixa, você deve alterar as propriedades da caixa de texto para que elas não se expandam automaticamente.  
  
 Quando você define a largura de coluna, você está especificando a largura máxima da coluna no relatório renderizado. As colunas não se ajustam automaticamente na horizontal para acomodar o texto.  
  
 Se uma célula em uma linha ou coluna contém um retângulo ou uma região de dados, a altura e largura mínimas da célula são determinadas pela altura e largura do item contido. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para alterar a altura da linha movendo os indicadores de linha  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da linha que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da linha e movê-la para cima ou para baixo para ajustar a altura da linha.  
  
### Para alterar a altura da linha definindo as propriedades de célula  
  
1.  Na exibição Design, clique em uma célula na linha da tabela.  
  
     ![Célula selecionada em uma tabela](../../reporting-services/report-design/media/table-selectcell.png "Célula selecionada em uma tabela")  
  
2.  No painel **Propriedades** exibido, modifique a propriedade **Altura**, e clique em qualquer lugar fora do painel **Propriedades**.  
  
     ![Painel de propriedades para células de tabela selecionadas](../../reporting-services/report-design/media/cell-propertiespane.png "Painel de propriedades para células de tabela selecionadas")  
  
### Para impedir que uma linha se expanda automaticamente na vertical  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de linha cinzas são exibidas na borda externa dessa região.  
  
2.  Clique na alça da linha para selecioná-la.  
  
3.  No painel Propriedades, defina CanGrow como **False**.  
  
    > [!NOTE]  
    >  Se você não puder ver o painel Propriedades, no menu **Exibir**, clique em **Propriedades**.  
  
### Para alterar a largura da coluna  
  
1.  No modo Design, clique em qualquer parte da região de dados tablix para selecioná-la. As alças de coluna cinzas são exibidas na borda externa dessa região.  
  
2.  Focalize a borda da alça da coluna que deseja expandir. Será exibida uma seta com duas pontas.  
  
3.  Clique para prender a borda da coluna e movê-la para a esquerda ou direita para ajustar a largura da coluna.  
  
## Consulte também  
 [Região de dados Tablix (Construtor de Relatórios e SSRS)](https://msdn.microsoft.com/library/dd220587.aspx)   
 [Células, linhas e colunas da região de dados Tablix (Construtor de Relatórios) e SSRS](https://msdn.microsoft.com/library/dd220511.aspx)   
 [Tabelas (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes (Construtor de Relatórios e SSRS)](https://msdn.microsoft.com/library/dd207149.aspx)   
 [Listas (Construtor de Relatórios e SSRS)](https://msdn.microsoft.com/library/dd239330.aspx)   
 [Tabelas, matrizes e listas (Construtor de Relatórios e SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  