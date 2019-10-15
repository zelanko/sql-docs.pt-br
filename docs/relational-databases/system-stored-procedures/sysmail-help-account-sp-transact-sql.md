---
title: sysmail_help_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 857e4139081833980ee6c90eca9d90d16d4c0ad2
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305148"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações (exceto senhas) sobre contas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_id = ] account_id` a ID da conta da qual listar informações. *account_id* é **int**, com um padrão de NULL.  
  
`[ @account_name = ] 'account_name'` o nome da conta para a qual listar informações. *account_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que contém as colunas listadas a seguir.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Descrição|  
|**account_id**|**int**|O ID da conta.|  
|**name**|**sysname**|O nome da conta.|  
|**description**|**nvarchar(256)**|A descrição da conta.|  
|**email_address**|**nvarchar(128)**|O endereço de email a partir do qual as mensagens serão enviadas.|  
|**display_name**|**nvarchar(128)**|O nome para exibição da conta.|  
|**replyto_address**|**nvarchar(128)**|O endereço onde as respostas às mensagens desta conta são enviadas.|  
|**servertype**|**sysname**|O tipo de servidor de email da conta.|  
|**servername**|**sysname**|O nome do servidor de email da conta.|  
|**port**|**int**|O número da porta usada pelo servidor de email.|  
|**username**|**nvarchar(128)**|O nome de usuário a ser usado para fazer logon no servidor de email, se o servidor de email usar autenticação. Quando **username** é nulo, Database Mail não usa a autenticação para essa conta.|  
|**use_default_credentials**|**bit**|Especifica se o email deve ser enviado ao servidor SMTP com as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** é bit, sem padrão. Quando este parâmetro for 1, o Database Mail usa as credenciais do serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando esse parâmetro é 0, Database Mail usa o **\@username** e **\@password** para autenticação no servidor SMTP. Se **\@username** e **\@password** forem nulos, Database Mail usará a autenticação anônima. Consulte o administrador do SMTP antes de especificar esse parâmetro.|  
|**enable_ssl**|**bit**|Especifica se o Database Mail criptografa a comunicação usando o Protocolo SSL. Use esta opção se o SSL for exigido em seu servidor SMTP. **Enable_ssl** é bit, sem padrão. 1 indica que o Database Mail criptografa a comunicação usando SSL. 0 indica que o Database Mail envia o email sem criptografia SSL.|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum *account_id* ou *account_name* é fornecido, o **sysmail_help_account** lista informações sobre todas as contas de Database Mail na instância de Microsoft SQL Server.  
  
 O procedimento armazenado **sysmail_help_account_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Listando as informações para todas as contas @ no__t-0  
  
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
  
 **B. Listando as informações de uma conta específica @ no__t-0  
  
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
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail procedimentos &#40;armazenados TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
