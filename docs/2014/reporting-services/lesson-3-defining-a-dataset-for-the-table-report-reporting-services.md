---
title: 'Lição 3: Definindo um conjunto de dados para o relatório de tabela (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4c78328e02215520b8d33213e01871f010f62d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108455"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lição 3: Definindo um conjunto de dados para o relatório de tabela (Reporting Services)
  Depois de definir a fonte de dados, é necessário definir um conjunto de dados. No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], os dados usados em relatórios são contidos em um *conjunto de dados*. Um conjunto de dados inclui um ponteiro para uma fonte de dados e uma consulta a ser usada pelo relatório, bem como variáveis e campos calculados.  
  
 Você pode usar o designer de consulta em Designer de Relatórios para criar a consulta. Para este tutorial, você criará uma consulta que recupera informações de pedidos de vendas [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]do banco de dados **2008** .  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Para definir uma consulta Transact-SQL a fim de obter dados de relatório  
  
1.  No painel **dados do relatório** , clique em **novo**e, em seguida, clique em **DataSet...**. A caixa de diálogo **Propriedades do conjunto** de os é aberta.  
  
2.  Na caixa **Nome** , digite **AdventureWorksDataset**.  
  
3.  Clique em **Usar um conjunto de dados inserido no meu relatório**.  
  
4.  Verifique se o nome da fonte de dados, AdventureWorks2012, está na caixa de texto **fonte de dados** e se o **tipo de consulta** é **texto**.  
  
5.  Digite, ou copie e cole, a consulta Transact-SQL a seguir na caixa **Consulta** .  
  
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
  
6.  (Opcional) Clique no botão **Designer de Consultas** . A consulta é exibida no designer de consulta baseado em texto. Você pode ativar/desativar o designer de consultas gráficas clicando em **Editar Como Texto**. Exiba os resultados da consulta clicando no botão executar **(!)** na barra de ferramentas do designer de consulta.  
  
     É possível ver os dados em seis campos de quatro tabelas diferentes no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . A consulta utiliza a funcionalidade Transact-SQL como aliases. Por exemplo, a tabela SalesOrderHeader é chamada de soh.  
  
     Clique em **OK** para sair do designer de consultas.  
  
7.  Clique em **OK** para sair da caixa de diálogo **Propriedades Conjunto de Dados** .  
  
     O conjunto de dados **AdventureWorksDataset** e os campos são exibidos no painel Dados do Relatório.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você especificou uma consulta que recupera dados para o relatório com êxito. A seguir, você criará o layout de relatório. Consulte [Lição 4: Adicionando uma tabela ao relatório &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de design de consulta no Report Designer SQL Server Data Tools &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [SQL Server tipo de conexão &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [Tutorial: Gravando instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
