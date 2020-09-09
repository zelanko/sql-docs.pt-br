---
description: sp_scriptsubconflicttable (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e8fe3437c1852ffb2ec5817125317fa1a8fa379
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538528"
---
# <a name="sp_scriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Gera um script para criar uma tabela de conflitos no Assinante para um determinado artigo de assinatura enfileirada. Esse procedimento é gerado e executado no Assinante, no banco de dados de assinatura. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação que contém o artigo. O nome deve ser exclusivo no banco de dados. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo da assinatura. o *artigo* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|Retorna o script [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar a tabela de conflitos no Assinante para o artigo de assinatura enfileirada. Esse script é executado no Assinante, no banco de dados de assinatura.|  
  
## <a name="remarks"></a>Comentários  
 **sp_scriptsubconflicttable** é usado para assinantes que têm assinaturas em que o instantâneo inicial é aplicado manualmente. A tabela de conflitos é uma tabela opcional no Assinante.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_scriptsubconflicttable**.  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflitos de atualização na fila](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
