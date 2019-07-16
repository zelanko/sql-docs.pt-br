---
title: Criar um banco de dados e as permissões para RevoScaleR tutoriais - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como criar um banco de dados do SQL Server para obter tutoriais de R...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 84f78219bf4bb188f7a29e79718e107d7fa43347
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962164"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Criar um banco de dados e permissões (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Lição um é sobre como configurar um banco de dados do SQL Server e as permissões necessárias para concluir este tutorial. Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outro editor de consultas para concluir as seguintes tarefas:

> [!div class="checklist"]
> * Criar um novo banco de dados para armazenar os dados de treinamento e pontuação dois modelos de R
> * Criar um logon de usuário de banco de dados com permissões para criar e usar objetos de banco de dados
  
## <a name="create-the-database"></a>Criar o banco de dados

Este tutorial requer um banco de dados para armazenar dados e código. Se você não for um administrador, peça ao seu DBA para criar o banco de dados e faça logon para você. Você precisará de permissões para gravar e ler dados e executar scripts do R.

1. No SQL Server Management Studio, conecte-se a uma instância de banco de dados habilitado para R.

2. Clique com botão direito **bancos de dados**e selecione **novo banco de dados**.
  
2. Digite um nome para o novo banco de dados: RevoDeepDive.
  

## <a name="create-a-login"></a>Criar um logon
  
1. Clique em **Nova Consulta**e altere o contexto do banco de dados mestre.
  
2. Na janela **Nova consulta** , execute os comandos a seguir para criar as contas de usuário e atribuí-las ao banco de dados usado neste tutorial. Lembre-se de alterar o nome do banco de dados, se necessário.

3. Para verificar se o logon, selecione o novo banco de dados, expanda **segurança**e expanda **usuários**.
  
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

Este tutorial demonstra o script R e operações de DDL, incluindo a criação e exclusão de tabelas e procedimentos armazenados e executar o script de R em um processo externo no SQL Server. Nesta etapa, atribua permissões para permitir que essas tarefas.

Este exemplo pressupõe um logon do SQL (DDUser01), mas se você tiver criado um logon do Windows, use-a.

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
  
    Motivos comuns para falhas de conexão incluem remoto conexões não estão habilitadas para o servidor e o protocolo de Pipes nomeados não está habilitado. Você pode encontrar mais dicas de solução de problemas neste artigo: [Solucionar problemas de conexão para o mecanismo de banco de dados do SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **O nome de minha tabela tem datareader como prefixo. Por quê?**
  
    Quando você especifica o esquema padrão para esse usuário como **db_datareader**, todas as tabelas e outros novos objetos criados por esse usuário são prefixados com o *esquema* nome. Um esquema é como uma pasta que você pode adicionar a um banco de dados para organizar objetos. O esquema também define os privilégios de um usuário no banco de dados.
  
    Quando o esquema está associado um determinado nome de usuário, o usuário é o _proprietário do esquema_. Quando você cria um objeto, você sempre o cria em seu próprio esquema, a menos que você solicite especificamente que ele seja criado em outro esquema.
  
    Por exemplo, se você criar uma tabela com o nome **TestData**, e seu esquema padrão é **db_datareader**, a tabela é criada com o nome `<database_name>.db_datareader.TestData`.
  
    Por esse motivo, um banco de dados pode conter várias tabelas com o mesmo nome, desde que as tabelas pertençam a esquemas diferentes.
   
    Se você estiver procurando por uma tabela e não especificar um esquema, o servidor de banco de dados procurará um esquema que você possui. Portanto, não é necessário especificar o nome do esquema ao acessar tabelas em um esquema associado ao seu logon.
  
- **Não tenho privilégios DDL. Ainda posso executar o tutorial**?
  
    Sim, mas você deve pedir que alguém pré-carregue os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas e vá em frente para a próxima lição. As funções que exigem privilégios DDL são destacadas no tutorial sempre que possível.

    Além disso, solicite ao administrador para conceder permissão, EXECUTE ANY EXTERNAL SCRIPT. Ela é necessária para execução do script R, se for remoto, ou usando `sp_execute_external_script`.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar objetos de dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)