---
title: sp_dropmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4575ae38c0ff0397c01a4f4966503e1129b94e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um filtro de mesclagem. **sp_dropmergefilter** descarta todas as colunas de filtro de mesclagem definidas no filtro de mesclagem a ser removido. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, sem padrão.  
  
 [  **@filtername=**] **'***filtername***'**  
 É o nome do filtro a ser removido. *FilterName* é **sysname**, sem padrão.  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 Habilita ou desabilita a capacidade de ter um instantâneo invalidado. *force_invalidate_snapshot* é um **bit**, com um padrão **0**.  
  
 **0** Especifica que as alterações no artigo de mesclagem fazem com que o instantâneo seja inválido.  
  
 **1** significa que as alterações no artigo de mesclagem pode invalidar o instantâneo seja inválido. Se esse for o caso, um valor de **1** dá permissão para a ocorrência do novo instantâneo.  
  
 [ **@force_reinit_subscription**=] *force_reinit_subscription*  
 Habilita ou desabilita a capacidade de marcar uma assinatura como não válida. *force_reinit_subscription* é um **bit**, com um padrão **0**.  
  
 **0** Especifica que as alterações no filtro de artigo de mesclagem fazem com que as assinaturas inválido.  
  
 **1** significa que as alterações para o filtro de artigo de mesclagem faz com que as assinaturas inválido.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergefilter** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_dropmergefilter**.  
  
## <a name="see-also"></a>Consulte também  
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
