---
title: Criar um perfil do Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 667dbd4e0b323f50721af716a30709ba9ea6d5c8
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49071810"
---
# <a name="create-a-database-mail-profile"></a>Criar um perfil do Database Mail
  Use o **Assistente para Configuração do Database Mail** ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar perfis públicos e privados do Database Mail.  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Crie uma ou mais contas do Database Mail para o perfil. Para obter mais informações sobre como criar o Database Mail, veja [Criar uma conta do Database Mail](create-a-database-mail-account.md).  
  
###  <a name="Security"></a> Segurança  
 Um perfil público permite a qualquer usuário acessar o banco de dados **msdb** para enviar emails usando o perfil. Um perfil particular pode ser usado por um usuário ou por uma função. Conceder a funções o acesso a perfis cria uma arquitetura de mais fácil manutenção. Para enviar emails, você deve ser membro da função **DatabaseMailUserRole** no banco de dados **msdb** e ter acesso a pelo menos um perfil do Database Mail.  
  
####  <a name="Permissions"></a> Permissões  
 O usuário que cria as contas de perfis e executa procedimentos armazenados deve ser membro da função de servidor fixa sysadmin.  
  

  
##  <a name="SSMSProcedure"></a> Usando o assistente para configuração do Database Mail  
 **Para criar um perfil do Database Mail**  
  
-   No Pesquisador de Objetos, conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usada para configurar o Database Mail e expanda a árvore de servidores.  
  
-   Expanda o nó **Gerenciamento** .  
  
-   Clique duas vezes em Database Mail para abrir o Assistente de Configuração do Database Mail.  
  
-   Na página **Selecionar Tarefa de Configuração** , selecione a opção **Gerenciar contas e perfis do Database Mail** e clique em **Avançar**.  
  
-   Na página **Gerenciar Perfis e Contas** , selecione a opção **Criar um novo perfil** e clique em **Avançar**.  
  
-   Na página **Novo Perfil** , especifique o nome do Perfil, a Descrição e adicione contas a serem incluídas no perfil; depois, clique em **Avançar**.  
  
-   Na página **Concluir o Assistente** , examine as ações a serem executadas e clique em **Concluir** para concluir a criação de um novo perfil.  
  
-   **Para configurar um perfil privado do Database Mail:**  
  
    -   Abra o Assistente para Configuração do Database Mail.  
  
    -   Na página **Selecionar Tarefa de Configuração** , selecione a opção **Gerenciar contas e perfis do Database Mail** e clique em **Avançar**.  
  
    -   Na página **Gerenciar Perfis e Contas** , selecione a opção **Gerenciar segurança do perfil** e clique em **Avançar**.  
  
    -   Na guia **Perfis Privados** , marque a caixa de seleção do perfil a ser configurado e clique em **Avançar**.  
  
    -   Na página **Concluir o Assistente** , examine as ações a serem executadas e clique em **Concluir** para concluir a configuração do perfil.  
  
-   **Para configurar um perfil público do Database Mail:**  
  
    -   Abra o Assistente para Configuração do Database Mail.  
  
    -   Na página **Selecionar Tarefa de Configuração** , selecione a opção **Gerenciar contas e perfis do Database Mail** e clique em **Avançar**.  
  
    -   Na página **Gerenciar Perfis e Contas** , selecione a opção **Gerenciar segurança do perfil** e clique em **Avançar**.  
  
    -   Na guia **Perfis Públicos** , marque a caixa de seleção do perfil a ser configurado e clique em **Avançar**.  
  
    -   Na página **Concluir o Assistente** , examine as ações a serem executadas e clique em **Concluir** para concluir a configuração do perfil.  
  

  
## <a name="using-transact-sql"></a>Usando Transact-SQL  
  
###  <a name="PrivateProfile"></a> Para criar um perfil privado do Database Mail  
  
-   Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para criar um novo perfil, execute o procedimento armazenado no sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Nome do Perfil*'  
  
     *@description* = '*Descrição*'  
  
     em que *@profile_name* é o nome do perfil e *@description* é a descrição do perfil. Esse parâmetro é opcional.  
  
-   Para cada conta, execute o procedimento armazenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@account_name* = '*Nome da conta*'  
  
     *@sequence_number* = '*número de sequência da conta dentro do perfil.* '  
  
     em que *@profile_name* é o nome do perfil e *@account_name* é o nome da conta a ser adicionada ao perfil e *@sequence_number* determina a ordem na qual as contas são usadas no perfil.  
  
-   Para cada função de banco de dados ou usuário que enviará email usando este perfil, conceda acesso ao perfil. Para fazer isso, execute o procedimento armazenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@ principal_name* = “*Nome de usuário de banco de dados ou função*”  
  
     *@is_default* = '*Status de perfil padrão* '  
  
     em que *@profile_name* é o nome do perfil e *@principal_name* é o nome do usuário ou função de banco de dados e *@is_default* determina se esse perfil é o padrão para o usuário ou a função de banco de dados.  
  
 O exemplo a seguir cria uma conta do Database Mail, cria um perfil privado do Database Mail, adiciona a conta ao perfil e concede acesso ao perfil à função de banco de dados **DBMailUsers** no banco de dados **msdb** .  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
 
  
###  <a name="PublicProfile"></a> Para criar um perfil público do Database Mail  
  
-   Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para criar um novo perfil, execute o procedimento armazenado no sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Nome do Perfil*'  
  
     *@description* = '*Descrição*'  
  
     em que *@profile_name* é o nome do perfil e *@description* é a descrição do perfil. Esse parâmetro é opcional.  
  
-   Para cada conta, execute o procedimento armazenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@account_name* = '*Nome da conta*'  
  
     *@sequence_number* = '*número de sequência da conta dentro do perfil.* '  
  
     em que *@profile_name* é o nome do perfil e *@account_name* é o nome da conta a ser adicionada ao perfil e *@sequence_number* determina a ordem na qual as contas são usadas no perfil.  
  
-   Para conceder acesso público, execute o procedimento armazenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) da seguinte forma:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@ principal_name* = '**público** ou **0**'  
  
     *@is_default* = '*Status de perfil padrão* '  
  
     em que *@profile_name* é o nome do perfil, e *@principal_name* para indicar que este é um perfil público, *@is_default* determina se este perfil é o padrão para o banco de dados usuário ou função.  
  
 O exemplo a seguir cria uma conta do Database Mail, cria um perfil privado do Database Mail, adiciona a conta ao perfil e concede acesso público ao perfil.  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  

  
  
