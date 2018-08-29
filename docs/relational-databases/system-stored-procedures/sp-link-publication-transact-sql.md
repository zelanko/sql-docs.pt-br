---
title: sp_link_publication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80513a0245d13cb955c9ced0e2f02d6f3d241d2e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026145"
---
# <a name="splinkpublication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define as informações de configuração e de segurança usadas por gatilhos de sincronização de assinaturas de atualização imediata na conexão com o Publicador. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
> [!IMPORTANT]  
>  Sob certas condições, esse procedimento armazenado pode falhar se o assinante estiver executando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 ou posterior e o publicador estiver executando uma versão anterior. Se o procedimento armazenado falhar neste cenário, atualize o Publicador para a versão do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 ou posterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher**=] **'***publisher***'**  
 É o nome do Publicador ao qual vincular-se. *Publisher* está **sysname**, sem padrão.  
  
 [ **@publisher_db**=] **'***publisher_db***'**  
 É o nome do banco de dados Publicador ao qual vincular-se. *publisher_db* está **sysname**, sem padrão.  
  
 [ **@publication**=] **'***publicação***'**  
 É o nome da publicação a qual vincular-se. *publicação* está **sysname**, sem padrão.  
  
 [ **@security_mode**=] *security_mode*  
 É o modo de segurança usado pelo Assinante para conexão a um Publicador remoto para atualização imediata. *security_mode* está **int**, e pode ser um destes valores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|Usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação com o logon especificado nesse procedimento armazenado como *login* e *senha*.<br /><br /> Observação: em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa opção foi usada para especificar uma chamada de procedimento dinâmico remoto (RPC).|  
|**1**|Usa o contexto de segurança (Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Autenticação do Windows) do usuário que faz a alteração no Assinante.<br /><br /> Observação: Essa conta também deve existir no publicador com privilégios suficientes. Ao usar Autenticação do Windows, deve haver suporte para delegação de conta de segurança.|  
|**2**|Usa um logon de servidor vinculado existente, definido pelo usuário criado usando **sp_link_publication**.|  
  
 [ **@login**=] **'***logon***'**  
 É o logon. *login* é **sysname**, com um padrão de NULL. Esse parâmetro deve ser especificado quando *security_mode* é **0**.  
  
 [ **@password**=] **'***senha***'**  
 É a senha. *senha* está **sysname**, com um padrão NULL. Esse parâmetro deve ser especificado quando *security_mode* é **0**.  
  
 [  **@distributor=** ] **'***distribuidor***'**  
 É o nome do distribuidor. *distribuidor* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_link_publication** é usado por assinaturas de atualização imediata em replicação transacional.  
  
 **sp_link_publication** pode ser usado para assinaturas push e pull. Pode ser chamado antes ou depois que a assinatura é criada. Uma entrada é inserida ou atualizada na [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabela do sistema.  
  
 Para assinaturas push, a entrada pode ser limpa por [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). Para assinaturas pull, a entrada pode ser limpa por [sp_droppullsubscription &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) ou [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). Você também pode chamar **sp_link_publication** com uma senha NULL para limpar a entrada na [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabela do sistema por questões de segurança.  
  
 O modo padrão usado por um Assinante de atualização imediata quando ele se conecta ao Publicador não permite uma conexão usando Autenticação do Windows. Para se conectar ao modo de Autenticação do Windows, um servidor vinculado precisa ser definido como Publicador e o Assinante de atualização imediata deve usar essa conexão ao atualizar o Assinante. Isso exige que o **sp_link_publication** a serem executados com *security_mode* = **2**. Ao usar Autenticação do Windows, deve haver suporte para delegação de conta de segurança.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_link_publication**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
