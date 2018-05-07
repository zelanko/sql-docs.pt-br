---
title: sp_restoremergeidentityrange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b8be3de617713868a755dbab55e4ac4674dfd07a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sprestoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esse procedimento armazenado é usado para atualizar atribuições de intervalo de identidade. Assegura que o gerenciamento de intervalo de identidade automático funcione apropriadamente, depois que um Publicador é restaurado de um backup. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com o valor padrão de **todos os**. Quando especificado, somente intervalos de identidade para aquela publicação são restaurados.  
  
 [ **@article** =] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, com um valor padrão de **todos os**. Quando especificado, somente intervalos de identidade para aquele artigo são restaurados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_restoremergeidentityrange** é usado com a replicação de mesclagem.  
  
 **sp_restoremergeidentityrange** obtém informações de alocação de intervalo de identidade máximo do distribuidor e atualiza os valores de **max_used** coluna de [MSmerge_identity_range_allocations &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md) para os artigos que usam gerenciamento de intervalo de identidade automática.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_restoremergeidentityrange**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
