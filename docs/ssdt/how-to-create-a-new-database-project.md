---
title: Como criar um novo projeto de banco de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.dbprojectwizard.importschema
- sql.data.tools.SqlProjectImportDatabaseDialog.dialog
- sql.data.tools.importscriptwizard.welcome
- sql.data.tools.importscriptwizard.summary
- sql.data.tools.SqlProjectImportDatabaseSummaryDialog.dialog
- sql.data.tools.importscriptwizard.fileselection
ms.assetid: 0b7883fa-b6e1-4ccf-b1d8-f522fd03a59d
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2482967c3001377a803b87e6bcd46c3cc9183b82
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093646"
---
# <a name="how-to-create-a-new-database-project"></a>Como: Criar um novo projeto de banco de dados
Você pode criar um novo projeto de banco de dados e importar o esquema de banco de dados de um banco de dados existente, um arquivo de script .sql ou um aplicativo da camada de dados (.dacpac). Você poderá invocar então as mesmas ferramentas de designer visual (Editor de Transact\-SQL, Designer de Tabela) disponíveis para o desenvolvimento de bancos de dados conectados para fazer alterações no projeto de banco de dados offline e para publicar as alterações no banco de dados de produção. As alterações também podem ser salvas como um script a ser publicado posteriormente. Usando o painel **Propriedades do Projeto**, você pode alterar a plataforma de destino para versões diferentes do SQL Server (incluindo o SQL Azure).  
  
Os dois procedimentos a seguir obtêm essencialmente a mesma meta criando um novo projeto de banco de dados e importando esquema de um banco de dados existente. Cada objeto de banco de dados será representado como um arquivo de script do SQL (.sql) no **Gerenciador de Soluções**. Para saber mais sobre como importar esquema de banco de dados de um instantâneo, confira [Como criar um instantâneo de um projeto](../ssdt/how-to-create-a-snapshot-of-a-project.md).  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-create-a-new-database-project-off-a-connected-database"></a>Para criar um novo projeto de banco de dados fora de um banco de dados conectado  
  
1.  Clique com o botão direito do mouse no nó **TradeDev** no **Pesquisador de Objetos do SQL Server** e selecione **Criar Novo Projeto**.  
  
2.  Na caixa de diálogo **Importar Banco de Dados**, observe que as configurações de **Conexão de banco de dados de origem** foram predefinidas pelo banco de dados que você selecionou no **Pesquisador de Objetos do SQL Server**. Na configuração **Projeto de destino**, altere o nome do projeto para **TradeDev**.  
  
3.  Na seção **Importar Configurações**, observe as opções para importar objetos e configurações específicas, e criar pastas para cada esquema e/ou tipo de objeto. Para obter uma hierarquia organizada de todos os seus objetos de banco de dados, aceite todas as configurações padrão e clique em **Iniciar**.  
  
4.  A caixa de diálogo **Importar Banco de Dados** mostra uma barra de progresso e exibe uma lista de objetos que o SSDT está importando. Quando a operação de importação tiver sido concluída, clique em **Concluir** para sair da tela final.  
  
5.  Examine a hierarquia no **Gerenciador de Soluções**. Expanda a pasta **dbo** e você localizará pastas **Funções**, **Tabelas** e **Exibições** separadas. Observe que as tabelas e a função são agrupadas nas suas pastas de esquema.  
  
6.  Clique duas vezes em **Products.sql** em **Tabelas**. O **Designer de Tabela** abre, mostrando a interpretação visual da tabela na Grade de Colunas e a definição de script da tabela no Painel de Script. Isso é idêntico ao mostrado na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
7.  Desmarque a caixa **Permitir Valores Nulos** para a coluna **CustomerId**. Pressione CTRL + S para salvar o arquivo.  
  
8.  Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Build** para criar o projeto de banco de dados.  
  
    Os resultados da operação Compilar podem ser vistos na Janela de Saída  
  
### <a name="to-create-a-new-project-and-import-existing-database-schema"></a>Para criar um novo projeto e importar esquema de banco de dados existente  
  
1.  Clique em **Arquivo**, **Novo** e **Projeto**. Na caixa de diálogo **Novo Projeto**, selecione **SQL Server** no painel esquerdo. Observe que há somente um tipo de projeto de banco de dados: o **Projeto de Banco de Dados do SQL Server**. Não há nenhum projeto específico de plataforma, como em versões anteriores do Visual Studio. Você poderá definir sua plataforma de destino na caixa de diálogo **Configurações do Projeto** depois que o projeto tiver sido criado. Essa tarefa será abordada no tópico [Como alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md).  
  
2.  Altere o nome do projeto para **TradeDev** e clique em **OK** para criar o novo projeto.  
  
3.  Clique com o botão direito do mouse no projeto **TradeDev** criado no **Gerenciador de Soluções**, selecione **Importar** e **Banco de Dados**.  
  
    A caixa de diálogo **Importar Banco de Dados** é aberta. Na seção **Conexão de banco de dados de origem**, clique em **Escolher um banco de dados** e selecione **TradeDev**. Se **TradeDev** estiver ausente da lista suspensa, use o botão **Nova Conexão** para editar as Propriedades da Conexão.  
  
4.  Na seção **Importar Configurações**, observe as opções para importar objetos e configurações específicas, e criar pastas para cada esquema e/ou tipo de objeto. Para obter uma hierarquia organizada de todos os seus objetos de banco de dados, aceite todas as configurações padrão e clique em **Iniciar**.  
  
5.  A caixa de diálogo **Importar Banco de Dados** mostra uma barra de progresso e exibe uma lista de objetos que o SSDT está importando. Quando a operação de importação tiver sido concluída, clique em **Concluir** para sair da tela final.  
  
6.  Examine a hierarquia no **Gerenciador de Soluções**. Expanda a pasta **dbo** e você localizará pastas **Funções**, **Tabelas** e **Exibições** separadas. Observe que as tabelas e a função são agrupadas nas suas pastas de esquema.  
  
7.  Clique duas vezes em **Products.sql** em **Tabelas**. O **Designer de Tabela** abre, mostrando a interpretação visual da tabela na Grade de Colunas e a definição de script da tabela no Painel de Script. Isso é idêntico ao mostrado na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
8.  Desmarque a caixa **Permitir Valores Nulos** para a coluna **CustomerId**. Pressione CTRL + S para salvar o arquivo.  
  
9. Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Build** para criar o projeto de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Como alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
