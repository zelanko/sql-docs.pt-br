---
title: 'Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3403d416ed7945d4f980ef4c15d89ff0e56c8720
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184306"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho
  Depois que você criar o relatório pai, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório filho. Neste tutorial, a conexão de dados é com o banco de dados AdventureWorks2008. Você também tem a opção de se conectar ao banco de dados AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório filho)  
  
1.  Sobre o **site** menu, clique em **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, clique em **DataSet** e, em seguida, clique em **adicionar**. Quando solicitado, você deve adicionar o item para o **App_Code** pasta clicando **Sim**.  
  
     Isso adicionará um novo arquivo XSD **DataSet2.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **TableAdapter** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Sobre o **escolha sua Conexão de dados** , clique em **nova Conexão**.  
  
5.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  No **nome do servidor** , digite o servidor em que o **AdventureWorks2008** banco de dados está localizado.  
  
         A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Dos **selecione ou insira um nome de banco de dados** lista suspensa, clique em **AdventureWorks2008**.  
  
    4.  Clique em **OK**e em **Avançar**.  
  
6.  Se você selecionou **Usar Autenticação do SQL Server** na etapa 5 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
7.  Sobre o **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** página, digite o nome da cadeia de caracteres de conexão ou aceite o padrão **AdventureWorks2008ConnectionString**. Clique em **Avançar**.  
  
8.  Sobre o **escolher um tipo de comando** página, selecione **usar instruções SQL**e, em seguida, clique em **próxima**.  
  
9. No **insira uma instrução SQL** página, insira a seguinte consulta Transact-SQL para recuperar dados do **AdventureWorks2008** banco de dados e, em seguida, clique em **próxima**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     Você também pode criar a consulta clicando **construtor de consultas**e, em seguida, verifique se a consulta clicando em **executar consulta** botão. Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como instalar o **AdventureWorks2008** versão da AdventureWorks, consulte [passo a passo: Instalando o banco de dados AdventureWorks](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
10. Sobre o **escolha métodos para gerar** página, desmarque a opção **crie métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)** e, em seguida, clique em **concluir**.  
  
     Agora você concluiu Configurando o ADO.NET [DataTable](http://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) como fonte de dados para seu relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a **DataTable** adicionada, listando as colunas especificadas na consulta. O DataSet2 contém os dados da tabela PurhcaseOrderDetail, com base na consulta.  
  
11. Salve o arquivo.  
  
12. Para visualizar os dados, clique em **visualizar dados** sobre o **dados** menu e, em seguida, clique **visualização**.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou uma conexão de dados e uma tabela de dados para o relatório filho. Em seguida, você criará o relatório filho usando o Assistente de Relatório.  
  
  
