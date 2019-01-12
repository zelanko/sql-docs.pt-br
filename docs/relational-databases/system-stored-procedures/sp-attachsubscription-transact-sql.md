---
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9cd00d75a8afd2fae06868fd4b44320865f239f2
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126365"
---
# <a name="spattachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Anexa um banco de dados de assinatura existente a qualquer Assinante. Esse procedimento armazenado é executado no novo Assinante, no banco de dados mestre.  
  
> [!IMPORTANT]  
>  Esse recurso é preterido e será removido em uma versão futura. Esse recurso não deveria ser usado em novo trabalho de desenvolvimento. Para publicações de mesclagem, que são particionadas usando filtros com parâmetros, recomendamos o uso de novos recursos de instantâneos particionados, que simplificam a inicialização de um grande número de assinaturas. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Para publicações que não são particionadas, é possível inicializar uma inscrição com um backup. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@dbname=** ] **'***dbname***'**  
 É a cadeia de caracteres que especifica o banco de dados de assinatura de destino por nome. *DBName* está **sysname**, sem padrão.  
  
 [  **@filename=** ] **'***filename***'**  
 É o nome e o local físico do MDF primário (**mestre** arquivo de dados). *nome do arquivo* está **nvarchar (260)**, sem padrão.  
  
 [  **@subscriber_security_mode=** ] **'***subscriber_security_mode***'**  
 É o modo de segurança do Assinante a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_security_mode* está **int**, com um padrão NULL.  
  
> [!NOTE]  
>  Autenticação do Windows deve ser usada. Se *subscriber_security_mode* não está **1** (autenticação do Windows), um erro será retornado.  
  
 [  **@subscriber_login=** ] **'***subscriber_login***'**  
 É o nome do logon do Assinante a ser usado ao conectar-se a um Assinante na sincronização. *subscriber_login* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores de scripts. Se *subscriber_security_mode* não está **1** e *subscriber_login* é especificado, um erro será retornado.  
  
 [  **@subscriber_password=** ] **'***subscriber_password***'**  
 É a senha de Assinante. *subscriber_password* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores de scripts. Se *subscriber_security_mode* não está **1** e *subscriber_password* é especificado, um erro será retornado.  
  
 [  **@distributor_security_mode=** ] *distributor_security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_security_mode* está **int**, com um padrão de **0**. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica a autenticação do Windows. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=** ] **'***distributor_login***'**  
 É o logon do Distribuidor a ser usado ao conectar-se a um Distribuidor na sincronização. *distributor_login* será necessária se *distributor_security_mode* é definido como **0**. *distributor_login* está **sysname**, com um padrão NULL.  
  
 [  **@distributor_password=** ] **'***distributor_password***'**  
 É a senha do Distribuidor. *distributor_password* será necessária se *distributor_security_mode* é definido como **0**. *distributor_password* está **sysname**, com um padrão NULL. O valor de *distributor_password* deve ser menor que 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@publisher_security_mode=** ] *publisher_security_mode*  
 É o modo de segurança a ser usado ao se conectar a um Publicador na sincronização. *publisher_security_mode* está **int**, com um padrão de **1**. Se **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login=** ] **'***publisher_login***'**  
 É o logon a ser usado na conexão com um Publicador durante a sincronização. *publisher_login* está **sysname**, com um padrão NULL.  
  
 [  **@publisher_password=** ] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* está **sysname**, com um padrão NULL. O valor de *publisher_password* deve ser menor que 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@job_login=** ] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* está **nvarchar(257)**, sem padrão. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor.  
  
 [  **@job_password=** ] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* está **sysname**, sem padrão. O valor de *job_password* deve ser menor que 120 caracteres Unicode.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [  **@db_master_key_password=** ] **'***db_master_key_password***'**  
 É a senha de uma chave mestra de banco de dados definida pelo usuário. *db_master_key_password* está **nvarchar(524)**, com um valor padrão de NULL. Se *db_master_key_password* não for especificado, uma chave mestra de banco de dados existente será descartada e recriada.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_attachsubscription** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 Uma assinatura não poderá ser anexada à publicação se o período de retenção da publicação tiver expirado. Se uma assinatura com um período de retenção decorrido for especificada, ocorrerá um erro quando ela for anexada ou quando for sincronizada pela primeira vez. Publicações com um período de retenção da publicação **0** (nunca expiram) serão ignorados.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_attachsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
