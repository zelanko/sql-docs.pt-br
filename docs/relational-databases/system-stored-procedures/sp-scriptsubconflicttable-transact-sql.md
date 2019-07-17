---
title: sp_scriptsubconflicttable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: stevestein
ms.author: sstein
ms.openlocfilehash: 806209b4f881576c680c14b0bc17ec4fd04a086c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126370"
---
# <a name="spscriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um script para criar uma tabela de conflitos no Assinante para um determinado artigo de assinatura enfileirada. Esse procedimento é gerado e executado no Assinante, no banco de dados de assinatura. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação que contém o artigo. O nome deve ser exclusivo no banco de dados. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo de assinatura. *artigo* está **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|Retorna o script [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar a tabela de conflitos no Assinante para o artigo de assinatura enfileirada. Esse script é executado no Assinante, no banco de dados de assinatura.|  
  
## <a name="remarks"></a>Comentários  
 **sp_scriptsubconflicttable** é usado para assinantes com assinaturas onde o instantâneo inicial é aplicado manualmente. A tabela de conflitos é uma tabela opcional no Assinante.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_scriptsubconflicttable**.  
  
## <a name="see-also"></a>Consulte também  
 [Detecção e resolução de conflitos na atualização na fila](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
