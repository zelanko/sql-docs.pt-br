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
ms.openlocfilehash: ccb5cfd245148c97288a34b1857955f48f3efc73
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528401"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações (exceto senhas) sobre contas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_id = ] account_id`O ID da conta para listar informações. *account_id* é **int**, com um padrão de NULL.  
  
`[ @account_name = ] 'account_name'`O nome da conta para listar informações. *account_name* é **sysname,** com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (sucesso) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que contém as colunas listadas a seguir.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Descrição|  
|**Account_id**|**int**|O ID da conta.|  
|**name**|**sysname**|O nome da conta.|  
|**Descrição**|**nvarchar(256)**|A descrição da conta.|  
|**Email_address**|**nvarchar(128)**|O endereço de email a partir do qual as mensagens serão enviadas.|  
|**display_name**|**nvarchar(128)**|O nome para exibição da conta.|  
|**replyto_address**|**nvarchar(128)**|O endereço onde as respostas às mensagens desta conta são enviadas.|  
|**Servertype**|**sysname**|O tipo de servidor de email da conta.|  
|**Servername**|**sysname**|O nome do servidor de email da conta.|  
|**Porta**|**int**|O número da porta usada pelo servidor de email.|  
|**Username**|**nvarchar(128)**|O nome de usuário a ser usado para fazer logon no servidor de email, se o servidor de email usar autenticação. Quando **o nome de usuário** é NULO, o Database Mail não usa autenticação para esta conta.|  
|**use_default_credentials**|**bit**|Especifica se o email deve ser enviado ao servidor SMTP com as credenciais do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** é pouco, sem padrão. Quando este parâmetro for 1, o Database Mail usa as credenciais do serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando este parâmetro é 0, o Database Mail usa o ** \@nome de usuário** e ** \@** a senha para autenticação no servidor SMTP. Se ** \@o nome de usuário** e ** \@a senha** forem NULL, então o Database Mail usará autenticação anônima. Consulte o administrador do SMTP antes de especificar este parâmetro.|  
|**enable_ssl**|**bit**|Especifica se o Database Mail criptografa a comunicação usando o TLS (Transport Layer Security, segurança de camada de transporte), anteriormente conhecido como Secure Sockets Layer (SSL). Use esta opção se o TLS for necessário no servidor SMTP. **enable_ssl** é pouco, sem padrão. 1 indica que o Database Mail criptografa a comunicação usando O TLS. 0 indica que o Database Mail envia o e-mail sem criptografia TLS.|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum *account_id* ou *account_name* é fornecido, **sysmail_help_account** lista informações em todas as contas do Database Mail na instância do Microsoft SQL Server.  
  
 O procedimento armazenado **sysmail_help_account_sp** está no banco de dados do **MSDB** e pertence ao esquema **dbo.** O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Execute permissões para este procedimento padrão para membros da função servidor fixo **sysadmin.**  
  
## <a name="examples"></a>Exemplos  
 **A. Listando as informações de todas as contas**  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Correio de banco de dados](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de correio de banco de dados](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimentos armazenados de correio de banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
