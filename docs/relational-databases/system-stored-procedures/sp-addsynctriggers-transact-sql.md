---
title: sp_addsynctriggers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 89a6a997fd272985bd60d0b5d574fea07463f54d
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588281"
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria gatilhos no Assinante usados com todos os tipos de assinaturas atualizáveis (Imediata, Enfileirada e Atualização imediata com atualização enfileirada como failover). Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
> [!IMPORTANT]  
>  O [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) procedimento deve ser usado em vez de **sp_addsynctrigger**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) gera um script que contém o **sp_addsynctrigger** chamadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@sub_table=**] **'**_sub_table_**'**  
 É o nome da tabela do Assinante. *sub_table* está **sysname**, sem padrão.  
  
 [  **@sub_table_owner=**] **'**_sub_table_owner_**'**  
 Corresponde ao nome do proprietário da tabela do Assinante. *sub_table_owner* está **sysname**, sem padrão.  
  
 [  **@publisher=**] **'**_publisher_**'**  
 É o nome do servidor do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 É o nome do banco de dados Publicador. *publisher_db* está **sysname**, sem padrão. Se NULL, será usado o banco de dados atual.  
  
 [  **@publication=**] **'**_publicação_**'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@ins_proc=**] **'**_ins_proc_**'**  
 É o nome do procedimento armazenado que oferece suporte às inserções de transação síncrona no Publicador. *ins_proc* está **sysname**, sem padrão.  
  
 [  **@upd_proc=**] **'**_upd_proc_**'**  
 É o nome do procedimento armazenado que oferece suporte às atualizações de transação síncrona no Publicador. *ins_proc* está **sysname**, sem padrão.  
  
 [  **@del_proc=**] **'**_del_proc_**'**  
 É o nome do procedimento armazenado que oferece suporte às exclusões de transação síncrona no Publicador. *ins_proc* está **sysname**, sem padrão.  
  
 [  **@cftproc =** ] **'**_cftproc_**'**  
 É o nome do procedimento gerado automaticamente usado por publicações que permitem a atualização enfileirada. *cftproc* está **sysname**, sem padrão. Para publicações que permitem atualização imediata, este valor é o NULL. Este parâmetro se aplica a publicações que permitem atualização feita fila (Atualização Feita fila e Atualização Imediata com Atualização Feita fila como Failover).  
  
 [  **@proc_owner =** ] **'**_proc_owner_**'**  
 Especifica a conta de usuário no Publicador na qual todos os procedimentos armazenados gerados automaticamente para a publicação de atualização (enfileirada e/ou imediata) foram criados. *proc_owner* está **sysname** sem nenhum padrão.  
  
 [  **@identity_col=**] **'**_identity_col_**'**  
 É o nome da coluna de identidade no Publicador. *identity_col* está **sysname**, com um padrão NULL.  
  
 [  **@ts_col=**] **'**_timestamp_col_**'**  
 É o nome da **carimbo de hora** coluna no publicador. *timestamp_col* está **sysname**, com um padrão NULL.  
  
 [  **@filter_clause=**] **'**_filter_clause_**'**  
 É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave onde. *filter_clause*está **nvarchar (4000)**, com um padrão NULL.  
  
 [  **@primary_key_bitmap =**] **'**_primary_key_bitmap_**'**  
 É um mapa de bits das colunas de chave primária na tabela. *primary_key_bitmap* está **varbinary(4000)**, sem padrão.  
  
 [  **@identity_support =** ] *identity_support*  
 Ativa e desativa o tratamento do intervalo de identidade automático quando a atualização na fila é usada. *identity_support* é um **bit**, com um padrão de **0**. **0** significa que não há nenhuma identidade de intervalo de suporte, **1** permite a manipulação de intervalo de identidade automática.  
  
 [  **@independent_agent =** ] *independent_agent*  
 Indica se há um único Distribution Agent (um agente independente) para esta publicação ou um Distribution Agent por par de banco de dados de publicação e banco de dados de assinatura (um agente compartilhado). Esse valor reflete o valor da propriedade ndependent_agent da publicação definida no Publicador. *independent_agent* é um pouco com um padrão de **0**. Se **0**, o agente é um agente compartilhado. Se **1**, o agente é um agente independente.  
  
 [  **@distributor =** ] **'**_distribuidor_**'**  
 É o nome do distribuidor. *distribuidor* está **sysname**, sem padrão.  
  
 [ **@pubversion**=] *pubversion*  
 Indica a versão do Publicador. *pubversion* está **int**, com um padrão de 1. **1** significa que é a versão do publicador [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 ou anterior; **2** significa que o publicador é [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 3 (SP3) ou posterior. *pubversion* deve ser explicitamente definida como **2** quando a versão do publicador for [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SP3 ou posterior.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addsynctriggers** é usado pelo agente de distribuição como parte da inicialização de assinatura. Esse procedimento armazenado não é executado com frequência pelos usuários, mas pode ser útil se o usuário precisar configurar manualmente uma assinatura “no-sync”.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addsynctriggers**.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
