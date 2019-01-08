---
title: 'Lição 2: Definir uma Conexão de dados e uma tabela de dados para o relatório pai | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5dba0a87f34c794e22fa52274591bbec0db63f86
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358538"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lição 2: definir uma conexão de dados e uma tabela de dados para o relatório pai
  Depois que você criar um novo projeto de site usando o modelo de site ASP.NET para o Visual C #, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório pai. Neste tutorial, a conexão de dados é com o banco de dados AdventureWorks2008. Você também tem a opção de se conectar ao banco de dados AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório pai)  
  
1.  No menu **Site** , selecione **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **DataSet** e clique em **adicionar**. Quando solicitado você deve adicionar o item para o **App_Code** pasta clicando **Sim**.  
  
     Isso adicionará um novo arquivo XSD **DataSet1.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Sobre o **escolha sua Conexão de dados** , clique em **nova Conexão**.  
  
5.  Se esta for a primeira vez que você criou uma fonte de dados no Visual Studio, você verá a página **Escolher Fonte de Dados**. Na caixa **Fonte de Dados** , selecione **Microsoft SQL Server**.  
  
6.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  No **nome do servidor** , digite o servidor em que o **AdventureWorks2008** banco de dados está localizado.  
  
         A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Dos **selecione ou insira um nome de banco de dados** lista suspensa, clique em **AdventureWorks2008**.  
  
    4.  Clique em **OK**e em **Avançar**.  
  
7.  Se você tiver selecionado **Usar Autenticação do SQL Server** na Etapa 6 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
8.  Sobre o **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** página, digite o nome da cadeia de caracteres de conexão ou aceite o padrão **AdventureWorks2008ConnectionString**. Clique em **Avançar**.  
  
9. Sobre o **escolher um tipo de comando** página, selecione **usar instruções SQL**e, em seguida, clique em **próxima**.  
  
10. No **insira uma instrução SQL** página, insira a seguinte consulta Transact-SQL para recuperar dados do **AdventureWorks2008** banco de dados e, em seguida, clique em **próxima**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     Você também pode criar a consulta clicando **construtor de consultas**e, em seguida, verifique se a consulta clicando em **executar consulta**. Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como instalar o **AdventureWorks2008** versão da AdventureWorks, consulte [passo a passo: Installing the AdventureWorks Database](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. Sobre o **escolha métodos para gerar** página, certifique-se de desmarcar **crie métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)** e, em seguida, clique em **concluir**.  
  
    > [!WARNING]  
    >  Verifique se desmarcou Criar  
  
     Agora você concluiu a configuração do objeto DataTable do ADO.NET como fonte de dados do relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a DataTable o objeto DataTable que adicionou, listando as colunas especificadas na consulta. O DataSet1 contém os dados da tabela Product, com base na consulta.  
  
12. Salve o arquivo.  
  
13. Para visualizar os dados, clique em **visualizar dados** sobre o **dados** menu e, em seguida, clique **visualização**.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou uma conexão de dados e uma tabela de dados para o relatório pai. Em seguida, você criará o relatório pai usando o Assistente de Relatório.  
  
  
