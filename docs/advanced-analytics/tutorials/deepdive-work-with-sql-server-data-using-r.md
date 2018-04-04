---
title: Trabalhar com dados do SQL Server usando o R (SQL e R mergulho profundo) | Microsoft Docs
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 5cd152ac5da350b216eaf3f517d5da2d1c415a4d
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="work-with-sql-server-data-using-r-sql-and-r-deep-dive"></a>Trabalhar com dados do SQL Server usando o R (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, configurar o ambiente e adicionar os dados que necessários para treinar os modelos e executar alguns resumos rápidos de dados. Como parte do processo, você deve concluir estas tarefas:
  
- Criar um novo banco de dados para armazenar os dados de treinamento e pontuação dos dois modelos do R.
  
- Criar uma conta (um usuário do Windows ou logon do SQL) que será usada na comunicação entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Criar fontes de dados no R para trabalhar com dados do e objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Usar a fonte de dados do R para carregar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Usar o R para obter uma lista de variáveis e modificar os metadados da tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Criar um contexto de computação para permitir a execução remota de código do R.
  
- (Opcional) Habilite o rastreamento no contexto de computação remota.
  
## <a name="create-the-database-and-user"></a>Criar o banco de dados e o usuário

Para este passo a passo, crie um novo banco de dados em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e adicionar um logon SQL com permissões para gravar e ler dados e executar scripts R.

> [!NOTE]
> Se você é somente leitura de dados, a conta que executa os scripts de R requer permissões SELECT (**db_datareader** função) no banco de dados especificado. No entanto, neste tutorial, você deve ter privilégios de administrador DDL para preparar o banco de dados e para criar tabelas para salvar os resultados de pontuação.
> 
> Além disso, se você não for o proprietário do banco de dados, você precisa de permissão EXECUTE ANY EXTERNAL SCRIPT, para executar scripts R.

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
  
    Se você não conseguir se conectar ao banco de dados, verifique se as conexões remotas estão habilitadas para o servidor e se o protocolo Pipes Nomeados foi habilitado. Dicas de solução de problemas adicionais são fornecidas neste artigo: [solucionar problemas de conexão com o mecanismo de banco de dados do SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **O nome de minha tabela tem datareader como prefixo. Por quê?**
  
    Quando você especifica o esquema padrão para esse usuário como **db_datareader**, todas as tabelas e outros novos objetos criados por esse usuário são prefixados com o *esquema* nome. Um esquema é como uma pasta que você pode adicionar a um banco de dados para organizar objetos. O esquema também define os privilégios de um usuário no banco de dados.
  
    Quando o esquema está associado um determinado nome de usuário, o usuário é o _proprietário do esquema_. Quando você cria um objeto, você sempre o cria em seu próprio esquema, a menos que você solicite especificamente que ele seja criado em outro esquema.
  
    Por exemplo, se você criar uma tabela com o nome `*`TestData`, and your default schema is **db\_datareader**, the table is created with the name `.db_datareader < database_name >. TestData'.
  
    Por esse motivo, um banco de dados pode conter várias tabelas com o mesmo nome, desde que as tabelas pertençam a esquemas diferentes.
   
    Se você está procurando uma tabela e não especificar um esquema, o servidor de banco de dados procura um esquema que você possui. Portanto, não é necessário especificar o nome do esquema ao acessar tabelas em um esquema associado ao seu logon.
  
- **Não tenho privilégios DDL. Ainda posso executar o tutorial**?
  
    Sim. No entanto, você precisará pedir que alguém pré-carregue os dados nas tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ignorar as seções que solicitam a criação de novas tabelas. As funções que exigem privilégios DDL são destacadas no tutorial sempre que possível.

    Além disso, peça ao administrador para conceder a permissão EXECUTE ANY EXTERNAL SCRIPT. É necessário para a execução de script R, se for remoto, ou usando `sp_execute_external_script`.

## <a name="next-step"></a>Próxima etapa

[Criar objetos de dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>Visão geral

[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)



