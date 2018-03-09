---
title: sp_addlogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53f2e42d92c9e100dfe90ae0b46ec2e2c2eef969
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um Log Leitor Agent a um determinado banco de dados. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_login** =] **'***job_login***'**  
 É o logon da conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, com um valor padrão de NULL. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor.  
  
> [!NOTE]  
>  Para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores, isso deve ser o mesmo logon especificado em [sp_adddistpublisher &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
 [  **@job_password** =] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* é **sysname**, com um valor padrão de NULL.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para melhor segurança, nomes de logon e senhas devem ser fornecidos em tempo de execução.  
  
 [  **@job_name** =] **'***job_name***'**  
 É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o agente é iniciado usando um trabalho existente em vez de um trabalho recém-criado (o padrão).  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 É o modo de segurança usado pelo agente ao conectar-se ao Publicador. *publisher_security_mode* é **smallint**, com um padrão de **1**. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, e **1** Especifica autenticação do Windows. Um valor de **0** devem ser especificados para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
 [  **@publisher_login** =] **'***publisher_login***'**  
 É o logon usado na conexão com o Publicador. *publisher_login* é **sysname**, com um padrão NULL. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* é NULL e *publisher_security_mode* é **1**, em seguida, a conta do Windows especificada na *job_login* será usado ao conectar-se ao publicador.  
  
 [  **@publisher_password** =] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para melhor segurança, nomes de logon e senhas devem ser fornecidos em tempo de execução.  
  
 [  **@publisher** =] **'***publicador***'**  
 É o nome do não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro não deve ser especificado para um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addlogreader_agent** é usado em replicação transacional.  
  
 Você deve executar **sp_addlogreader_agent** para adicionar um agente de leitor de Log, se você tiver atualizado um banco de dados foi habilitado para replicação para esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de que era criada uma publicação que usou o banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addlogreader_agent**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
