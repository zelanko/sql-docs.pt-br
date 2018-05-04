---
title: sys.sp_rda_deauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e01204dbd28c114daed84a6c3d7d92691952694e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>sys.sp_rda_deauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Remove a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto do Azure. Executar **sp_rda_deauthorize_db** quando o banco de dados remoto está inacessível ou em um estado inconsistente e você deseja alterar o comportamento da consulta para todas as tabelas habilitadas para Stretch no banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  
  
## <a name="remarks"></a>Remarks  
 Depois de executar **sp_rda_deauthorize_db** , todas as consultas em tabelas e bancos de dados habilitados para Stretch falharem. Ou seja, o modo de consulta é definido como desabilitado. Para sair deste modo, siga um destes procedimentos.  
  
-   Executar [sys. sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) reconectar-se ao banco de dados remoto do Azure. Esta operação redefine automaticamente o modo de consulta como LOCAL_AND_REMOTE, que é o comportamento padrão para o Stretch Database. Ou seja, consultas retornam resultados de dados locais e remotos.  
  
-   Executar [sp_rda_set_query_mode &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) com o argumento LOCAL_ONLY para permitir que consultas continue executar apenas dados locais.  
  
## <a name="see-also"></a>Consulte também  
 [sys.sp_rda_set_query_mode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
