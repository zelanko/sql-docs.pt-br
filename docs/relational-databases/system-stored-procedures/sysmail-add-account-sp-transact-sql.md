---
title: sysmail_add_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e24d90b20c91ab6dfb510faad46ceb2b5f8cc19b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma nova conta do Database Mail que contém informações sobre uma conta SMTP.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@account_name**  =] **'***account_name***'**  
 O nome da conta a ser adicionada. *account_name* é **sysname**, sem padrão.  
  
 [  **@email_address**  =] **'***email_address***'**  
 O endereço de email a partir do qual a mensagem será enviada. Esse endereço deve ser um endereço de email na Internet. *endereço de email* é **nvarchar (128)**, sem padrão. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode enviar email do endereço  **SqlAgent@Adventure-Works.com** .  
  
 [  **@display_name**  =] **'***display_name***'**  
 O nome para exibição a ser usado em mensagens de email enviadas por essa conta. *display_name* é **nvarchar (128)**, com um padrão NULL. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode exibir o nome **SQL Server Agent Automated Mailer** em mensagens de email.  
  
 [  **@replyto_address**  =] **'***replyto_address***'**  
 O endereço para o qual as respostas às mensagens dessa conta são enviadas. *replyto_address* é **nvarchar (128)**, com um padrão NULL. Por exemplo, respostas para uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent podem ir para o administrador de banco de dados,  **danw@Adventure-Works.com** .  
  
 [  **@description**  =] **'***descrição***'**  
 É uma descrição da conta. *Descrição* é **nvarchar (256)**, com um padrão NULL.  
  
 [  **@mailserver_name**  =] **'***nome_do_servidor***'**  
 O nome ou o endereço IP do servidor de email SMTP a ser usado para esta conta. O computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de resolver o *nome_do_servidor* para um endereço IP. *server_name* é **sysname**, sem padrão.  
  
 [  **@mailserver_type**  =] '*server_type*'  
 O tipo de servidor de email. *server_type* é **sysname**, com um padrão de **'SMTP'**...  
  
 [  **@port**  =] *port_number*  
 O número de porta do servidor de email. *port_number* é **int**, com um padrão de 25.  
  
 [  **@username**  =] **'***username***'**  
 O novo nome de usuário a ser usado para fazer logon no servidor de email. *nome de usuário* é **nvarchar (128)**, com um padrão NULL. Quando este parâmetro for NULL, o Database Mail não usa autenticação para esta conta. Se o servidor de email não requerer autenticação, use NULL para o nome de usuário.  
  
 [  **@password**  =] **'***senha***'**  
 A nova senha a ser usada para fazer logon no servidor de email. *senha* é **nvarchar (128)**, com um padrão NULL. Não há necessidade em fornecer uma senha, a menos que um nome de usuário seja especificado.  
  
 [  **@use_default_credentials**  =] use_default_credentials  
 Especifica se o email deve ser enviado ao servidor SMTP com as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** é bit, com um padrão de 0. Quando este parâmetro for 1, o Database Mail usará as credenciais do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando esse parâmetro é 0, o Database Mail envia o  **@username**  e  **@password**  parâmetros se estiver presente, caso contrário, envia email sem  **@username** e  **@password**  parâmetros.  
  
 [  **@enable_ssl**  =] enable_ssl  
 Especifica se o Database Mail criptografa a comunicação usando o protocolo SSL. **Enable_ssl** é bit, com um padrão de 0.  
  
 [  **@account_id**  =] *account_id* saída  
 Retorna a ID da nova conta. *account_id* é **int**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 O Database Mail fornece parâmetros separados para  **@email_address** ,  **@display_name** , e  **@replyto_address** . O  **@email_address**  parâmetro é o endereço do qual a mensagem é enviada. O  **@display_name**  parâmetro é o nome exibido no **de:** campo da mensagem de email. O  **@replyto_address**  parâmetro é o endereço onde respostas à mensagem de email serão enviadas. Por exemplo, uma conta usada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode enviar mensagens de email a partir de um endereço de email usado apenas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. As mensagens desse endereço devem exibir um nome amigável, de maneira que os destinatários possam determinar facilmente que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent enviou a mensagem. Se um destinatário responder à mensagem, a resposta deve ir para o administrador do banco de dados, em vez do endereço usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para este cenário, a conta usa  **SqlAgent@Adventure-Works.com**  como o endereço de email. O nome de exibição é definido como **SQL Server Agent Automated Mailer**. A conta usa  **danw@Adventure-Works.com**  como a resposta para o endereço, portanto as respostas às mensagens enviadas desta conta ir para o administrador de banco de dados em vez do endereço de email para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Ao fornecer configurações independentes para esses três parâmetros, o Database Mail permite configurar mensagens adequadas às suas necessidades.  
  
 O  **@mailserver_type**  parâmetro dá suporte ao valor **'SMTP'**.  
  
 Quando  **@use_default_credentials**  é 1, o email é enviado para o servidor SMTP usando as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando  **@use_default_credentials**  é 0 e um  **@username**  e  **@password**  especificado para uma conta, a conta usa autenticação SMTP. O  **@username**  e  **@password**  são as credenciais que usa a conta para o servidor SMTP, não as credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a rede que o computador está ligado.  
  
 O procedimento armazenado **sysmail_add_account_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma conta denominada `AdventureWorks Administrator`. A conta usa o endereço de email `dba@Adventure-Works.com` e envia correio ao servidor de email SMTP `smtp.Adventure-Works.com`. Mensagens de email enviadas desta conta mostram `AdventureWorks Automated Mailer` no **de:** linha da mensagem. As respostas às mensagens são direcionadas para `danw@Adventure-Works.com`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Armazenados do Database Mail procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
