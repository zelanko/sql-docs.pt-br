---
title: sysmail_update_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4be8c0c87771f89d92cc0344c207149467c4554c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as informações em uma conta existente do Database Mail.  
 
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@account_id** = ] *account_id*  
 A ID da conta a ser atualizada. *account_id* é **int**, com um padrão NULL. Pelo menos uma das *account_id* ou *account_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
 [ **@account_name** = ] **'***account_name***'**  
 O nome da conta a ser atualizada. *account_name* é **sysname**, com um padrão NULL. Pelo menos uma das *account_id* ou *account_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
 [ **@email_address** = ] **'***email_address***'**  
 O novo endereço de email a partir do qual a mensagem será enviada. Esse endereço deve ser um endereço de email na Internet. O nome do servidor no endereço é o servidor que o Database Mail usa para enviar email dessa conta. *endereço de email* é **nvarchar (128)**, com um padrão NULL.  
  
 [ **@display_name** = ] **'***display_name***'**  
 O novo nome para exibição a ser usado em mensagens de email enviadas por essa conta. *display_name* é **nvarchar (128)**, sem padrão.  
  
 [ **@replyto_address** = ] **'***replyto_address***'**  
 O novo endereço a ser usado no cabeçalho Responder das mensagens de email desta conta. *replyto_address* é **nvarchar (128)**, sem padrão.  
  
 [  **@description**  =] **'***descrição***'**  
 A nova descrição da conta. *Descrição* é **nvarchar (256)**, com um padrão NULL.  
  
 [ **@mailserver_name** = ] **'***server_name***'**  
 O novo nome do servidor de email SMTP a ser usado para essa conta. O computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de resolver o *nome_do_servidor* para um endereço IP. *server_name* é **sysname**, sem padrão.  
  
 [ **@mailserver_type** = ] **'***server_type***'**  
 O novo tipo do servidor de email. *server_type* é **sysname**, sem padrão. Apenas um valor de **'SMTP'** tem suporte.  
  
 [ **@port** = ] *port_number*  
 O novo número da porta do servidor de email. *port_number* é **int**, sem padrão.  
  
 [  **@timeout**  =] **'***tempo limite***'**  
 Parâmetro de tempo limite para SmtpClient.Send de uma única mensagem de email. *Tempo limite* é **int** em segundos, sem padrão.  
  
 [ **@username** = ] **'***username***'**  
 O novo nome do usuário a ser usado para fazer logon no servidor de email. *Nome de usuário* é **sysname**, sem padrão.  
  
 [ **@password** = ] **'***password***'**  
 A nova senha a ser usado para fazer logon no servidor de email. *senha* é **sysname**, sem padrão.  
  
 [ **@use_default_credentials** = ] use_default_credentials  
 Especifica se o email deve ser enviado ao servidor SMTP com as credenciais do serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** é bit, sem padrão. Quando este parâmetro for 1, o Database Mail usará as credenciais do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando esse parâmetro é 0, o Database Mail usa o  **@username**  e  **@password**  para autenticação no servidor SMTP. Se  **@username**  e  **@password**  forem NULL, ele usará a autenticação anônima. Consulte o administrador de SMTP antes de especificar este parâmetro.  
  
 [  **@enable_ssl**  =] enable_ssl  
 Especifica se o Database Mail criptografa a comunicação usando o Protocolo SSL. Use esta opção se o SSL for exigido em seu servidor SMTP. **enable_ssl** é bit, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Quando o nome e a identificação da conta são especificados, o procedimento armazenado altera o nome da conta além de atualizar as informações da conta. A alteração do nome da conta pode ser útil para corrigir erros que existam nela.  
  
 O procedimento armazenado **sysmail_update_account_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-information-for-an-account"></a>A. Alterando as informações de uma conta  
 O exemplo a seguir atualiza a conta `AdventureWorks Administrator` no **msdb** banco de dados. As informações da conta são definidas com os valores fornecidos.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. Alterando o nome de uma conta e as informações de uma conta  
 O exemplo a seguir altera o nome e atualiza as informações da conta com a identificação de conta `125`. O novo nome da conta é `Backup Mail Server`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Armazenados do Database Mail procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
