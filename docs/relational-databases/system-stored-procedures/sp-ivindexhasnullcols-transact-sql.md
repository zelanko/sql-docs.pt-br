---
title: sp_ivindexhasnullcols (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77a0e3f1795545e553347ae699e719af2ad506b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62959619"
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Valida que o índice clusterizado da exibição indexada é exclusivo e não contém nenhuma coluna que possa ser nula quando a exibição indexada for usada para criar uma publicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @viewname = ] 'view_name'` É o nome de exibição a ser verificada. *view_name* está **sysname**, sem padrão.  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` É o sinalizador que indica se o índice de exibição tem colunas que permitem NULL. *view_name* está **sysname**, sem padrão. Retorna um valor de **1** se o índice de exibição tem colunas que permitem NULL. Retorna um valor de **0** se o modo de exibição não contiver colunas que permitem valores nulos.  
  
> [!NOTE]  
>  Se o próprio procedimento armazenado retorna um código de retorno **1**, que significa que a execução do procedimento armazenado teve uma falha, esse valor é **0** e deve ser ignorado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_ivindexhasnullcols** é usada pela replicação transacional.  
  
 Por padrão, são criados artigos de exibição indexada em uma publicação como tabelas nos Assinantes No entanto, quando a coluna indexada permite valores NULL, a exibição indexada é criada como uma exibição indexada no Assinante em vez de em uma tabela. Executando esse procedimento armazenado ele pode alertar o usuário quanto à existência ou não desse problema com a exibição indexada atual.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
