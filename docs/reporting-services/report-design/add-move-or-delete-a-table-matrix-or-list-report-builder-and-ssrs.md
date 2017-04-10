---
title: "Adicionar, mover ou excluir uma tabela, matriz ou lista (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Adicionar, mover ou excluir uma tabela, matriz ou lista (Construtor de Relat&#243;rios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], uma região de dados exibe dados de um conjunto de dados de relatório em um relatório. As regiões de dados incluem tabela, matriz, gráfico e medidor. Para aninhar uma região de dados dentro de outra, adicione cada uma separadamente e arraste a região de dados filho para a região de dados pai.  
  
 A maneira mais simples de adicionar uma região de dados de tabela ou matriz a seu relatório é executar o Assistente de Nova Tabela ou Nova Matriz. Esses assistentes o orientarão pelo processo de escolher uma conexão com uma fonte de dados, organizar campos e escolher o layout e o estilo. Os assistentes só estão disponíveis no Construtor de Relatórios.  
  
## Para adicionar uma tabela ou matriz a um relatório usando o Assistente de Nova Tabela ou Nova Matriz  
  
1.  Na guia **Inserir**, clique em **Tabela** ou **Matriz** e clique em **Assistente de Tabela** ou **Assistente de Matriz**.  
  
2.  Siga as etapas no assistente de **Nova Tabela** ou **Nova Matriz**.  
  
3.  Na guia **Página Inicial**, clique em **Executar** para visualizar o relatório renderizado.  
  
4.  Na guia **Executar**, clique em **Design** para continuar trabalhando no relatório.  
  
## Para adicionar uma região de dados  
  
1.  Na **Faixa de Opções**, no grupo **Regiões de Dados**, clique na região de dados que será adicionada.  
  
2.  Clique na superfície de design e a arraste para criar uma caixa com o tamanho desejado da região de dados.  
  
3.  Arraste um campo do conjunto de dados do relatório do painel de dados do relatório para a célula da região de dados. A região de dados agora está associada aos dados de um conjunto de dados do relatório.  
  
## Para selecionar uma região de dados  
  
-   Para uma região de dados de tablix, clique com o botão direito na alça de canto. Em uma região de dados de gráfico ou medidor, clique na região de dados.  
  
     Uma alça de seleção e oito alças de redimensionamento são exibidas.  
  
     Para regiões de dados aninhadas, clique com o botão direito do mouse na região de dados aninhada, clique em **Selecionar** e, em seguida, selecione o item de relatório desejado. Para verificar qual item de relatório está selecionado, use o painel Propriedades. O nome do item selecionado na superfície de design aparece na barra de ferramentas do painel Propriedades.  
  
## Para mover uma região de dados  
  
-   Para mover uma região de dados, clique na alça de seleção da região de dados e arraste-a. Use linhas ajustadas para alinhá-las aos itens de relatório existentes.  
  
     Se a régua não estiver visível, clique na guia Exibir e selecione a opção **Régua**.  
  
     Como alternativa, use as teclas de seta para mover a região de dados selecionada na superfície de design.  
  
## Para excluir uma região de dados  
  
-   Selecione a região de dados, clique nela com o botão direito do mouse e, em seguida, clique em **Excluir**.  
  
## Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  