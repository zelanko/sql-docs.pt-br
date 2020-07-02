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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c713c2d6dc07c9f9dfc9e31dfbf8a1749bb2c189
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716341"
---
# <a name="sp_addsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Cria gatilhos no Assinante usados com todos os tipos de assinaturas atualizáveis (Imediata, Enfileirada e Atualização imediata com atualização enfileirada como failover). Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
> [!IMPORTANT]  
>  O procedimento de [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) deve ser usado em vez de **sp_addsynctrigger**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) gera um script que contém as chamadas de **sp_addsynctrigger** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @sub_table = ] 'sub_table'`É o nome da tabela do Assinante. *sub_table* é **sysname**, sem padrão.  
  
`[ @sub_table_owner = ] 'sub_table_owner'`É o nome do proprietário da tabela do Assinante. *sub_table_owner* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'`É o nome do servidor do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, sem padrão. Se NULL, será usado o banco de dados atual.  
  
`[ @publication = ] 'publication'`É o nome da publicação. A *publicação* é **sysname**, sem padrão.  
  
`[ @ins_proc = ] 'ins_proc'`É o nome do procedimento armazenado que dá suporte a inserções de transações síncronas no Publicador. *ins_proc* é **sysname**, sem padrão.  
  
`[ @upd_proc = ] 'upd_proc'`É o nome do procedimento armazenado que dá suporte a atualizações de transação síncronas no Publicador. *ins_proc* é **sysname**, sem padrão.  
  
`[ @del_proc = ] 'del_proc'`É o nome do procedimento armazenado que dá suporte a exclusões de transações síncronas no Publicador. *ins_proc* é **sysname**, sem padrão.  
  
`[ @cftproc = ] 'cftproc'`É o nome do procedimento gerado automaticamente usado por publicações que permitem atualização em fila. *cftproc* é **sysname**, sem padrão. Para publicações que permitem atualização imediata, este valor é o NULL. Este parâmetro se aplica a publicações que permitem atualização feita fila (Atualização Feita fila e Atualização Imediata com Atualização Feita fila como Failover).  
  
`[ @proc_owner = ] 'proc_owner'`Especifica a conta de usuário no Publicador sob a qual todos os procedimentos armazenados gerados automaticamente para atualizar a publicação (na fila e/ou imediata) foram criados. *proc_owner* é **sysname** sem padrão.  
  
`[ @identity_col = ] 'identity_col'`É o nome da coluna de identidade no Publicador. *identity_col* é **sysname**, com um padrão de NULL.  
  
`[ @ts_col = ] 'timestamp_col'`É o nome da coluna de **carimbo de data/hora** no Publicador. *timestamp_col* é **sysname**, com um padrão de NULL.  
  
`[ @filter_clause = ] 'filter_clause'`É uma cláusula de restrição (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave WHERE. *filter_clause*é **nvarchar (4000)**, com um padrão de NULL.  
  
`[ @primary_key_bitmap = ] 'primary_key_bitmap'`É um mapa de bits das colunas de chave primária na tabela. *primary_key_bitmap* é **varbinary (4000)**, sem padrão.  
  
`[ @identity_support = ] identity_support`Habilita e desabilita o tratamento automático de intervalo de identidade quando a atualização em fila é usada. *identity_support* é um **bit**, com um padrão de **0**. **0** significa que não há suporte para intervalo de identidade, **1** habilita o tratamento automático de intervalo de identidade.  
  
`[ @independent_agent = ] independent_agent`Indica se há um único Agente de Distribuição (um agente independente) para essa publicação, ou um Agente de Distribuição por par de banco de dados de publicação e de assinatura (um agente compartilhado). Esse valor reflete o valor da propriedade ndependent_agent da publicação definida no Publicador. *independent_agent* é um bit com um padrão de **0**. Se for **0**, o agente será um agente compartilhado. Se for **1**, o agente será um agente independente.  
  
`[ @distributor = ] 'distributor'`É o nome do distribuidor. o *distribuidor* é **sysname**, sem padrão.  
  
`[ @pubversion = ] pubversion`Indica a versão do Publicador. *pubversion* é **int**, com um padrão de 1. **1** significa que a versão do Publicador é [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 ou anterior; **2** significa que o Publicador é o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 3 (SP3) ou posterior. *pubversion* deve ser definido explicitamente como **2** quando a versão do Publicador for [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SP3 ou posterior.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addsynctriggers** é usado pelo agente de distribuição como parte da inicialização da assinatura. Esse procedimento armazenado não é executado com frequência pelos usuários, mas pode ser útil se o usuário precisar configurar manualmente uma assinatura “no-sync”.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addsynctriggers**.  
  
## <a name="see-also"></a>Consulte Também  
 [Assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [&#41;&#40;Transact-SQL de sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
