---
description: sp_attachsubscription (Transact-SQL)
title: sp_attachsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_attachsubscription
- sp_attachsubscription_TSQL
helpviewer_keywords:
- sp_attachsubscription
ms.assetid: b9bbda36-a46a-4327-a01e-9cd632e4791b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 25a617eeac0926e6bcb80f99125603072ee34be8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539140"
---
# <a name="sp_attachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

  Anexa um banco de dados de assinatura existente a qualquer Assinante. Esse procedimento armazenado é executado no novo Assinante, no banco de dados mestre.  
  
> [!IMPORTANT]  
>  Esse recurso é preterido e será removido em uma versão futura. Esse recurso não deveria ser usado em novo trabalho de desenvolvimento. Para publicações de mesclagem, que são particionadas usando filtros com parâmetros, recomendamos o uso de novos recursos de instantâneos particionados, que simplificam a inicialização de um grande número de assinaturas. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Para publicações que não são particionadas, é possível inicializar uma inscrição com um backup. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_attachsubscription [ @dbname = ] 'dbname'  
        , [ @filename = ] 'filename'  
    [ , [ @subscriber_security_mode = ] 'subscriber_security_mode' ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @db_master_key_password = ] 'db_master_key_password' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` É a cadeia de caracteres que especifica o banco de dados de assinatura de destino por nome. *dbname* é **sysname**, sem padrão.  
  
`[ @filename = ] 'filename'` É o nome e o local físico do MDF principal (arquivo de dados**mestre** ). *filename* é **nvarchar (260)**, sem padrão.  
  
`[ @subscriber_security_mode = ] 'subscriber_security_mode'` É o modo de segurança do assinante a ser usado ao se conectar a um Assinante durante a sincronização. *subscriber_security_mode* é **int**, com um padrão de NULL.  
  
> [!NOTE]  
>  Autenticação do Windows deve ser usada. Se *subscriber_security_mode* não for **1** (autenticação do Windows), um erro será retornado.  
  
`[ @subscriber_login = ] 'subscriber_login'` É o nome de logon do assinante a ser usado ao se conectar a um assinante ao sincronizar. *subscriber_login* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores de scripts. Se *subscriber_security_mode* não for **1** e *subscriber_login* for especificado, um erro será retornado.  
  
`[ @subscriber_password = ] 'subscriber_password'` É a senha do Assinante. *subscriber_password* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores de scripts. Se *subscriber_security_mode* não for **1** e *subscriber_password* for especificado, um erro será retornado.  
  
`[ @distributor_security_mode = ] distributor_security_mode` É o modo de segurança a ser usado ao se conectar a um distribuidor durante a sincronização. *distributor_security_mode* é **int**, com um padrão de **0**. **0** especifica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** especifica a autenticação do Windows. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'` É o logon do distribuidor a ser usado ao se conectar a um distribuidor durante a sincronização. *distributor_login* será necessário se *distributor_security_mode* for definido como **0**. *distributor_login* é **sysname**, com um padrão de NULL.  
  
`[ @distributor_password = ] 'distributor_password'` É a senha do distribuidor. *distributor_password* será necessário se *distributor_security_mode* for definido como **0**. *distributor_password* é **sysname**, com um padrão de NULL. O valor de *distributor_password* deve ter menos de 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @publisher_security_mode = ] publisher_security_mode` É o modo de segurança a ser usado ao se conectar a um Publicador durante a sincronização. *publisher_security_mode* é **int**, com um padrão de **1**. Se **0**, especifica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` É o logon a ser usado ao se conectar a um Publicador durante a sincronização. *publisher_login* é **sysname**, com um padrão de NULL.  
  
`[ @publisher_password = ] 'publisher_password'` É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, com um padrão de NULL. O valor de *publisher_password* deve ter menos de 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_login = ] 'job_login'` É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor.  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão. O valor de *job_password* deve ter menos de 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @db_master_key_password = ] 'db_master_key_password'` É a senha de uma chave mestra de banco de dados definida pelo usuário. *db_master_key_password* é **nvarchar (524)**, com um valor padrão de NULL. Se *db_master_key_password* não for especificado, uma chave mestra de banco de dados existente será descartada e recriada.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_attachsubscription** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
 Uma assinatura não poderá ser anexada à publicação se o período de retenção da publicação tiver expirado. Se uma assinatura com um período de retenção decorrido for especificada, ocorrerá um erro quando ela for anexada ou quando for sincronizada pela primeira vez. As publicações com um período de retenção de publicação de **0** (nunca expiram) são ignoradas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_attachsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
