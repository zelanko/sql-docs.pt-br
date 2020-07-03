---
title: sysmail_update_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4d50c251d2486b53611c2f2fccfc7e8c2bfa352d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890841"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera as informações em uma conta existente do Database Mail.  
 
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @account_id = ] account_id`A ID da conta a ser atualizada. *account_id* é **int**, com um padrão de NULL. Pelo menos um dos *account_id* ou *account_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
`[ @account_name = ] 'account_name'`O nome da conta a ser atualizada. *account_name* é **sysname**, com um padrão de NULL. Pelo menos um dos *account_id* ou *account_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
`[ @email_address = ] 'email_address'`O novo endereço de email do qual enviar a mensagem. Esse endereço deve ser um endereço de email na Internet. O nome do servidor no endereço é o servidor que o Database Mail usa para enviar email dessa conta. *email_address* é **nvarchar (128)**, com um padrão de NULL.  
  
`[ @display_name = ] 'display_name'`O novo nome de exibição a ser usado em mensagens de email desta conta. *display_name* é **nvarchar (128)**, sem padrão.  
  
`[ @replyto_address = ] 'replyto_address'`O novo endereço a ser usado no cabeçalho de resposta de mensagens de email dessa conta. *replyto_address* é **nvarchar (128)**, sem padrão.  
  
`[ @description = ] 'description'`A nova descrição da conta. a *Descrição* é **nvarchar (256)**, com um padrão de NULL.  
  
`[ @mailserver_name = ] 'server_name'`O novo nome do servidor de email SMTP a ser usado para essa conta. O computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de resolver o *server_name* para um endereço IP. *server_name* é **sysname**, sem padrão.  
  
`[ @mailserver_type = ] 'server_type'`O novo tipo do servidor de email. *server_type* é **sysname**, sem padrão. Somente um valor de **' SMTP '** tem suporte.  
  
`[ @port = ] port_number`O novo número de porta do servidor de email. *port_number* é **int**, sem padrão.  
  
`[ @timeout = ] 'timeout'`Parâmetro Timeout para SmtpClient. Send de uma única mensagem de email. O *tempo limite* é **int** em segundos, sem padrão.  
  
`[ @username = ] 'username'`O novo nome de usuário a ser usado para fazer logon no servidor de email. O *nome de usuário* é **sysname**, sem padrão.  
  
`[ @password = ] 'password'`A nova senha a ser usada para fazer logon no servidor de email. a *senha* é **sysname**, sem padrão.  
  
`[ @use_default_credentials = ] use_default_credentials`Especifica se o email deve ser enviado ao servidor SMTP usando as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] serviço. **use_default_credentials** é bit, sem padrão. Quando este parâmetro for 1, o Database Mail usará as credenciais do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando esse parâmetro for 0, Database Mail usará o ** \@ nome de usuário** e a ** \@ senha** para autenticação no servidor SMTP. Se o ** \@ nome de usuário** e a ** \@ senha** forem nulos, ele usará a autenticação anônima. Consulte o administrador de SMTP antes de especificar este parâmetro.  
  
`[ @enable_ssl = ] enable_ssl`Especifica se Database Mail criptografa a comunicação usando TLS (segurança de camada de transporte), anteriormente conhecido como protocolo SSL (SSL). Use esta opção se o TLS for necessário no servidor SMTP. **Enable_ssl** é bit, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o nome e a identificação da conta são especificados, o procedimento armazenado altera o nome da conta além de atualizar as informações da conta. A alteração do nome da conta pode ser útil para corrigir erros que existam nela.  
  
 O procedimento armazenado **sysmail_update_account_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-information-for-an-account"></a>a. Alterando as informações de uma conta  
 O exemplo a seguir atualiza a conta `AdventureWorks Administrator` no banco de dados **msdb** . As informações da conta são definidas com os valores fornecidos.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
