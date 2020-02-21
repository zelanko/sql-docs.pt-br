---
title: 'Lição 3: definir um conjunto de dados para o relatório de tabela | Microsoft Docs'
description: Depois de definir a fonte de dados para o relatório paginado, é necessário definir um conjunto de dados. No SQL Server Reporting Services, os dados usados em relatórios são mantidos em um conjunto de dados.
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25c62e0cd615748a764937d6dc2b8e4c952e59a1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244314"
---
# <a name="lesson-3-define-a-dataset-for-the-table-report---sql-server-reporting-services"></a>Lição 3: Definir um conjunto de dados para o relatório de tabela – SQL Server Reporting Services

Depois de definir a fonte de dados para o relatório paginado, é necessário definir um conjunto de dados. No [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)], os dados usados em relatórios são contidos em um *conjunto de dados*. Um conjunto de dados inclui um ponteiro para uma fonte de dados e uma consulta a ser usada pelo relatório, variáveis e campos calculados.

Use o Designer de Consultas no Designer de Relatórios para criar o conjunto de dados. Para este tutorial, você criará uma consulta que recupera informações de pedido de vendas do banco de dados AdventureWorks2016.

## <a name="define-a-transact-sql-query-for-report-data"></a>Definir uma consulta Transact-SQL a fim de obter dados de relatório  

1. No painel **Dados do Relatório**, selecione **Nova** > **Conjunto de Dados...** . A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta exibindo a seção **Consulta**.

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. Na caixa de texto **Nome**, digite "AdventureWorksDataset".

3. Abaixo disso, selecione o botão de opção **Usar um conjunto de dados inserido no meu relatório**.

4. Na caixa suspensa **Fonte de dados**, selecione AdventureWorks2016.

5. Como **Tipo de consulta**, selecione o botão de opção **Texto**.

6. Digite, ou copie e cole, a consulta Transact-SQL a seguir na caixa de texto **Consulta**.

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (Opcional) Selecione o botão **Designer de Consultas**. A consulta é exibida no *Designer de Consultas* baseado em texto. Para conferir os resultados da consulta, selecione o botão ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png) **executar** na barra de ferramentas **Designer de Consultas**. O conjunto de dados exibido contém seis campos de quatro tabelas no banco de dados AdventureWorks2016. A consulta utiliza a funcionalidade Transact-SQL como aliases. Por exemplo, a tabela SalesOrderHeader é chamada *soh*.

8. Selecione **OK** para sair do **Designer de Consultas**.

9. Selecione **OK** para sair da caixa de diálogo **Propriedades do Conjunto de Dados**.

O painel **Dados do Relatório** exibe os campos e o conjunto de dados AdventureWorksDataset.

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>Próximas etapas

Você especificou com êxito uma consulta que recupera dados para o relatório. A seguir, você criará o layout do relatório. Continue com a [Lição 4: Adicionar uma tabela ao relatório &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).

## <a name="see-also"></a>Confira também

[Ferramentas do Design de Consultas &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[Tipo de Conexão do SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
