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
ms.openlocfilehash: 3dd772a1519ea856cac0302d31be9eb7d0f9d782
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283074"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @account_id = ] account_id`O ID da conta para atualizar. *account_id* é **int**, com um padrão de NULL. Pelo menos uma de *account_id* ou *account_name* deve ser especificada. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
`[ @account_name = ] 'account_name'`O nome da conta para atualizar. *account_name* é **sysname,** com um padrão de NULL. Pelo menos uma de *account_id* ou *account_name* deve ser especificada. Se ambos forem especificados, o procedimento alterará o nome da conta.  
  
`[ @email_address = ] 'email_address'`O novo endereço de e-mail para enviar a mensagem de. Esse endereço deve ser um endereço de email na Internet. O nome do servidor no endereço é o servidor que o Database Mail usa para enviar email dessa conta. *email_address* é **nvarchar(128)**, com um padrão de NULL.  
  
`[ @display_name = ] 'display_name'`O novo nome de exibição a ser usado em mensagens de e-mail desta conta. *display_name* é **nvarchar(128)**, sem padrão.  
  
`[ @replyto_address = ] 'replyto_address'`O novo endereço a ser usado no cabeçalho De Resposta para e-mail de mensagens de e-mail desta conta. *replyto_address* é **nvarchar(128)**, sem padrão.  
  
`[ @description = ] 'description'`A nova descrição da conta. *descrição* **é nvarchar(256)**, com um padrão de NULL.  
  
`[ @mailserver_name = ] 'server_name'`O novo nome do servidor de e-mail SMTP para usar nesta conta. O computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é executado deve ser capaz de resolver o *server_name* para um endereço IP. *server_name* **é sysname,** sem padrão.  
  
`[ @mailserver_type = ] 'server_type'`O novo tipo do servidor de correio. *server_type* **é sysname,** sem padrão. Apenas um valor de **'SMTP'** é suportado.  
  
`[ @port = ] port_number`O novo número de porta do servidor de e-mail. *port_number* é **int,** sem inadimplência.  
  
`[ @timeout = ] 'timeout'`Parâmetro de tempo para SmtpClient.Enviar uma única mensagem de e-mail. *O tempo int* **é int** em segundos, sem padrão.  
  
`[ @username = ] 'username'`O novo nome de usuário para usar para fazer logon no servidor de e-mail. *O nome* de usuário **é sysname**, sem padrão.  
  
`[ @password = ] 'password'`A nova senha para usar para fazer logon no servidor de e-mail. *senha* é **sysname,** sem padrão.  
  
`[ @use_default_credentials = ] use_default_credentials`Especifica se deve enviar o e-mail para o servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] SMTP usando as credenciais do serviço. **use_default_credentials** é pouco, sem padrão. Quando este parâmetro for 1, o Database Mail usará as credenciais do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando este parâmetro é 0, o Database Mail usa o ** \@nome de usuário** e ** \@** a senha para autenticação no servidor SMTP. Se ** \@o nome de usuário** e ** \@a senha** forem NULL, ele usará autenticação anônima. Consulte o administrador de SMTP antes de especificar este parâmetro.  
  
`[ @enable_ssl = ] enable_ssl`Especifica se o Database Mail criptografa a comunicação usando o TLS (Transport Layer Security, segurança de camada de transporte), anteriormente conhecido como Secure Sockets Layer (SSL). Use esta opção se o TLS for necessário no servidor SMTP. **enable_ssl** é pouco, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (sucesso) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o nome e a identificação da conta são especificados, o procedimento armazenado altera o nome da conta além de atualizar as informações da conta. A alteração do nome da conta pode ser útil para corrigir erros que existam nela.  
  
 O procedimento armazenado **sysmail_update_account_sp** está no banco de dados do **MSDB** e pertence ao esquema **dbo.** O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Requer a adesão na função de servidor fixo **sysadmin.**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-information-for-an-account"></a>a. Alterando as informações de uma conta  
 O exemplo a seguir `AdventureWorks Administrator` atualiza a conta no banco de dados do **msdb.** As informações da conta são definidas com os valores fornecidos.  
  
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
 [Correio de banco de dados](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de correio de banco de dados](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimentos armazenados de correio de banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
