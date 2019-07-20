---
title: Criar um banco de dados e permissões para tutoriais do RevoScaleR
description: Tutorial explicativo sobre como criar um banco de dados SQL Server para tutoriais de R..
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 88a8bb4ab81f3e7c18bcafce70488583fa0421fa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344644"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Criar um banco de dados e permissões (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

A lição um é sobre como configurar um banco de dados SQL Server e as permissões necessárias para concluir este tutorial. Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outro editor de consultas para concluir as seguintes tarefas:

> [!div class="checklist"]
> * Criar um novo banco de dados a fim de armazená-los para treinamento e pontuação de dois modelos de R
> * Criar um logon de usuário de banco de dados com permissões para criar e usar objetos de banco de dados
  
## <a name="create-the-database"></a>Criar o banco de dados

Este tutorial requer um banco de dados para o armazenamento e o código. Se você não for um administrador, peça ao DBA para criar o banco de dados e o logon para você. Você precisará de permissões para gravar e ler dados e para executar scripts do R.

1. No SQL Server Management Studio, conecte-se a uma instância de banco de dados habilitada para R.

2. Clique com o botão direito do mouse em **bancos**de dados e selecione **New Database**.
  
2. Digite um nome para o novo banco de dados: RevoDeepDive.
  

## <a name="create-a-login"></a>Criar um logon
  
1. Clique em **Nova Consulta**e altere o contexto do banco de dados mestre.
  
2. Na janela **Nova consulta** , execute os comandos a seguir para criar as contas de usuário e atribuí-las ao banco de dados usado neste tutorial. Lembre-se de alterar o nome do banco de dados, se necessário.

3. Para verificar o logon, selecione o novo banco de dados, expanda **segurança**e expanda **usuários**.
  
**usuário Windows**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**Logon do SQL**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>Atribuir permissões

Este tutorial demonstra o script R e as operações DDL, incluindo a criação e exclusão de tabelas e procedimentos armazenados, e a execução do script R em um processo externo no SQL Server. Nesta etapa, atribua permissões para permitir essas tarefas.

Este exemplo pressupõe um logon do SQL (DDUser01), mas se você tiver criado um logon do Windows, use-o em vez disso.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>Solucionar problemas de conexões

Esta seção lista alguns problemas comuns que podem ocorrer durante a configuração do banco de dados.

- **Como posso verificar a conectividade de banco de dados e verificar as consultas SQL?**
  
    Antes de executar o código do R usando o servidor, é recomendável verificar se o banco de dados pode ser acessado no ambiente de desenvolvimento do R. O [Gerenciador de Servidores no Visual Studio](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) e o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) são ferramentas gratuitas com recursos avançados de gerenciamento e conectividade de banco de dados.
  
    Se você não quiser instalar as ferramentas de gerenciamento de banco de dados adicionais, será possível criar um teste de conexão com a instância do SQL Server usando o [Administrador de Fonte de Dados ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) no Painel de Controle. Se o banco de dados estiver configurado corretamente e você inserir o nome de usuário correto e a senha, você deverá conseguir ver o banco de dados que acabou de criar e selecioná-lo como o banco de dados padrão.
  
    Os motivos comuns para falhas de conexão incluem conexões remotas não estão habilitadas para o servidor e o protocolo de pipes nomeados não está habilitado. Você pode encontrar mais dicas de solução de problemas neste artigo: [Solucionar problemas de conexão com o mecanismo de banco de dados de SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **O nome de minha tabela tem datareader como prefixo. Por quê?**
  
    Quando você especifica o esquema padrão para esse usuário como **db_datareader**, todas as tabelas e outros novos objetos criados por esse usuário são prefixados com o nome do *esquema* . Um esquema é como uma pasta que você pode adicionar a um banco de dados para organizar objetos. O esquema também define os privilégios de um usuário no banco de dados.
  
    Quando o esquema está associado a um nome de usuário específico, o usuário é o _proprietário do esquema_. Quando você cria um objeto, você sempre o cria em seu próprio esquema, a menos que você solicite especificamente que ele seja criado em outro esquema.
  
    Por exemplo, se você criar uma tabela com o nome **TestData**e o esquema padrão for **db_datareader**, a tabela será criada com o nome `<database_name>.db_datareader.TestData`.
  
    Por esse motivo, um banco de dados pode conter várias tabelas com o mesmo nome, desde que as tabelas pertençam a esquemas diferentes.
   
    Se você estiver procurando uma tabela e não especificar um esquema, o servidor de banco de dados procurará um esquema que você possui. Portanto, não é necessário especificar o nome do esquema ao acessar tabelas em um esquema associado ao seu logon.
  
- **Não tenho privilégios DDL. Ainda posso executar o tutorial**?
  
    Sim, mas você deve pedir que alguém carregue previamente os dados nas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas e pule para a próxima lição. As funções que exigem privilégios DDL são chamadas no tutorial sempre que possível.

    Além disso, peça ao administrador para conceder a você a permissão, EXECUTE qualquer SCRIPT externo. Ele é necessário para a execução do script do R, seja remoto `sp_execute_external_script`ou usando.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar objetos de dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)