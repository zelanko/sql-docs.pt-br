---
title: 'Lição 2: Modificando as propriedades de fonte de dados de relatório | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e2a729c844d88ffb11b5de3622868fc9bc2eee17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159616"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
  Nesta lição, você usará o Gerenciador de Relatórios para selecionar um relatório que será entregue a destinatários. A assinatura controlada por dados que será definida distribuirá o relatório **Pedidos de Vendas** criado no tutorial [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md). Nas etapas a seguir, você modificará as informações da conexão de fonte de dados usadas pelo relatório para obter dados. Somente relatórios que usam **credenciais armazenadas** para acessar uma fonte de dados de relatório podem ser distribuídos por uma assinatura controlada por dados. Credenciais armazenadas são necessárias para o processamento de relatório autônomo.  
  
 Você também modificará o conjunto de dados e relatório para usar um parâmetro para filtrar o relatório no `[Order]` para que a assinatura possa produzir instâncias diferentes do relatório para pedidos específicos e formatos de renderização.  
  
 **Neste tópico:**  
  
-   [Para modificar as propriedades de fonte de dados](#bkmk_modify_datasource)  
  
-   [Para modificar o AdventureWorksDataset](#bkmk_modify_dataset)  
  
-   [Para adicionar um parâmetro de relatório e republicar o relatório](#bkmk_add_reportparameter)  
  
-   [Para implantar o relatório novamente](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> Para modificar as propriedades de fonte de dados  
  
1.  Inicie [Gerenciador de relatórios &#40;modo nativo do SSRS&#41; ](../../2014/reporting-services/report-manager-ssrs-native-mode.md) com privilégios de administrador, por exemplo, clique com botão direito no ícone do Internet Explorer e clique em **executar como administrador**.  
  
2.  Navegue até a pasta que contém o relatório **Pedidos de Vendas** e, no menu de contexto do relatório, clique em **Gerenciar**.  
  
     ![Abra o menu de contexto do relatório e selecione Gerenciar](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "abrir o menu de contexto do relatório e selecionar gerenciar")  
  
3.  Clique na guia **Fontes de Dados** .  
  
4.  Para **Tipo de conexão**, selecione **Microsoft SQL Server**.  
  
5.  A cadeia de conexão da fonte de dados personalizada será a seguinte e presumirá que o banco de dados de exemplo esteja em um servidor de banco de dados local:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  Clique em **Credenciais armazenadas com segurança no servidor de relatórios**.  
  
7.  Digite seu nome de usuário (use o formato *domain\user*) e a senha. Se você não tiver permissão para acessar o [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] de banco de dados, especifique um logon que tenha.  
  
8.  Clique em **Usar as credenciais do Windows ao conectar-se à fonte de dados**e depois clique em **OK**. Se você não estiver usando uma conta de domínio (por exemplo, se você estiver usando um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] logon), não clique essa caixa de seleção.  
  
9. Clique em **Testar Conexão** para verificar se é possível conectar-se à fonte de dados.  
  
10. Clique em **Aplicar**.  
  
11. Exiba o relatório para verificar se o relatório está sendo executado com as credenciais especificadas. Para exibir o relatório, clique na guia **Exibir** . Observe que, quando o relatório é aberto, você deve selecionar um nome de funcionário e, em seguida, clique no **Exibir relatório** botão para exibir o relatório.  
  
##  <a name="bkmk_modify_dataset"></a> Para modificar o AdventureWorksDataset  
  
1.  Abra o relatório pedidos de vendas no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  Clique com o botão direito do mouse no conjunto de dados `AdventureWorksDataset` e clique em **Propriedades do Conjunto de Dados**.  
  
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
  
##  <a name="bkmk_add_reportparameter"></a> Para adicionar um parâmetro de relatório e republicar o relatório  
  
1.  No painel **Dados do Relatório** , clique em **Novo** e em **Parâmetro...**  
  
2.  Em **Nome**, digite `OrderNumber`.  
  
3.  Em **Aviso**, digite `OrderNumber`.  
  
4.  Selecione **Permitir valor em branco ("")**.  
  
5.  Selecione **Permitir valor nulo**.  
  
6.  Clique em **OK**. O parâmetro será adicionado ao **Painel Dados do Relatório** e ele se parecerá com a seguinte imagem:  
  
     ![O novo parâmetro é adicionado ao painel dados do relatório](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "o novo parâmetro é adicionado ao painel dados do relatório")  
  
7.  Clique na guia **Visualização** para executar o relatório. Observe a caixa de entrada de parâmetro na parte superior do relatório. Você pode:  
  
    -   Clicar em Exibir Relatório para ver o relatório completo sem usar um parâmetro.  
  
    -   Cancelar a seleção da opção Nula e digitar um número de pedido, por exemplo so71949 para exibir somente este pedido no relatório.  
  
         ![Visualizador de relatórios com área de parâmetro visível](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "Visualizador de relatórios com área de parâmetro visível")  
  
8.  Reimplantar o relatório para que a configuração de assinatura na próxima lição possa utilizar as alterações que você fez nesta lição. Para obter mais informações sobre as propriedades de projeto usadas no tutorial de tabela, consulte a seção “Para publicar o relatório no Servidor de Relatório (opcional)” da [Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
##  <a name="bkmk_redeploy"></a> Para implantar o relatório novamente  
  
1.  Reimplantar o relatório para que a configuração de assinatura na próxima lição possa utilizar as alterações que você fez nesta lição. Para obter mais informações sobre as propriedades de projeto usadas no tutorial de tabela, consulte a seção “Para publicar o relatório no Servidor de Relatório (opcional)” da [Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  Na barra de ferramentas, clique em **Compilar** e, em seguida, em **Implantar tutorial**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você configurou o relatório com êxito para obter dados usando credenciais armazenadas. Depois, especifique a assinatura usando as páginas de Assinatura Controlada por Dados no Gerenciador de Relatórios. Consulte [Lição 3: Definindo uma assinatura controlada por dados](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar fontes de dados de relatório](report-data/manage-report-data-sources.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
