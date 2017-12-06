---
title: "Lição 3: Definindo um conjunto de dados para o relatório de tabela (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
caps.latest.revision: "53"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: c610c2cba4f004a35d1d90aceb9288b995587c74
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lição 3: Definindo um conjunto de dados para o relatório de tabela (Reporting Services)
Depois de definir a fonte de dados, é necessário definir um conjunto de dados. No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], os dados usados em relatórios são contidos em um *conjunto de dados*. Um conjunto de dados inclui um ponteiro para uma fonte de dados e uma consulta a ser usada pelo relatório, bem como variáveis e campos calculados.  
  
Use o designer de consultas no Designer de Relatórios para criar o conjunto de dados. Para este tutorial, você criará uma consulta que recupera informações de pedido de vendas do banco de dados [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] .  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Para definir uma consulta Transact-SQL a fim de obter dados de relatório  
  
1.  No painel **Dados do Relatório** , clique em **Novo**e em **Conjunto de Dados...**. A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta.  
  
2.  Na caixa **Nome** , digite **AdventureWorksDataset**.  
  
3.  Clique em **Usar um conjunto de dados inserido em meu relatório**.  
  
4.  Escolha a fonte de dados que você criou na lição anterior, [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)].   
5. Selecione **Texto** em **Tipo de Consulta**.  
  
6.  Digite, ou copie e cole, a consulta Transact-SQL a seguir na caixa **Consulta** .  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
7.  (Opcional) Clique no botão **Designer de Consultas** . A consulta é exibida no designer de consulta baseado em texto. Você pode ativar/desativar o designer de consultas gráficas clicando em **Editar Como Texto**. Veja os resultados da consulta clicando no botão Executar ![ssrs_querydesigner_run](../reporting-services/media/ssrs-querydesigner-run.png)  na barra de ferramentas do designer de consultas.  
  
    É possível ver os dados em seis campos de quatro tabelas diferentes no banco de dados [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . A consulta utiliza a funcionalidade Transact-SQL como aliases. Por exemplo, a tabela SalesOrderHeader é chamada *soh*.  
  
8.  Clique em **OK** para sair do designer de consultas.  
  
9.  Clique em **OK** para sair da caixa de diálogo **Propriedades Conjunto de Dados** .  
  
    O conjunto de dados **AdventureWorksDataset** e os campos são exibidos no painel Dados do Relatório.  
    ![ssrs_adventureworksdataset](../reporting-services/media/ssrs-adventureworksdataset.png)  
  
## <a name="next-task"></a>Próxima tarefa  
Você especificou uma consulta que recupera dados para o relatório com êxito. A seguir, você criará o layout de relatório. Consulte [Lição 4: Adicionando uma tabela ao relatório &#40;Reporting Services&#41;](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
[Ferramentas de Design da Consulta &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)  
[O tipo de conexão do SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)  
[Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
  

