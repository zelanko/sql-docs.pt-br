---
title: sys. sp_rda_deauthorize_db (Transact-SQL) | Microsoft Docs
description: Saiba como usar sys. sp_rda_deauthorize_db para remover conexões autenticadas entre bancos de dados locais habilitados para Stretch e bancos de dados remotos do Azure.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c8413bf0a78ea1780d0babfc6fd88abb615d4ea
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538464"
---
# <a name="syssp_rda_deauthorize_db-transact-sql"></a>sys. sp_rda_deauthorize_db (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Remove a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto do Azure. Execute **sp_rda_deauthorize_db**  quando o banco de dados remoto estiver inacessível ou em um estado inconsistente e você quiser alterar o comportamento da consulta para todas as tabelas habilitadas para Stretch no banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
  
## <a name="remarks"></a>Comentários  
 Depois de executar **sp_rda_deauthorize_db** , todas as consultas em bancos de dados e tabelas habilitadas para Stretch falham. Ou seja, o modo de consulta é definido como DESABILITAdo. Para sair desse modo, execute uma das ações a seguir.  
  
-   Execute [Sys. sp_rda_reauthorize_db &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para reconectar-se ao banco de dados remoto do Azure. Esta operação redefine automaticamente o modo de consulta para LOCAL_AND_REMOTE, que é o comportamento padrão para Stretch Database. Ou seja, as consultas retornam resultados de dados locais e remotos.  
  
-   Execute [Sys. sp_rda_set_query_mode &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) com o argumento LOCAL_ONLY para permitir que as consultas continuem a ser executadas somente nos dados locais.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_rda_set_query_mode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys. sp_rda_reauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
