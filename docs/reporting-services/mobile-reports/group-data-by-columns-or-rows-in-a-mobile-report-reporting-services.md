---
title: "Agrupar dados por colunas ou linhas em um relat&#243;rio m&#243;vel | Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
caps.latest.revision: 6
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Agrupar dados por colunas ou linhas em um relat&#243;rio m&#243;vel | Reporting Services
Você pode organizar os dados por colunas ou linhas em vários tipos de gráficos no [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]. Acompanhe esse passo a passo.

Nos gráficos de tempo, totais, de pizza e de funil, é possível organizar os dados por linhas ou colunas. 
* Organizar por colunas será útil se uma tabela tiver várias colunas de dados que você deseja comparar. 
* Organizar por linhas funciona melhor se uma coluna na tabela contém os nomes de diferentes categorias. 

As etapas a seguir usam uma tabela de totais de comparação com dados simulados em [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] para ilustrar a diferença entre a estrutura dos dados por linhas ou colunas em um gráfico.  

1. Arraste um **Gráfico de comparação de totais** da guia **Layout** para a superfície de design e aumentá-lo.

2. Selecione a guia **Dados**. Você verá que a tabela SimulatedTable contém uma série de colunas, **Metric1** a **Metric5** e **Comparison1** a **Comparison5**. 

   ![mobile-report-data-group-column](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. No painel **Propriedades de dados**, a **Série Principal** é **SimulatedTable**. Selecione a seta na caixa ao lado de **Série Principal** e você verá que **Metric1** a **Metric5** está selecionado.

   ![mobile-report-properties-columns](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   Da mesma forma para a **Série de Comparação** -- **Comparison1** a **Comparison5** são selecionados.
   
4. Selecione **Visualização**.

   ![mobile-report-chart-by-columns](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   Cada barra no gráfico representa uma coluna na tabela. As barras mais espessas são as colunas Métricas e as barras mais finas são as colunas de Comparação.

5. Clique na seta Voltar no canto superior esquerdo para sair do modo de visualização.

6. Na guia **Layout**, no painel **Propriedades visuais**, altere a **Estrutura de dados** de **Por colunas** para **Por linhas**.  

7. Selecione a guia **Dados**. Agora a tabela SimulatedTable tem uma coluna **Categoria** junto com as colunas **Métrica** e **Comparação**, com a categoria A a E. 

   ![mobile-report-data-group-rows](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  No painel **Propriedades de dados**, agora há uma caixa Coluna de Categoria, que lista a coluna Categoria de SimulatedTable. Na Série Principal, você pode escolher qual coluna deve ser usada para os valores. Por padrão, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] seleciona Metric1 a Metric5 para a Série Principal e Comparison1 a Comparison5 para a Série de Comparação. 

    ![mobile-report-properties-rows](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. Selecione **Visualização**.

   ![mobile-report-chart-by-rows](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   Agora cada barra no gráfico representa os valores para cada categoria na coluna Categoria.

### Consulte também
* [Visualizações nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)