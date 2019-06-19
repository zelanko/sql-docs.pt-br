---
title: 'Como fazer: criar um teste de unidade do SQL Server vazio | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.createtest
ms.assetid: b6f3cd5a-3389-42d6-a93f-97b3ddf31b95
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8921129e8e5b7afcf3f141749bc31ec857a166e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098035"
---
# <a name="how-to-create-an-empty-sql-server-unit-test"></a>Como fazer: Criar um teste de unidade do SQL Server vazio
Inclua os testes de unidade no projeto de banco de dados verificar se as alterações feitas nos objetos de banco de dados não prejudicam a funcionalidade existente. Os procedimentos a seguir explicam como criar testes de unidade SQL Server para qualquer objeto de banco de dados. O SQL Server Data Tools inclui suporte adicional para procedimentos armazenados, gatilhos e funções de banco de dados. Para obter mais informações, confira [Como Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md).  
  
Quando você criar um teste de unidade do SQL Server usando o primeiro procedimento, um projeto de teste será criado automaticamente para você se não houver nenhum projeto de teste. Se os projetos de teste já existirem, você terá a opção de adicionar o novo teste a um desses projetos ou poderá criar um novo projeto de teste. Para obter mais informações sobre os projetos de teste, veja [Como: Criar um projeto de teste para testes de unidade de banco de dados do SQL Server](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md).  
  
Você tem duas opções para criar um teste de unidade do SQL Server:  
  
-   Crie um novo teste de unidade do SQL Server em uma nova classe de teste.  
  
    Todos os testes de unidade do SQL Server em uma classe de teste específica usarão os mesmos scripts TestInitialize e TestCleanup. Crie uma nova classe de teste se quiser que o teste de unidade use scripts TestInitialize e TestCleanup diferentes dos utilizados por outros testes de unidade. Para saber mais, confira [Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).  
  
-   Crie um novo teste de unidade do SQL Server em uma classe de teste existente.  
  
    Escolha esta opção se o teste de unidade usar os mesmos scripts TestInitialize e TestCleanup utilizados por outros testes de unidade na classe.  
  
### <a name="to-create-a-sql-server-unit-test-inside-a-new-test-class"></a>Para criar um teste de unidade do SQL Server em uma nova classe de teste  
  
1.  No menu **Teste**, clique em **Novo Teste**.  
  
    A caixa de diálogo **Adicionar Novo Teste** é exibida.  
  
2.  Em **Modelos**, clique em **Teste de Unidade do SQL Server**.  
  
3.  Em **Nome do Teste**, insira um nome para o teste.  
  
4.  Em **Adicionar ao Projeto de Teste**, selecione um projeto de teste existente, no qual esse teste será adicionado. Se não houver nenhum projeto de teste, ou se você quiser criar um novo projeto de teste, selecione **Criar um novo <language>projeto de teste**.  
  
5.  Clique em **OK**.  
  
    Se o projeto de teste for novo, a caixa de diálogo **Novo Projeto de Teste** será exibida. Nomeie o projeto e clique em **OK**.  
  
    Se o projeto de teste for novo ou não tiver sido configurado, a caixa de diálogo **Configuração de Teste do SQL Server<ProjectName>** é exibida. Essa caixa de diálogo permite configurar as seguintes informações do projeto de teste:  
  
    -   A conexão de banco de dados usada para executar os testes.  
  
    -   A conexão de banco de dados usada para validar os resultados do teste, implantar um banco de dados e gerar dados.  
  
    -   A implantação automática do projeto de banco de dados e das alterações de esquema associadas a uma configuração de projeto específica antes de você executar os testes de unidade.  
  
    Para obter mais informações, confira [Como Configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).  
  
6.  Forneça informações de configuração do projeto e clique em **OK**.  
  
    \- ou –  
  
    Clique em **Cancelar** para criar o teste de unidade sem configurar o projeto de teste.  
  
    O teste em branco aparece no **Designer de Teste de Unidade do SQL Server**. Dependendo da linguagem especificada para criar o projeto de teste, um arquivo de código-fonte do Visual Basic ou do Visual C\# é adicionado ao projeto de teste. Esse arquivo contém a classe de teste de unidade do SQL Server que o SQL Server Data Tools gera para o teste de unidade recém-criado. Essa classe de teste pode conter um ou mais testes de unidade que você pode adicionar por meio do Designer de Teste de Unidade do SQL Server ou do código como novos métodos de teste na classe de teste.  
  
    Você também pode adicionar testes fazendo o seguinte:  
  
    -   Clique com o botão direito do mouse em um projeto de teste no **Gerenciador de Soluções**, selecionando **Adicionar**, **Novo Teste** e, em seguida, **Teste de Unidade do SQL Server**.  
  
    -   No Pesquisador de Objetos do SQL Server, selecione Criar Testes de Unidade.  
  
    Quando você seleciona esse arquivo no **Gerenciador de Soluções**, ele é exibido no Designer de Teste de Unidade do SQL Server por padrão. Para exibir o código ou personalizá-la para adicionar mais funcionalidade aos testes de unidade, selecione o arquivo, clique com o botão direito do mouse e escolha **Exibir Código**.  
  
### <a name="to-create-a-sql-server-unit-test-inside-an-existing-test-class"></a>Para criar um teste de unidade do SQL Server em uma classe de teste existente  
  
1.  Abra uma classe de teste de unidade do SQL Server existente no **Designer de Teste de Unidade do SQL Server**. Você pode acessar o **Designer do Teste de Unidade do SQL Server** clicando duas vezes no arquivo do código de origem do teste de unidade no **Gerenciador de Soluções**.  
  
2.  Clique no sinal de adição ( **+** ) na barra de navegação para exibir a caixa de diálogo **Especificar um nome de teste de unidade**.  
  
3.  Digite um nome e clique em **OK**.  
  
    O novo teste de unidade do SQL Server está disponível na lista suspensa na barra de navegação. Ele também é adicionado como um novo método de teste na classe de teste. Para exibir o método de teste no código, selecione o arquivo de classe, clique com o botão direito do mouse e escolha **Exibir Código**. O nome do arquivo de classe de teste atual é exibido na guia na parte superior do **Designer de Teste de Unidade do SQL Server**.  
  
Depois que você configurar o projeto de teste e criar o teste de unidade, estas serão as próximas etapas:  
  
-   Adicionar um script de teste Transact\-SQL.  
  
-   Defina as ações de pré-teste e pós-teste.  
  
-   Adicione condições de teste ou outra instrução de asserção para verificar os resultados do script.  
  
> [!NOTE]  
> A condição de teste Inconclusivo é a condição padrão adicionada a cada teste. Ela é incluída para indicar que a verificação de teste não foi implementada. Exclua essa condição do teste depois que você tiver adicionado outras condições. Para obter mais informações, confira [Como adicionar condições de teste a testes de unidade de banco de dados](https://msdn.microsoft.com/library/aa833242(VS.100).aspx).  
  
## <a name="see-also"></a>Consulte Também  
[Como: Executar testes de unidade do SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md)  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Criar testes de unidade](https://msdn.microsoft.com/library/ms182523(VS.90).aspx)  
  
