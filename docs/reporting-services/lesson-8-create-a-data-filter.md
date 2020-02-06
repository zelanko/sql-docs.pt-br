---
title: 'Lição 8: Criar um filtro de dados | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 991610dacf7a13a467a3058f2bdbcfcc454ee71e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62512388"
---
# <a name="lesson-8-create-a-data-filter"></a>Lição 8: Criar um filtro de dados
Após adicionar uma ação de detalhamento no relatório pai, a próxima etapa é criar um filtro de dados para a tabela de dados definida para o relatório filho.  
  
Você pode criar um filtro baseado em tabela **ou** um filtro de consulta para o relatório de detalhamento. Esta lição fornece instruções para ambas as opções.  
  
## <a name="table-based-filter"></a>Filtro baseado em tabela  
É necessário concluir as seguintes tarefas para implementar um filtro baseado em tabela.  
  
-   Adicione uma expressão de filtro ao tablix no relatório filho.  
  
-   Criar uma função que seleciona dados não filtrados na tabela **PurchaseOrderDetail** .  
  
-   Adicionar um manipulador de eventos que associa a DataTable **PurchaseOrderDetail** ao relatório filho.  
  
### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>Para adicionar uma expressão de filtro ao tablix no relatório filho  
  
1.  Abra o relatório filho.  
  
2.  Selecione um título de coluna no tablix, clique com o botão direito do mouse na célula cinza exibida acima do título de coluna e selecione **Propriedades do Tablix**.  
  
3.  Selecione a página **filtros** e **Adicionar**.  
  
4.  No campo **Expressão** , clique em **ProductID** na lista suspensa. Esta é a coluna à qual você aplicará o filtro.  
  
5.  Clique no operador igual ( **=** ) na lista suspensa **Operador** .  
  
6.  Clique no botão de expressão ao lado do campo **Valor** , selecione **Parâmetros** na área **Categoria** e clique duas vezes em **productid** na área **Valores** . O campo **Definir expressão para: Valor** agora deve conter uma expressão semelhante a **=Parameters!productid.Value**.  
  
7.  Selecione **OK** e **OK** novamente na caixa de diálogo **Propriedades do Tablix** .  
  
8.  Salve o arquivo .rdlc.  
  
### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>Para criar uma função que seleciona dados não filtrados na tabela PurchaseOrdeDetail.  
  
1.  No Gerenciador de Soluções, expanda Default.aspx e clique duas vezes em Default.aspx.cs.  
  
2.  Crie uma nova função que aceita um parâmetro, **productid**, do tipo Inteiro, retorna um objeto **datatable** e faz o seguinte.  
  
    1.  Cria uma instância do conjunto de dados, **DataSet2**, criado na Etapa 2 da [Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Crie uma conexão com o banco de dados SQL Server para executar a consulta definida na **Lição 4: Definir uma conexão de dados e uma DataTable para o relatório filho**.  
  
    3.  A consulta deve retornará dados não filtrados.  
  
    4.  Preencha a instância do DataSet com os dados não filtrados executando a consulta.  
  
    5.  Retorna a DataTable **PurchaseOrderDetail** .  
  
        A função terá aparência similar à mostrada abaixo (Isso é apenas para fins de referência. Você pode seguir o padrão desejado para buscar os dados necessários ao relatório filho).  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>Para adicionar um manipulador de eventos que associe a DataTable PurchaseOrderDetail ao relatório filho.  
  
1.  Abra Default.aspx no modo designer.  
  
2.  Clique com o botão direito do mouse no controle ReportViewer e selecione **Propriedades**.  
  
3.  Na página **Propriedades** , selecione o ícone **Eventos** .  
  
4.  Clique duas vezes no evento **Detalhamento** .  
  
    Isso adicionará uma seção do manipulador de eventos ao código, que será semelhante ao bloco abaixo.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Conclua o manipulador de eventos. Ela deve incluir a funcionalidade a seguir.  
  
    1.  Busque a referência de objeto do relatório filho no parâmetro *DrillthroughEventArgs* .  
  
    2.  Chame a função **GetPurchaseOrderDetail**  
  
    3.  Associe a DataTable **PurchaseOrderDetail** à fonte de dados correspondente do relatório.  
  
        O código completo do manipulador de eventos será semelhante ao conteúdo seguinte.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salve o arquivo.  
  
## <a name="query-filter"></a>Filtro de consulta  
É necessário concluir as seguintes tarefas para implementar um filtro de consulta.  
  
-   Crie uma função que seleciona dados filtrados da tabela **PurchaseOrderDetail** .  
  
-   Adicione um manipulador de eventos que recupera valores de parâmetro e associa a DataTable **PurchaseOrdeDetail** ao relatório filho.  
  
### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>Para criar uma função que selecione dados filtrados na tabela PurchaseOrderDetail  
  
1.  No Gerenciador de Soluções, expanda Default.aspx e clique duas vezes em Default.aspx.cs.  
  
2.  Crie uma nova função que aceita um parâmetro, **productid**, do tipo Inteiro, retorna um objeto **datatable** e faz o seguinte.  
  
    1.  Cria uma instância do conjunto de dados, **DataSet2**, criado na Etapa 2 da [Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Crie uma conexão com o banco de dados SQL Server para executar a consulta definida na **Lição 4: Definir uma conexão de dados e uma DataTable para o relatório filho**.  
  
    3.  A consulta incluirá um parâmetro, **productid**, para garantir que os dados retornados serão filtrados com base na **ProductID** selecionada no relatório pai.  
  
    4.  Preencha a instância do DataSet com os dados filtrados executando a consulta.  
  
    5.  Retorna a DataTable **PurchaseOrderDetail** .  
  
        A função terá aparência similar à mostrada abaixo (Isso é apenas para fins de referência. Você pode seguir o padrão desejado para buscar os dados necessários ao relatório filho).  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlCommand cmd = new SqlCommand("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = @ProductID", sqlconn);  
                  
                        // Sets the productid parameter.  
                        cmd.Parameters.Add((new SqlParameter("@ProductID", SqlDbType.Int)).Value = productid);  
  
                        SqlDataAdapter adap = new SqlDataAdapter(cmd);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>Para adicionar um manipulador de eventos que recupere valores de parâmetro e associe a DataTable PurchaseOrdeDetail ao relatório filho  
  
1.  Abra Default.aspx no modo designer.  
  
2.  Clique com o botão direito do mouse no controle ReportViewer e selecione **Propriedades**.  
  
3.  No painel **Propriedades** , selecione o ícone **Eventos** .  
  
4.  Clique duas vezes no evento **Detalhamento** .  
  
    Isso adicionará uma seção do manipulador de eventos ao código, que será semelhante ao conteúdo abaixo.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Conclua o manipulador de eventos. Ele deve incluir a seguinte funcionalidade.  
  
    1.  Busque a referência de objeto do relatório filho no parâmetro *DrillthroughEventArgs* .  
  
    2.  Obtenha a lista de parâmetros do relatório filho no objeto do relatório filho buscado.  
  
    3.  Itere pela coleção do parâmetro e recupere o valor do parâmetro **ProductID**, passado pelo relatório pai.  
  
    4.  Chame a função **GetPurchaseOrderDetail**e passe o valor para o parâmetro **ProductID**.  
  
    5.  Associe a DataTable **PurchaseOrderDetail** à fonte de dados correspondente do Relatório.  
  
        O código completo do manipulador de eventos será semelhante ao conteúdo seguinte.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salve o arquivo.  
  
## <a name="next-task"></a>Próxima tarefa  
Você criou, com êxito, um filtro de dados para a tabela de dados definida para o relatório filho. Em seguida, você compilará e executará o aplicativo de site. Consulte [Lição 9: Criar e executar o aplicativo](../reporting-services/lesson-9-build-and-run-the-application.md).  
  
  
  

