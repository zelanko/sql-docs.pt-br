---
description: sp_dropmergefilter (Transact-SQL)
title: sp_dropmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5eb42c423d562ad251dc55ce015fdd111fa7d6fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464329"
---
# <a name="sp_dropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove um filtro de mesclagem. **sp_dropmergefilter** remove todas as colunas de filtro de mesclagem definidas no filtro de mesclagem que deve ser removida. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. o *artigo* é **sysname**, sem padrão.  
  
`[ @filtername = ] 'filtername'` É o nome do filtro a ser removido. *FilterName* é **sysname**, sem padrão.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Habilita ou desabilita a capacidade de um instantâneo ser invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não fazem com que o instantâneo seja inválido.  
  
 **1** significa que as alterações no artigo de mesclagem podem fazer com que o instantâneo seja inválido. Se esse for o caso, um valor de **1** dará permissão para que o novo instantâneo ocorra.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` Habilita ou desabilita a capacidade de marcar uma assinatura como inválida. *force_reinit_subscription* é um **bit**, com um padrão **0**.  
  
 **0** especifica que as alterações no filtro de artigo de mesclagem não fazem com que as assinaturas sejam inválidas.  
  
 **1** significa que as alterações no filtro de artigo de mesclagem fazem com que as assinaturas sejam inválidas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropmergefilter** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_dropmergefilter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addmergefilter ](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergefilter ](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergefilter ](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
