---
title: 'Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 987e6924fe3fbffb416e4266861ae7cfede16596
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108503"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai
  Depois que você criar um novo projeto de site usando o modelo de site ASP.NET para o Visual C #, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório pai. Neste tutorial, a conexão de dados é com o banco de dados AdventureWorks2008. Você também tem a opção de se conectar ao banco de dados AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório pai)  
  
1.  No menu **Site** , selecione **Adicionar Novo Item**.  
  
2.  Na caixa de diálogo **Adicionar novo item** , selecione **conjunto** de um e clique em **Adicionar**. Quando solicitado, você deve adicionar o item à pasta **App_Code** clicando em **Sim**.  
  
     Isso adicionará um novo arquivo XSD **DataSet1.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Na página **escolher sua conexão de dados** , clique em **nova conexão**.  
  
5.  Se esta for a primeira vez que você criou uma fonte de dados no Visual Studio, você verá a página **Escolher Fonte de Dados**. Na caixa **Fonte de Dados** , selecione **Microsoft SQL Server**.  
  
6.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  Na caixa **nome do servidor** , insira o servidor no qual o banco de dados **AdventureWorks2008** está localizado.  
  
         A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Na lista suspensa **selecionar ou digitar um nome de banco de dados** , clique em **AdventureWorks2008**.  
  
    4.  Clique em **OK** e em **Avançar**.  
  
7.  Se você tiver selecionado **Usar Autenticação do SQL Server** na Etapa 6 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
8.  Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , digite o nome da cadeia de conexão ou aceite o **AdventureWorks2008ConnectionString**padrão. Clique em **Próximo**.  
  
9. Na página **escolher um tipo de comando** , selecione **usar instruções SQL**e clique em **Avançar**.  
  
10. Na página **Inserir uma instrução SQL** , insira a seguinte consulta TRANSACT-SQL para recuperar dados do banco de **AdventureWorks2008** e clique em **Avançar**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     Você também pode criar a consulta clicando em **Construtor de consultas**e, em seguida, verificar a consulta clicando em **Executar consulta**. Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como instalar a versão **AdventureWorks2008** do AdventureWorks, consulte [passo a passos: Instalando o banco de dados AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. Na página **escolher os métodos a serem gerados** , não se esqueça de desmarcar **criar métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)** e, em seguida, clique em **concluir**.  
  
    > [!WARNING]  
    >  Verifique se desmarcou Criar  
  
     Agora você concluiu a configuração do objeto DataTable do ADO.NET como fonte de dados do relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a DataTable o objeto DataTable que adicionou, listando as colunas especificadas na consulta. O DataSet1 contém os dados da tabela Product, com base na consulta.  
  
12. Salve o arquivo.  
  
13. Para visualizar os dados, clique em **Visualizar dados** no menu **dados** e clique em **Visualizar**.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou uma conexão de dados e uma tabela de dados para o relatório pai. Em seguida, você criará o relatório pai usando o Assistente de Relatório.  
  
  
