---
title: "Definir uma mensagem Nenhum Dado para uma regi&#227;o de dados (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Definir uma mensagem Nenhum Dado para uma regi&#227;o de dados (Construtor de Relat&#243;rios e SSRS)
  Quando quiser especificar o texto que será exibido no relatório renderizado em vez de uma região de dados sem dados, defina a propriedade NoRowsMessage para uma tabela, matriz ou região de dados de lista, NoDataMessage para uma região de dados do gráfico e NoDataText para a escala de cores de um mapa. No tempo de execução, o processador do relatório executa a consulta para cada conjunto de dados em um relatório e a consulta do conjunto de dados pode não produzir nenhum conjunto de resultados. Em uma região de dados associada a um conjunto de dados vazio, você pode especificar o texto que deseja exibir em vez de exibir uma região de dados vazia. Também é possível definir a propriedade NoRowsMessage para um sub-relatório quando nenhum conjunto de dados no sub-relatório tiver dados no tempo de execução.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para definir a propriedade NoRowsMessage para uma tabela, matriz ou lista  
  
1.  No modo Design, clique na região de dados de tabela, matriz ou lista ou no sub-relatório na superfície de design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, digite o texto que você deseja exibir como uma mensagem no campo da propriedade **NoRowsMessage**.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### Para definir a propriedade NoDataMessage para um gráfico  
  
1.  Na exibição Design, clique no gráfico na superfície do design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, expanda o nó de **NoDataMessage**.  
  
3.  Em **Legenda**, digite o texto que você deseja exibir como uma mensagem no campo da propriedade **NoDataMessage**.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### Para definir NoRowsMessage para um sub-relatório  
  
1.  Na exibição Design, clique no sub-relatório na superfície do design para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, digite o texto que você deseja exibir como uma mensagem no campo da propriedade **NoRowsMessage**.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
### Para definir a propriedade NoDataText para uma escala de cores para um mapa  
  
1.  Na exibição Design, clique na escala de cores no mapa para selecioná-lo. O painel Propriedades exibe as propriedades do item selecionado.  
  
2.  No painel Propriedades, em **NoDataText**, digite o texto que você deseja exibir como um rótulo para cores sem nenhum valor de dados.  
  
     Como alternativa, na lista suspensa, clique em **Expressão** para abrir a caixa de diálogo **Expressão** e criar uma expressão.  
  
## Consulte também  
 [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)  
  
  