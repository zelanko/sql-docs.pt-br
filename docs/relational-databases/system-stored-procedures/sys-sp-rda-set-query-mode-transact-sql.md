---
title: sys. sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
description: Use sys. sp_rda_set_query_mode para especificar se as consultas em relação ao banco de dados atual habilitado para Stretch e suas tabelas retornam locais e remotos, ou apenas dados locais.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2fbef46606f182e2c9833d2ce421c61fc421105
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243327"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys. sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Especifica se as consultas em relação ao banco de dados atual habilitado para Stretch e suas tabelas retornam tanto local quanto remoto (o padrão) ou somente dados locais.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @mode * \@ modo* [=]  
 É um dos valores a seguir.  
  
-   **Desabilitado** Todas as consultas em tabelas habilitadas para Stretch falham.  
  
-   **LOCAL_ONLY** As consultas em tabelas habilitadas para Stretch retornam apenas dados locais.  
  
-   **LOCAL_AND_REMOTE** As consultas em tabelas habilitadas para Stretch retornam dados locais e remotos. Esse é o comportamento padrão.  
  
 [ @force =] * \@ forçar*  
 É um valor de bit opcional que você pode definir como 1 se desejar alterar o modo de consulta sem validação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
  
## <a name="remarks"></a>Comentários  
 Os procedimentos armazenados estendidos a seguir também definem o modo de consulta para um banco de dados habilitado para Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Depois de executar **sp_rda_deauthorize_db** , todas as consultas em bancos de dados e tabelas habilitadas para Stretch falham. Ou seja, o modo de consulta é definido como DESABILITAdo. Para sair desse modo, execute uma das ações a seguir.  
  
    -   Execute [Sys. sp_rda_reauthorize_db &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para reconectar-se ao banco de dados remoto do Azure. Esta operação redefine automaticamente o modo de consulta para LOCAL_AND_REMOTE, que é o comportamento padrão para Stretch Database. Ou seja, as consultas retornam resultados de dados locais e remotos.  
  
    -   Execute [Sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) com o argumento LOCAL_ONLY para permitir que as consultas continuem a ser executadas somente nos dados locais.  
  
-   **sp_rda_reauthorize_db**  
  
     Quando você executa [Sys. sp_rda_reauthorize_db &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para se reconectar ao banco de dados remoto do Azure, essa operação redefine automaticamente o modo de consulta como LOCAL_AND_REMOTE, que é o comportamento padrão para Stretch Database. Ou seja, as consultas retornam resultados de dados locais e remotos.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
