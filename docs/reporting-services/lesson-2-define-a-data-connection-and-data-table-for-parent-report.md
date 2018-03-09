---
title: "Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
caps.latest.revision: "8"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aaa0c4a8bccf85ddb3e3d58322cd2617db715f03
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai
Depois que você criar um novo projeto de site usando o modelo de site ASP.NET para o Visual C #, a próxima etapa será criar uma conexão de dados e uma tabela de dados para o relatório pai. Neste tutorial, a conexão de dados é estabelecida com o banco de dados AdventureWorks2014.  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir uma conexão de dados e uma DataTable adicionando um DataSet (para o relatório pai)  
  
1.  No menu **Site** , selecione **Adicionar Novo Item**.  
  
2.  Na caixa de diálogo **Adicionar Novo Item** , selecione **DataSet** e **Adicionar**. Quando solicitado, você deve adicionar o item à pasta **App_Code** selecionando **Sim**.  
  
    Isso adicionará um novo arquivo XSD **DataSet1.xsd** ao projeto e abrirá o Designer de Conjunto de Dados.  
  
3.  Na janela Caixa de Ferramentas, arraste um controle **[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx.aspx)** até a superfície de design. Isso inicializará o Assistente de Configuração do **TableAdapter** .  
  
4.  Na página **Escolher a Conexão de Dados** , clique em **Nova Conexão**.  
  
5.  Se esta for a primeira vez que você criou uma fonte de dados no Visual Studio, você verá a página **Escolher Fonte de Dados** . Na caixa **Fonte de Dados** , selecione **Microsoft SQL Server**.  
  
6.  Na caixa de diálogo **Adicionar Conexão** , realize as seguintes etapas:  
  
    1.  Na caixa **Nome do servidor** , insira o servidor em que o banco de dados **AdventureWorks2014** está localizado.  
  
        A instância padrão do SQL Server Express é **(local)\sqlexpress**.  
  
    2.  Na seção **Fazer logon no servidor** , selecione a opção que lhe fornece acesso aos dados. **Usar Autenticação do Windows** é o padrão.  
  
    3.  Na lista suspensa **Selecionar ou inserir um nome de banco de dados** , clique em **AdventureWorks2014**.  
  
    4.  Selecione **OK**e selecione **Avançar**.  
  
7.  Se você tiver selecionado **Usar Autenticação do SQL Server** na Etapa 6 (b), selecione a opção que especificará se os dados confidenciais serão incluídos na cadeia de caracteres ou defina as informações no código do aplicativo.  
  
8.  Na página **Salvar a Cadeia de Conexão no Arquivo de Configuração do Aplicativo** , digite o nome da cadeia de conexão ou aceite o **AdventureWorks2014ConnectionString**padrão. Selecione **Avançar**.  
  
9. Na página **Escolher um Tipo de Comando** , selecione **Usar Instruções SQL**e clique em **Avançar**.  
  
10. Na página **Inserir uma Instrução SQL** , insira a consulta Transact-SQL a seguir para recuperar dados do banco de dados **AdventureWorks2014** e clique em **Avançar**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    Você também pode criar a consulta clicando em **Construtor de Consultas**e verificar a consulta selecionando **Executar Consulta**. Se a consulta não retornar os dados esperados, talvez você esteja usando uma versão anterior do AdventureWorks. Para obter mais informações sobre como obter o banco de dados de exemplo **AdventureWorks2014**, consulte [Bancos de dados de exemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
11. Na página **Escolher os Métodos a Serem Gerados** , lembre-se de desmarcar **Crie métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)**e selecione **Concluir**.  
  
    > [!WARNING]  
    > Lembre-se de desmarcar a opção **Criar métodos para enviar atualizações diretamente ao banco de dados (GenerateDBDirectMethods)**  
  
    Agora você concluiu a configuração do objeto DataTable do ADO.NET como fonte de dados do relatório. Na página Designer de Conjunto de Dados no Visual Studio, você verá a DataTable o objeto DataTable que adicionou, listando as colunas especificadas na consulta. O DataSet1 contém os dados da tabela Product, com base na consulta.  
  
12. Salve o arquivo.  
  
13. Para visualizar os dados, selecione **Visualizar Dados** no menu **Dados** e selecione **Visualizar**.  
  
## <a name="next-task"></a>Próxima tarefa  
Você criou uma conexão de dados e uma tabela de dados para o relatório pai. Em seguida, você criará o relatório pai usando o Assistente de Relatório. Consulte [Lição 3: Criar o relatório pai usando o Assistente de Relatório](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md).  
  

