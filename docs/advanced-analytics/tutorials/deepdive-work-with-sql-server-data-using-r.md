---
title: Trabalhar com dados do SQL Server usando o R | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0a3d7ba0-4113-4cde-9645-debba45cae8f
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6db9cc485778e4074b5b648b23572edee3a0f42e
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="work-with-sql-server-data-using-r"></a>Trabalhar com dados do SQL Server usando o R

Nesta lição, você aprenderá a configurar o ambiente e adicionar os dados necessários para treinar seus modelos e executar alguns resumos rápidos dos dados. Como parte do processo, você concluirá estas tarefas:
  
- Criar um novo banco de dados para armazenar os dados de treinamento e pontuação dos dois modelos do R.
  
- Criar uma conta (um usuário do Windows ou logon do SQL) que será usada na comunicação entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Criar fontes de dados no R para trabalhar com dados do e objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Usar a fonte de dados do R para carregar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Usar o R para obter uma lista de variáveis e modificar os metadados da tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Criar um contexto de computação para permitir a execução remota de código do R.
  
- Saiba como habilitar o rastreamento no contexto de computação remota.
  
## <a name="create-the-database-and-user"></a>Criar o banco de dados e o usuário

Neste passo a passo, você criará um novo banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], e adicionará um logon SQL com permissões para gravar e ler dados, bem como para executar scripts do R.

> [!NOTE]
> Se você é somente leitura de dados, a conta que executa os scripts de R requer somente as permissões SELECT (**db_datareader** função) no banco de dados especificado. No entanto, neste tutorial, você precisará de privilégios de administrador DDL para preparar o banco de dados e criar tabelas para salvar os resultados da pontuação.
> 
> Além disso, se você não for o proprietário do banco de dados, você precisará de permissão, EXECUTE ANY EXTERNAL SCRIPT, para poder executar scripts R.

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione a instância em que o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está habilitado, clique com o botão direito do mouse em **Bancos de dados**e selecione **Novo banco de dados**.
  
2. Digite um nome para o novo banco de dados. Você pode usar qualquer nome desejado. Basta se lembrar de editar todos os scripts do [!INCLUDE[tsql](../../includes/tsql-md.md)] e R neste passo a passo de forma adequada.
  
    > [!TIP]
    > Para exibir o nome do banco de dados atualizado, clique com o botão direito do mouse em **Bancos de dados** e selecione **Atualizar** .
  
3. Clique em **Nova Consulta**e altere o contexto do banco de dados mestre.
  
4. Na janela **Nova consulta** , execute os comandos a seguir para criar as contas de usuário e atribuí-las ao banco de dados usado neste tutorial. Lembre-se de alterar o nome do banco de dados, se necessário.
  
**Usuário do Windows**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**Logon do SQL**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. Para confirmar que o usuário foi criado, selecione o novo banco de dados, expanda **Segurança**e expanda **Usuários**.

## <a name="troubleshooting"></a>Solução de problemas

Esta seção lista alguns problemas comuns que podem ocorrer durante a configuração do banco de dados.

- **Como posso verificar a conectividade de banco de dados e verificar as consultas SQL?**
  
    Antes de executar o código do R usando o servidor, é recomendável verificar se o banco de dados pode ser acessado no ambiente de desenvolvimento do R. O [Gerenciador de Servidores no Visual Studio](https://msdn.microsoft.com/library/x603htbk.aspx) e o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) são ferramentas gratuitas com recursos avançados de gerenciamento e conectividade de banco de dados.
  
    Se você não quiser instalar as ferramentas de gerenciamento de banco de dados adicionais, será possível criar um teste de conexão com a instância do SQL Server usando o [Administrador de Fonte de Dados ODBC](https://msdn.microsoft.com/library/ms714024.aspx) no Painel de Controle. Se o banco de dados estiver configurado corretamente e você inserir o nome de usuário correto e a senha, você deverá conseguir ver o banco de dados que acabou de criar e selecioná-lo como o banco de dados padrão.
  
    Se você não conseguir se conectar ao banco de dados, verifique se as conexões remotas estão habilitadas para o servidor e se o protocolo Pipes Nomeados foi habilitado. Outras dicas de solução de problemas são fornecidas [neste artigo](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx).
  
- **O nome de minha tabela tem datareader como prefixo. Por quê?**
  
    Quando você especificar o esquema padrão para esse usuário como **db_datareader**, todas as tabelas e outros novos objetos criados por esse usuário terão esse *esquema*como prefixo. Um esquema é como uma pasta que você pode adicionar a um banco de dados para organizar objetos. O esquema também define os privilégios de um usuário no banco de dados.
  
    Quando o esquema estiver associado a determinado nome de usuário, o usuário será chamado o proprietário do esquema. Quando você cria um objeto, você sempre o cria em seu próprio esquema, a menos que você solicite especificamente que ele seja criado em outro esquema.
  
    Por exemplo, se você criar uma tabela com o nome *TestData* e o esquema padrão for **db_datareader**, a tabela será criada com o nome *<database_name>.db_datareader.TestData*.
  
    Por esse motivo, um banco de dados pode conter várias tabelas com o mesmo nome, desde que as tabelas pertençam a esquemas diferentes.
   
    Se você estiver procurando uma tabela e não especificar um esquema, o servidor de banco de dados procurará um esquema seu. Portanto, não é necessário especificar o nome do esquema ao acessar tabelas em um esquema associado ao seu logon.
  
- **Não tenho privilégios DDL. Ainda posso executar o tutorial**?
  
    Sim. No entanto, você precisará pedir que alguém pré-carregue os dados nas tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ignorar as seções que solicitam a criação de novas tabelas. As funções que exigem privilégios DDL geralmente são destacadas no tutorial.

    Além disso, peça ao administrador para conceder a permissão EXECUTE ANY EXTERNAL SCRIPT. É necessário para a execução de script R, se for remoto, ou usando `sp_execute_external_script`.

## <a name="next-step"></a>Próxima etapa

[Criar Objetos de Dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>Visão geral

[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)




