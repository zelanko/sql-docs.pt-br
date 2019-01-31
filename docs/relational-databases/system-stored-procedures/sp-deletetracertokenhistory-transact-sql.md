---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8f1a91210cbd263a9225cef54bcf27a81bf2bf4
ms.sourcegitcommit: dc3543e81e32451568133e9b1b560f7ee76d7fb5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55428593"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove registros de token de rastreamento a [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) e [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) tabelas do sistema. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
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
 [ **@publication=** ] **'***publication***'**  
 É o nome da publicação na qual o token de rastreamento foi inserido. *publicação* está **sysname**, sem padrão.  
  
 [ **@tracer_id=** ] *tracer_id*  
 É a ID do token de rastreamento a ser excluído. *tracer_id* está **int**, com um valor padrão de NULL. Se **nulo**, em seguida, todos os tokens de rastreamento que pertencem à publicação serão excluídos.  
  
 [ **@cutoff_date=** ] *cutoff_date*  
 Especifica uma data de prazo da qual são removidos todos os tokens de rastreamento inseridos na publicação antes daquela data. *cutoff_date* é a data e hora, com um valor padrão de NULL.  
  
 [ **@publisher=** ] **'***publisher***'**  
 O nome do publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]
>  Esse parâmetro só deve ser especificado para não - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores ou ao executar o procedimento armazenado do distribuidor.  
  
 [ **@publisher_db=** ] **'***publisher_db***'**  
 O nome do banco de dados de publicação. *publisher_db* está **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
> [!NOTE]
>  Esse parâmetro deve ser especificado ao executar o procedimento armazenado do distribuidor.  

## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_deletetracertokenhistory** é usado em replicação transacional.  
  
 Ao executar **sp_deletetracertokenhistory**, você só pode especificar uma das *tracer_id* ou *cutoff_date*. Um erro ocorre quando você especifica ambos os parâmetros.  
  
 Se você não executa **sp_deletetracertokenhistory** para remover metadados de token de rastreamento, as informações serão removidas quando ocorre a limpeza de histórico agendada regularmente.  
  
 IDs de token de rastreamento podem ser determinadas executando [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ou consultando os [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabela do sistema.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa, o **db_owner** fixa a função de banco de dados no banco de dados de publicação, ou **db_owner** banco de dados fixo ou  **replmonitor** funções no banco de dados de distribuição podem executar **sp_deletetracertokenhistory**.  
  
## <a name="see-also"></a>Consulte também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
