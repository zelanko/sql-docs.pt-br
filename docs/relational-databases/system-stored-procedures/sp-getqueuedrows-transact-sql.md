---
title: sp_getqueuedrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad7521eed3cd25d067e3ea253ff2a4362350c889
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123937"
---
# <a name="sp_getqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera linhas no Assinante que têm atualizações pendente na fila. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tablename = ] 'tablename'`É o nome da tabela. *TableName* é **sysname**, sem padrão. A tabela deve ser uma parte de uma assinatura em fila.  
  
`[ @owner = ] 'owner'`É o proprietário da assinatura. *Owner* é **sysname**, com um padrão de NULL.  
  
`[ @tranid = ] 'transaction_id'`Permite que a saída seja filtrada pela ID da transação. *transaction_id* é **nvarchar (70)**, com um padrão de NULL. Se especificada, a ID da transação associada ao comando em fila será exibida. Se for NULL, são exibidos todos os comandos na fila.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Mostra todas as linhas que atualmente têm pelo menos uma transação em fila para a tabela assinada.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Ação**|**nvarchar (10)**|Tipo de ação a ser realizada quando ocorre sincronização.<br /><br /> INS = inserir<br /><br /> DEL = excluir<br /><br /> UPD = atualizar|  
|**Transid**|**nvarchar (70)**|ID da transação sob a qual o comando foi executado.|  
|**table column1...n**||O valor de cada coluna da tabela especificada em *TableName*.|  
|**msrepl_tran_version**|**uniqueidentifier**|Essa coluna é usada para localizar alterações a dados replicados e executar detecção de conflito no Publicador. Essa coluna é adicionada automaticamente à tabela.|  
  
## <a name="remarks"></a>Comentários  
 **sp_getqueuedrows** é usado em assinantes que participam da atualização em fila.  
  
 **sp_getqueuedrows** localiza linhas de uma determinada tabela em um banco de dados de assinatura que participou de uma atualização enfileirada, mas que, no momento, não foi resolvida pelo Queue Reader Agent.  
  
## <a name="permissions"></a>Permissões  
 **sp_getqueuedrows** requer permissões SELECT na tabela especificada em *TableName*.  
  
## <a name="see-also"></a>Consulte Também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Detecção e resolução de conflitos de atualização na fila](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
