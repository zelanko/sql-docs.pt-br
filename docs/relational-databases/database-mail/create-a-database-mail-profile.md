---
title: "Criar um perfil do Database Mail | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Database Mail [SQL Server], perfis públicos"
  - "perfis [SQL Server], Database Mail"
  - "perfis públicos [Database Mail]"
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
caps.latest.revision: 34
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 34
---
# Criar um perfil do Database Mail
  Use o **Assistente para Configuração do Database Mail** ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar perfis públicos e privados do Database Mail. Para obter mais informações sobre perfis de email, consulte [Perfil do Database Mail](https://msdn.microsoft.com/library/ms175100.aspx#Anchor_2).
  
-   **Antes de começar:** [Pré-requisitos](#Prerequisites), , [Segurança](#Security)  
  
-   **Para criar um perfil privado do Database Mail usando:** [Assistente de Configuração do Database Mail](#SSMSProcedure), [Transact-SQL](#PrivateProfile)  
  
-   **Para criar um perfil público do Database Mail usando:** [Assistente de Configuração do Database Mail](#SSMSProcedure), [Transact-SQL](#PublicProfile)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Crie uma ou mais contas do Database Mail para o perfil. Para obter mais informações sobre como criar o Database Mail, veja [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md).  
  
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
  
## Usando Transact-SQL  
  
###  <a name="PrivateProfile"></a> Para criar um perfil privado do Database Mail  
  
-   Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para criar um novo perfil, execute o procedimento armazenado no sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Nome do Perfil*'  
  
     *@description* = '*Descrição*'  
  
     em que *@profile_name* é o nome do perfil e *@description* é a descrição do perfil. Esse parâmetro é opcional.  
  
-   Para cada conta, execute o procedimento armazenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@account_name* = '*Nome da conta*'  
  
     *@sequence_number* = '*número de sequência da conta dentro do perfil.* '  
  
     em que *@profile_name* é o nome do perfil, *@account_name* é o nome da conta a ser adicionada ao perfil e *@sequence_number* determina a ordem na qual as contas são usadas no perfil.  
  
-   Para cada função de banco de dados ou usuário que enviará email usando este perfil, conceda acesso ao perfil. Para fazer isso, execute o procedimento armazenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@ principal_name* = “*Nome de usuário de banco de dados ou função*”  
  
     *@is_default* = '*Status de perfil padrão*'  
  
     em que *@profile_name* é o nome do perfil, *@principal_name* é o nome do usuário ou função de banco de dados e *@is_default* determina se esse perfil é o padrão para o usuário ou a função de banco de dados.  
  
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
  
-   Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para criar um novo perfil, execute o procedimento armazenado no sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Nome do Perfil*'  
  
     *@description* = '*Descrição*'  
  
     em que *@profile_name* é o nome do perfil e *@description* é a descrição do perfil. Esse parâmetro é opcional.  
  
-   Para cada conta, execute o procedimento armazenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@account_name* = '*Nome da conta*'  
  
     *@sequence_number* = '*número de sequência da conta dentro do perfil.* '  
  
     em que *@profile_name* é o nome do perfil, *@account_name* é o nome da conta a ser adicionada ao perfil e *@sequence_number* determina a ordem na qual as contas são usadas no perfil.  
  
-   Para conceder acesso público, execute o procedimento armazenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md) da seguinte forma:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Nome do perfil*'  
  
     *@ principal_name* = '**público** ou **0**'  
  
     *@is_default* = '*Status de perfil padrão*'  
  
     em que *@profile_name* é o nome do perfil, *@principal_name* indica que este é um perfil público e *@is_default* determina se esse perfil é o padrão para o usuário ou a função de banco de dados.  
  
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
  
  