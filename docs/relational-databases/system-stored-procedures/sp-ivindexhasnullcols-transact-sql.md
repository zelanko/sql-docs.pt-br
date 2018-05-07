---
title: sp_ivindexhasnullcols (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4431ae915c43d6ceb96200c3ebbf6aa976dd4ff3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 [ **@viewname**=] **'***view_name***'**  
 É o nome da exibição a ser verificada. *view_name* é **sysname**, sem padrão.  
  
 [ **@fhasnullcols**=] *field_has_null_columns* saída  
 É o sinalizador que indica se o índice de exibição tem colunas que permitem NULL. *view_name* é **sysname**, sem padrão. Retorna um valor de **1** se o índice de exibição tem colunas que permitem NULL. Retorna um valor de **0** se o modo de exibição não contém colunas que permitem valores nulos.  
  
> [!NOTE]  
>  Se o próprio procedimento armazenado retorna um código de retorno **1**, o que significa que a execução do procedimento armazenado teve uma falha, esse valor é **0** e deve ser ignorado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_ivindexhasnullcols** é usada pela replicação transacional.  
  
 Por padrão, são criados artigos de exibição indexada em uma publicação como tabelas nos Assinantes No entanto, quando a coluna indexada permite valores NULL, a exibição indexada é criada como uma exibição indexada no Assinante em vez de em uma tabela. Executando esse procedimento armazenado ele pode alertar o usuário quanto à existência ou não desse problema com a exibição indexada atual.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
