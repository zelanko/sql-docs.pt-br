---
title: sp_getqueuedrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1915bec9f0a9f1e05bfe6a2975553bb20e330289
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spgetqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera linhas no Assinante que têm atualizações pendente na fila. Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tablename =**] **'***tablename***'**  
 É o nome da tabela. *TableName* é **sysname**, sem padrão. A tabela deve ser uma parte de uma assinatura em fila.  
  
 [  **@owner =**] **'***proprietário***'**  
 É o proprietário da assinatura. *proprietário* é **sysname**, com um padrão NULL.  
  
 [  **@tranid =** ] **'***transaction_id***'**  
 Permite que a saída seja filtrada pela ID da transação. *transaction_id* é **nvarchar (70)**, com um padrão NULL. Se especificada, a ID da transação associada ao comando em fila será exibida. Se for NULL, são exibidos todos os comandos na fila.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Mostra todas as linhas que atualmente têm pelo menos uma transação em fila para a tabela assinada.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Ação**|**nvarchar(10)**|Tipo de ação a ser realizada quando ocorre sincronização.<br /><br /> INS = inserir<br /><br /> DEL = excluir<br /><br /> UPD = atualizar|  
|**Tranid**|**nvarchar (70)**|ID da transação sob a qual o comando foi executado.|  
|**tabela column1... n**||O valor para cada coluna da tabela especificada no *tablename*.|  
|**msrepl_tran_version**|**uniqueidentifier**|Essa coluna é usada para localizar alterações a dados replicados e executar detecção de conflito no Publicador. Essa coluna é adicionada automaticamente à tabela.|  
  
## <a name="remarks"></a>Remarks  
 **sp_getqueuedrows** é usado em assinantes que participam de atualização na fila.  
  
 **sp_getqueuedrows** localiza linhas de uma determinada tabela em uma assinatura de banco de dados que participou de uma atualização na fila, mas atualmente não foi resolvida pelo queue reader agent.  
  
## <a name="permissions"></a>Permissões  
 **sp_getqueuedrows** requer permissões SELECT na tabela especificada na *tablename*.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Detecção e resolução de conflitos na atualização na fila](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
