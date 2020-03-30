---
title: 'Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d9be825b53cfab3601dc755b9122039669ce758
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "62651356"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho
Depois que você criar o relatório pai, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório filho. Neste tutorial, a conexão de dados é estabelecida com o banco de dados AdventureWorks2014.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório filho)  
  
1.  No menu **Site** , selecione **Adicionar Novo Item**.  
  
2.  Na caixa de diálogo **Adicionar Novo Item** , selecione **DataSet** e clique em **Adicionar**. Quando solicitado, você deve adicionar o item à pasta **App_Code** selecionando **Sim**.  
  
    Isso adicionará um novo arquivo XSD **DataSet2.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **TableAdapter** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Na página **Escolher sua Conexão de Dados** , você pode selecionar a conexão criada na Lição 2. Se você já fez isso, selecione **Avançar** e vá para a etapa 8. Caso contrário, selecione **Nova Conexão**.  
  
5.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  Na caixa **Nome do servidor** , insira o servidor em que o banco de dados **AdventureWorks2014** está localizado.  
  
        A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Na lista suspensa **Selecionar ou inserir um nome de banco de dados** , clique em **AdventureWorks2014**.  
  
    4.  Selecione **OK** e, em seguida, selecione **Avançar**.  
  
6.  Se você selecionou **Usar Autenticação do SQL Server** na etapa 5 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
7.  Na página **Salvar a Cadeia de Conexão no Arquivo de Configuração do Aplicativo** , digite o nome da cadeia de conexão ou aceite o **AdventureWorks2014ConnectionString**padrão. Selecione **Avançar**.  
  
8.  Na página **Escolher um Tipo de Comando** , selecione **Usar Instruções SQL**e clique em **Avançar**.  
  
9. Na página **Inserir uma Instrução SQL** , insira a consulta Transact-SQL a seguir para recuperar dados do banco de dados **AdventureWorks2014** e clique em **Avançar**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
    Você também pode criar a consulta selecionando **Construtor de Consultas**e verificar a consulta selecionando o botão **Executar Consulta** . Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como obter o banco de dados de exemplo **AdventureWorks2014**, consulte [Bancos de dados de exemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
10. Na página **Escolher os Métodos a Serem Gerados** , desmarque **Crie métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)** e selecione **Concluir**.  
  
    > [!WARNING]  
    > Lembre-se de desmarcar a opção **Criar métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)**  
  
    Agora você concluiu a configuração de [DataTable](https://msdn.microsoft.com/library/system.data.datatable.aspx) do ADO.NET como uma fonte de dados do relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a **DataTable** adicionada, listando as colunas especificadas na consulta. O DataSet2 contém os dados da tabela PurhcaseOrderDetail, com base na consulta.  
  
11. Salve o arquivo.  
  
12. Para visualizar os dados, selecione **Visualizar Dados** no menu **Dados** e selecione **Visualizar**.  
  
## <a name="next-task"></a>Próxima tarefa  
Você criou uma conexão de dados e uma tabela de dados para o relatório filho. Em seguida, você criará o relatório filho usando o Assistente de Relatório. Consulte [Lição 5: Criar o relatório filho usando o Assistente de Relatório](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md).  
  

