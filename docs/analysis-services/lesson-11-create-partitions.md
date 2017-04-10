---
title: "Li&#231;&#227;o 11: Criar parti&#231;&#245;es | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 11: Criar parti&#231;&#245;es
Nesta lição, você criará partições para dividir a tabela Internet Sales em partes lógicas menores que podem ser processadas (Atualizadas) independentemente de outras partições. Por padrão, cada tabela que você inclui no modelo tem uma partição que contém todas as colunas e linhas da tabela. No caso da tabela Internet Sales, desejamos dividir os dados por ano; uma partição para cada um dos cinco anos da tabela.  Cada partição pode ser processada independentemente. Para obter mais informações, consulte [Partições &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 10: Criar hierarquias](../analysis-services/lesson-10-create-hierarchies.md).  
  
## Criar partições  
  
#### Para criar partições na tabela Internet Sales  
  
1.  No designer de modelos, clique na tabela **Internet Sales**, clique no menu **Tabela** e em **Partições**.  
  
    A caixa de diálogo **Gerenciador de Partições** é aberta.  
  
2.  Na caixa de diálogo **Gerenciador de Partições**, na lista de partições, clique na partição **Internet Sales**.  
  
3.  Em **Nome da Partição**, altere o nome para **Internet Sales 2010**.  
  
    > [!TIP]  
    > Antes de passar para a próxima etapa, observe que os nomes de coluna na janela Visualização de Tabela exibem essas colunas incluídas na tabela de modelo (marcada) com os nomes de coluna da origem. Isso acontece porque a janela Visualização de Tabela exibe colunas da tabela de origem, e não da tabela de modelo.  
  
4.  Selecione o botão **Editor de Consultas** logo acima do lado direito da janela de visualização.  
  
    Como você deseja que a partição inclua apenas essas linhas em um certo período, você deve incluir uma cláusula WHERE. Você só pode criar uma cláusula WHERE usando uma Instrução SQL.  
  
5.  No campo **Instrução SQL**, substitua a instrução existente colando a seguinte instrução:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Essa instrução especifica que a partição deve incluir todos os dados nas linhas em que OrderDate se refere ao ano civil 2010, conforme especificado na cláusula WHERE.  
  
6.  Clique em **Validar**.  
  
  
#### Para criar uma partição para o ano 2011  
  
1.  Na lista de partições, clique na partição **Vendas pela Internet de 2010** que você acabou de criar e em **Copiar**.  
  
2.  Em **Nome da Partição**, digite **Vendas pela Internet de 2011**.  
  
3.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2011, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### Para criar uma partição para o ano 2012  
  
1.  Na caixa de diálogo **Gerenciador de Partições**, clique em **Copiar**.  
  
2.  Em **Nome da Partição**, digite **Vendas pela Internet de 2012**.  
  
3.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2012, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### Para criar uma partição para o ano 2013  
  
1.  Na caixa de diálogo **Gerenciador de Partições**, clique em **Novo**.  
  
2.  Em **Nome da Partição**, digite **Vendas pela Internet de 2013**.  
  
3.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2013, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### Para criar uma partição para o ano 2014 na tabela Internet Sales  
  
1.  Na caixa de diálogo **Gerenciador de Partições**, clique em **Novo**.  
  
2.  Em **Nome da Partição**, digite **Vendas pela Internet de 2014**.  
  
3.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2014, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## Processar partições  
Na caixa de diálogo **Gerenciador de Partições**, observe o asterisco (**\***) ao lado dos nomes de partição de cada nova partição que você acabou de criar. Isso indica que a partição não foi processada (atualizada). Quando você cria novas partições, deve executar a operação Processar Partições ou Processar Tabela para atualizar os dados nessas partições.  
  
#### Para processar partições Internet Sales  
  
1.  Clique em **OK** para fechar a caixa de diálogo **Gerenciador de Partições**.  
  
2.  No designer de modelos, clique na tabela **Internet Sales**, clique no menu **Modelo**, aponte para **Processar** (Atualizar) e clique em **Processar Partições**.  
  
3.  Na caixa de diálogo **Processar Partições**, verifique se o **Modo** está definido como **Processo Padrão**.  
  
4.  Marque a caixa de seleção na coluna **Processar** para cada uma das cinco partições criadas e clique em **OK**.  
  
    Se você for solicitado a fornecer credenciais de Representação, insira o nome de usuário e a senha do Windows que especificou na Lição 2, etapa 6.  
  
    A caixa de diálogo **Processamento de Dados** será exibida, mostrando os detalhes do processo de cada partição. Observe que um número diferente de linhas para cada partição é transferido. Isso acontece porque cada partição inclui somente as linhas referentes ao ano especificado na cláusula WHERE da Instrução SQL: Quando o processamento for concluído, vá em frente e feche a caixa de diálogo Processamento de Dados.  
  
  
  
## Próximas etapas  
Para continuar este tutorial, vá para a próxima lição: [Lição 12: Criar funções](../analysis-services/lesson-12-create-roles.md).  
  
  
  
