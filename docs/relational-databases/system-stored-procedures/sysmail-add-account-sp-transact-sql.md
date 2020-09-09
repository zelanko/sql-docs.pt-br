---
description: sysmail_add_account_sp (Transact-SQL)
title: sysmail_add_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 85625e9b8e5a3c1acf5bbc8152b90789f33665ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551079"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria uma nova conta do Database Mail que contém informações sobre uma conta SMTP.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @account_name = ] 'account_name'` O nome da conta a ser adicionada. *account_name* é **sysname**, sem padrão.  
  
`[ @email_address = ] 'email_address'` O endereço de email do qual enviar a mensagem. Esse endereço deve ser um endereço de email na Internet. *email_address* é **nvarchar (128)**, sem padrão. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode enviar email do endereço **sqlagent \@ Adventure-Works.com**.  
  
`[ @display_name = ] 'display_name'` O nome de exibição a ser usado em mensagens de email desta conta. *display_name* é **nvarchar (128)**, com um padrão de NULL. Por exemplo, uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode exibir o nome **SQL Server Agent mensageiro automatizado** em mensagens de email.  
  
`[ @replyto_address = ] 'replyto_address'` O endereço para o qual as respostas a mensagens dessa conta são enviadas. *replyto_address* é **nvarchar (128)**, com um padrão de NULL. Por exemplo, as respostas a uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent podem ir para o administrador do banco de dados, **danw \@ Adventure-Works.com**.  
  
`[ @description = ] 'description'` É uma descrição para a conta. a *Descrição* é **nvarchar (256)**, com um padrão de NULL.  
  
`[ @mailserver_name = ] 'server_name'` O nome ou endereço IP do servidor de email SMTP a ser usado para essa conta. O computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de resolver o *server_name* para um endereço IP. *server_name* é **sysname**, sem padrão.  
  
`[ @mailserver_type = ] 'server_type'` O tipo de servidor de email. *server_type* é **sysname**, com um padrão de **' SMTP '**..  
  
`[ @port = ] port_number` O número da porta do servidor de email. *port_number* é **int**, com um padrão de 25.  
  
`[ @username = ] 'username'` O nome de usuário a ser usado para fazer logon no servidor de email. *username* é **nvarchar (128)**, com um padrão de NULL. Quando este parâmetro for NULL, o Database Mail não usa autenticação para esta conta. Se o servidor de email não requerer autenticação, use NULL para o nome de usuário.  
  
`[ @password = ] 'password'` A senha a ser usada para fazer logon no servidor de email. a *senha* é **nvarchar (128)**, com um padrão de NULL. Não há necessidade em fornecer uma senha, a menos que um nome de usuário seja especificado.  
  
`[ @use_default_credentials = ] use_default_credentials` Especifica se o email deve ser enviado ao servidor SMTP usando as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . **use_default_credentials** é bit, com um padrão de 0. Quando este parâmetro for 1, o Database Mail usará as credenciais do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando esse parâmetro for 0, Database Mail enviará os parâmetros de ** \@ nome de usuário** e ** \@ senha** , se estiverem presentes, caso contrário, enviará mensagens sem parâmetros de ** \@ nome de usuário** e ** \@ senha** .  
  
`[ @enable_ssl = ] enable_ssl` Especifica se Database Mail criptografa a comunicação usando protocolo SSL. **Enable_ssl** é bit, com um padrão de 0.  
  
`[ @account_id = ] account_id OUTPUT` Retorna a ID da conta para a nova conta. *account_id* é **int**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Database Mail fornece parâmetros separados para ** \@ email_address**, ** \@ display_name**e ** \@ replyto_address**. O parâmetro ** \@ email_address** é o endereço do qual a mensagem é enviada. O parâmetro ** \@ display_name** é o nome mostrado no campo **de:** da mensagem de email. O parâmetro ** \@ replyto_address** é o endereço em que as respostas para a mensagem de email serão enviadas. Por exemplo, uma conta usada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode enviar mensagens de email a partir de um endereço de email usado apenas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. As mensagens desse endereço devem exibir um nome amigável, de maneira que os destinatários possam determinar facilmente que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent enviou a mensagem. Se um destinatário responder à mensagem, a resposta deve ir para o administrador do banco de dados, em vez do endereço usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para esse cenário, a conta usa **SqlAgent@Adventure-Works.com** como o endereço de email. O nome de exibição é definido como **SQL Server Agent mensageiro automatizado**. A conta usa **danw@Adventure-Works.com** como o endereço de resposta para, portanto, as respostas às mensagens enviadas dessa conta vão para o administrador de banco de dados em vez do endereço de email do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Ao fornecer configurações independentes para esses três parâmetros, o Database Mail permite configurar mensagens adequadas às suas necessidades.  
  
 O parâmetro ** \@ mailserver_type** dá suporte ao valor **' SMTP '**.  
  
 Quando ** \@ use_default_credentials** é 1 email é enviado ao servidor SMTP usando as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Quando ** \@ use_default_credentials** é 0 e um ** \@ nome de usuário** e ** \@ senha** são especificados para uma conta, a conta usa a autenticação SMTP. O ** \@ nome de usuário** e a ** \@ senha** são as credenciais que a conta usa para o servidor SMTP, não para as credenciais [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para a rede em que o computador está.  
  
 O procedimento armazenado **sysmail_add_account_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma conta denominada `AdventureWorks Administrator`. A conta usa o endereço de email `dba@Adventure-Works.com` e envia correio ao servidor de email SMTP `smtp.Adventure-Works.com`. As mensagens de email enviadas desta conta são mostradas `AdventureWorks Automated Mailer` na linha **de:** da mensagem. As respostas às mensagens são direcionadas para `danw@Adventure-Works.com`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
