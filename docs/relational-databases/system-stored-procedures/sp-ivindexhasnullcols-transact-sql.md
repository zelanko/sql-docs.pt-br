---
description: sp_ivindexhasnullcols (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86fef9d3b131770e11edde117ea12e96d336de24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464185"
---
# <a name="sp_ivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Valida que o índice clusterizado da exibição indexada é exclusivo e não contém nenhuma coluna que possa ser nula quando a exibição indexada for usada para criar uma publicação transacional. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @viewname = ] 'view_name'` É o nome da exibição a ser verificada. *view_name* é **sysname**, sem padrão.  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` É o sinalizador que indica se o índice de exibição tem colunas que permitem NULL. *view_name* é **sysname**, sem padrão. Retorna um valor de **1** se o índice de exibição tem colunas que permitem NULL. Retornará um valor de **0** se a exibição não contiver colunas que permitam nulos.  
  
> [!NOTE]  
>  Se o procedimento armazenado em si retornar um código de retorno **1**, o que significa que a execução do procedimento armazenado teve uma falha, esse valor será **0** e deverá ser ignorado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_ivindexhasnullcols** é usado pela replicação transacional.  
  
 Por padrão, são criados artigos de exibição indexada em uma publicação como tabelas nos Assinantes No entanto, quando a coluna indexada permite valores NULL, a exibição indexada é criada como uma exibição indexada no Assinante em vez de em uma tabela. Executando esse procedimento armazenado ele pode alertar o usuário quanto à existência ou não desse problema com a exibição indexada atual.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
