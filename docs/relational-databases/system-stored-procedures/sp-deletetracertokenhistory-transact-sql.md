---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25f264f72042b6d26b3ebc5c677bc9ed4a981751
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove registros de token de rastreamento de [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) e [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) tabelas do sistema. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_deletetracertokenhistory [ @publication = ] 'publication'   
    [ , [ @tracer_id = ] tracer_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação na qual o token de rastreamento foi inserido. *publicação* é **sysname**, sem padrão.  
  
 [  **@tracer_id=** ] *tracer_id*  
 É a ID do token de rastreamento a ser excluído. *tracer_id* é **int**, com um valor padrão de NULL. Se **nulo**, em seguida, todos os tokens de rastreamento que pertencem à publicação serão excluídos.  
  
 [  **@cutoff_date=** ] *cutoff_date*  
 Especifica uma data de prazo da qual são removidos todos os tokens de rastreamento inseridos na publicação antes daquela data. *cutoff_date* é datetime, com um valor padrão de NULL.  
  
 [  **@publisher=** ] **'***publicador***'**  
 O nome do publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Esse parâmetro só deve ser especificado para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 O nome do banco de dados de publicação. *publisher_db* é **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_deletetracertokenhistory** é usado em replicação transacional.  
  
 Ao executar **sp_deletetracertokenhistory**, você só pode especificar um dos *tracer_id* ou *cutoff_date*. Um erro ocorre quando você especifica ambos os parâmetros.  
  
 Se você não executar **sp_deletetracertokenhistory** para remover metadados de token de rastreamento, as informações serão removidas quando ocorre a limpeza de histórico agendada regularmente.  
  
 IDs de token de rastreamento podem ser determinados executando [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ou consultando o [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabela do sistema.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, o **db_owner** função de banco de dados fixa no banco de dados de publicação, ou **db_owner** banco de dados fixo ou  **replmonitor** funções no banco de dados de distribuição podem executar **sp_deletetracertokenhistory**.  
  
## <a name="see-also"></a>Consulte também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
