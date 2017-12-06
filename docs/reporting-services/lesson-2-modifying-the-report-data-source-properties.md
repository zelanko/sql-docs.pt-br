---
title: "Lição 2: Modificando as propriedades de fonte de dados de relatório | Microsoft Docs"
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
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ba7880d9cc6f316b7ce06b73dda896becd892797
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
Nesta lição do tutorial do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] , você usa o portal da Web para selecionar um relatório que será entregue aos destinatários. A assinatura controlada por dados que será definida distribuirá o relatório **Pedidos de Vendas** criado no tutorial [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  Nas etapas a seguir, você modificará as informações da conexão de fonte de dados usadas pelo relatório para obter dados. Somente relatórios que usam **credenciais armazenadas** para acessar uma fonte de dados de relatório podem ser distribuídos por uma assinatura controlada por dados. Credenciais armazenadas são necessárias para o processamento de relatório autônomo.  
  
Você também modificará o conjunto de dados e relatório para usar um parâmetro para filtrar o relatório no `[Order]` para que a assinatura possa produzir instâncias diferentes do relatório para pedidos específicos e formatos de renderização.  
  
## <a name="bkmk_modify_datasource"></a>Para modificar a fonte de dados para usar credenciais armazenadas  
  
1.  Procure o portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] com privilégios de administrador, por exemplo, clique com o botão direito do mouse no ícone do Internet Explorer e clique em **Executar como administrador**.  
 
2.    Navegue até a URL do portal da Web.  Por exemplo:   
    `http://<server name>/reports`.  
    `http://localhost/reports`
 **Observação:** a URL do *portal* da Web é "Reports", não a URL do *Servidor* de Relatório "Reportserver".  
3.  Navegue até a pasta que contém o relatório **Pedidos de Vendas** e, no menu de contexto do relatório, clique em **Gerenciar**.  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  Clique em **Fontes de Dados** no painel esquerdo.  
  
4.  Verifique se o **Tipo de Conexão** é **Microsoft SQL Server**.  
  
5.  Verifique se a cadeia de conexão da fonte de dados personalizada é a seguinte e se ela presume que o banco de dados de exemplo está em um servidor de banco de dados local:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  Clique em **Usar as seguintes credenciais**.  
  
7. Em **Tipo de credenciais**, selecione **Nome de usuário do Windows e senha**
8. Digite seu nome de usuário (use o formato *domain\user*) e a senha. Se você não tiver permissão para acessar o banco de dados AdventureWorks2014, especifique um logon que tem essa permissão.  
    
9. Clique em **Testar Conexão** para verificar se é possível conectar-se à fonte de dados.  
  
10. Clique em **Salvar**.
11. Clique em **Cancelar**  
  
11. Exiba o relatório para verificar se o relatório está sendo executado com as credenciais especificadas. .  
  
## <a name="bkmk_modify_dataset"></a>Para modificar o AdventureWorksDataset  
 Nas etapas a seguir, você modificará o conjunto de dados para usar um parâmetro a fim de filtrar o conjunto de dados com base em um número de pedido.
1.  Abra o relatório **Pedidos de Vendas** no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  Clique com o botão direito do mouse no conjunto de dados `AdventureWorksDataset` e clique em **Propriedades do Conjunto de Dados**.  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  Adicione a instrução `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` antes da instrução `Group By` . A sintaxe da consulta completa é a seguinte:  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  Clique em **OK**.  
 Nas etapas a seguir, você adicionará um parâmetro ao relatório.  O parâmetro de relatório alimenta o parâmetro de conjunto de dados. 
## <a name="bkmk_add_reportparameter"></a>Para adicionar um parâmetro de relatório e republicar o relatório  
  
1.  No painel **Dados do Relatório** , expanda a pasta de parâmetros e clique duas vezes no parâmetro **Ordernumber** .  Ele foi criado automaticamente como parte das etapas anteriores, quando o parâmetro foi adicionado ao conjunto de dados. Clique em **Novo** e em **Parâmetro...**  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  Verifique se o **Nome** é `OrderNumber`.  
  
3.  Verifique se o **Prompt** é `OrderNumber`.  
  
4.  Selecione **Permitir valor em branco ("")**.  
  
5.  Selecione **Permitir valor nulo**.  
  
6.  Clique em **OK**.  
  
7.  Clique na guia **Visualizar** para executar o relatório. Observe a caixa de entrada de parâmetro na parte superior do relatório. Você pode:  
  
    -   Clicar em Exibir Relatório para ver o relatório completo sem usar um parâmetro.  
  
    -   Desmarque a opção **Null** e digite um número de pedido, por exemplo *so71949*, e clique em **Exibir Relatório** para exibir apenas uma pedido no relatório.  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>Implantar o relatório novamente  
  
1.  Reimplantar o relatório para que a configuração de assinatura na próxima lição possa utilizar as alterações que você fez nesta lição. Para obter mais informações sobre as propriedades de projeto usadas no tutorial de tabela, consulte a seção “Para publicar o relatório no Servidor de Relatório (opcional)” da [Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  Na barra de ferramentas, clique em **Compilar** e, em seguida, em **Implantar tutorial**.  
  
## <a name="next-steps"></a>Próximas etapas  
+ Você configurou o relatório com êxito para obter dados usando as credenciais armazenadas, e os dados podem ser filtrados com um parâmetro. 
+ Na próxima lição, você configura a assinatura usando as páginas Assinatura Controlada por Dados do portal da Web. Consulte [Lição 3: Definindo uma assinatura controlada por dados](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).  
  
## <a name="see-also"></a>Consulte também  
[Gerenciar fontes de dados de relatório](../reporting-services/report-data/manage-report-data-sources.md)  
[Especificar informações de credenciais e de conexão para fontes de dados de relatório](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

