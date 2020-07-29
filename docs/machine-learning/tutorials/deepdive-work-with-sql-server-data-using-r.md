---
title: Banco de dados para tutoriais do RevoScaleR
description: 'Tutorial 1 do RevoScaleR: Como criar um banco de dados do SQL Server para tutoriais de R.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5cd0d5e6706dc946ba5be34487edb72e4cbf996b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757123"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Criar um banco de dados e permissões (tutorial de SQL Server e RevoScaleR)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este é o tutorial 1 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Este tutorial descreve como criar um banco de dados SQL Server e definir as permissões necessárias para concluir os outros tutoriais nesta série. Use o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outro editor de consultas para concluir as seguintes tarefas:

> [!div class="checklist"]
> * Criar um novo banco de dados para armazenar os dados de treinamento e pontuação dos dois modelos do R
> * Criar um logon de usuário de banco de dados com permissões para criar e usar objetos de banco de dados
  
## <a name="create-the-database"></a>Criar o banco de dados

Este tutorial requer um banco de dados para o armazenamento de dados e código. Se você não for um administrador, peça ao DBA para criar o banco de dados e o logon para você. Você precisará de permissões para gravar e ler dados e para executar scripts do R.

1. No SQL Server Management Studio, conecte-se a uma instância do banco de dados habilitada para R.

2. Clique com o botão direito do mouse em **Bancos de dados**e selecione **Novo banco de dados**.
  
2. Digite um nome para o novo banco de dados: RevoDeepDive.
  
## <a name="create-a-login"></a>Criar um logon
  
1. Clique em **Nova Consulta**e altere o contexto do banco de dados mestre.
  
2. Na janela **Nova consulta** , execute os comandos a seguir para criar as contas de usuário e atribuí-las ao banco de dados usado neste tutorial. Lembre-se de alterar o nome do banco de dados, se necessário.

3. Para confirmar o logon, selecione o novo banco de dados, expanda **Segurança**e expanda **Usuários**.
  
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

Este tutorial demonstra o script R e as operações DDL, incluindo a criação e exclusão de tabelas e procedimentos armazenados e a execução do script R em um processo externo no SQL Server. Nesta etapa, atribua permissões para permitir essas tarefas.

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
  
    Os motivos comuns para falhas de conexão incluem conexões remotas não habilitadas para o servidor e o protocolo de Pipes Nomeados não habilitado. Você pode encontrar mais dicas de solução de problemas neste artigo: [Solucionar problemas na conexão com o Mecanismo de Banco de Dados do SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **O nome de minha tabela tem datareader como prefixo. Por quê?**
  
    Ao especificar o esquema padrão para esse usuário como **db_datareader**, todas as tabelas e outros novos objetos criados por esse usuário são prefixados com o nome do *esquema*. Um esquema é como uma pasta que você pode adicionar a um banco de dados para organizar objetos. O esquema também define os privilégios de um usuário no banco de dados.
  
    Quando o esquema é associado a um nome de usuário específico, o usuário é o _proprietário do esquema_. Quando você cria um objeto, você sempre o cria em seu próprio esquema, a menos que você solicite especificamente que ele seja criado em outro esquema.
  
    Por exemplo, se você criar uma tabela com o nome **TestData** e o esquema padrão for **db_datareader**, a tabela será criada com o nome `<database_name>.db_datareader.TestData`.
  
    Por esse motivo, um banco de dados pode conter várias tabelas com o mesmo nome, desde que as tabelas pertençam a esquemas diferentes.
   
    Se você estiver procurando uma tabela e não especificar um esquema, o servidor de banco de dados procurará um esquema seu. Portanto, não é necessário especificar o nome do esquema ao acessar tabelas em um esquema associado ao seu logon.
  
- **Não tenho privilégios DDL. Ainda posso executar o tutorial**?
  
    Sim, mas você deve pedir a alguém para pré-carregar os dados nas tabelas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e avançar para o próximo tutorial. As funções que exigem privilégios DDL são indicadas no tutorial sempre que possível.

    Além disso, peça ao administrador para conceder a você a permissão EXECUTE ANY EXTERNAL SCRIPT. Ela é necessária para a execução do script do R, seja remoto ou usando `sp_execute_external_script`.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar objetos de dados do SQL Server usando RxSqlServerData](../../machine-learning/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)