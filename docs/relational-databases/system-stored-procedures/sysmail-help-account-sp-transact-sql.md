---
title: sysmail_help_account_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
caps.latest.revision: "48"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfc032a279abad7949e67f4c232cbe30219baa30
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailhelpaccountsp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações (exceto senhas) sobre contas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@account_id**  =] *account_id*  
 A ID da conta para a qual as informações serão listadas. *account_id* é **int**, com um padrão NULL.  
  
 [  **@account_name**  =] **'***account_name***'**  
 O nome da conta para a qual listar informações. *account_name* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que contém as colunas listadas a seguir.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Description|  
|**account_id**|**int**|O ID da conta.|  
|**name**|**sysname**|O nome da conta.|  
|**Descrição**|**nvarchar(256)**|A descrição da conta.|  
|**endereço de email**|**nvarchar (128)**|O endereço de email a partir do qual as mensagens serão enviadas.|  
|**display_name**|**nvarchar (128)**|O nome para exibição da conta.|  
|**replyto_address**|**nvarchar (128)**|O endereço onde as respostas às mensagens desta conta são enviadas.|  
|**tipo do servidor**|**sysname**|O tipo de servidor de email da conta.|  
|**nome do servidor**|**sysname**|O nome do servidor de email da conta.|  
|**port**|**int**|O número da porta usada pelo servidor de email.|  
|**nome de usuário**|**nvarchar (128)**|O nome de usuário a ser usado para fazer logon no servidor de email, se o servidor de email usar autenticação. Quando **username** for NULL, o Database Mail não usa autenticação para esta conta.|  
|**use_default_credentials**|**bit**|Especifica se o email deve ser enviado ao servidor SMTP com as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** é bit, sem padrão. Quando este parâmetro for 1, o Database Mail usa as credenciais do serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando esse parâmetro é 0, o Database Mail usa o  **@username**  e  **@password**  para autenticação no servidor SMTP. Se  **@username**  e  **@password**  forem NULL, o Database Mail usa a autenticação anônima. Consulte o administrador de SMTP antes de especificar esse parâmetro.|  
|**enable_ssl**|**bit**|Especifica se o Database Mail criptografa a comunicação usando o Protocolo SSL. Use esta opção se o SSL for exigido em seu servidor SMTP. **enable_ssl** é bit, sem padrão. 1 indica que o Database Mail criptografa a comunicação usando SSL. 0 indica que o Database Mail envia o email sem criptografia SSL.|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum *account_id* ou *account_name* for fornecido, **sysmail_help_account** lista informações sobre todas as contas do Database Mail na instância do Microsoft SQL Server.  
  
 O procedimento armazenado **sysmail_help_account_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Listando informações para todas as contas**  
  
 O exemplo a seguir mostra a lista de informações de conta para todas as contas na instância.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. Listando as informações de uma conta específica**  
  
 O exemplo a seguir mostra a lista de informações de conta para a conta denominada `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Armazenados do Database Mail procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
