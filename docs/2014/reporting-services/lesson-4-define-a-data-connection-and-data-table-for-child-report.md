---
title: 'Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1008202519f1d9bcbf48dfdc4cd4ef3a3cbbe20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108472"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho
  Depois que você criar o relatório pai, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório filho. Neste tutorial, a conexão de dados é com o banco de dados AdventureWorks2008. Você também tem a opção de se conectar ao banco de dados AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório filho)  
  
1.  No menu do **site** , clique em **Adicionar novo item**.  
  
2.  Na caixa de diálogo **Adicionar novo item** , clique em **conjunto** de um e em **Adicionar**. Quando solicitado, você deve adicionar o item à pasta **App_Code** clicando em **Sim**.  
  
     Isso adicionará um novo arquivo XSD **DataSet2.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **TableAdapter** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Na página **escolher sua conexão de dados** , clique em **nova conexão**.  
  
5.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  Na caixa **nome do servidor** , insira o servidor no qual o banco de dados **AdventureWorks2008** está localizado.  
  
         A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Na lista suspensa **selecionar ou digitar um nome de banco de dados** , clique em **AdventureWorks2008**.  
  
    4.  Clique em **OK** e em **Avançar**.  
  
6.  Se você selecionou **Usar Autenticação do SQL Server** na etapa 5 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
7.  Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , digite o nome da cadeia de conexão ou aceite o **AdventureWorks2008ConnectionString**padrão. Clique em **Próximo**.  
  
8.  Na página **escolher um tipo de comando** , selecione **usar instruções SQL**e clique em **Avançar**.  
  
9. Na página **Inserir uma instrução SQL** , insira a seguinte consulta TRANSACT-SQL para recuperar dados do banco de **AdventureWorks2008** e clique em **Avançar**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     Você também pode criar a consulta clicando em **Construtor de consultas**e, em seguida, verificar a consulta clicando no botão **Executar consulta** . Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como instalar a versão **AdventureWorks2008** do AdventureWorks, consulte [passo a passos: Instalando o banco de dados AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
10. Na página **escolher os métodos a serem gerados** , desmarque **criar métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)** e clique em **concluir**.  
  
     Agora você concluiu a configuração da [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) ADO.net como fonte de dados para o relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a **DataTable** adicionada, listando as colunas especificadas na consulta. O DataSet2 contém os dados da tabela PurhcaseOrderDetail, com base na consulta.  
  
11. Salve o arquivo.  
  
12. Para visualizar os dados, clique em **Visualizar dados** no menu **dados** e clique em **Visualizar**.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou uma conexão de dados e uma tabela de dados para o relatório filho. Em seguida, você criará o relatório filho usando o Assistente de Relatório.  
  
  
