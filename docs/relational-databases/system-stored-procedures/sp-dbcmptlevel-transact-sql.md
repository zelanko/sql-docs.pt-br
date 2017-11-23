---
title: sp_dbcmptlevel (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
caps.latest.revision: "110"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fba712ff23978ec3af33e481b947b1e1eca7d0f9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define certos comportamentos de banco de dados como sendo compatíveis com a versão especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Use [nível de compatibilidade do banco de dados ALTER](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)em vez disso.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=** ] *nome*  
 É o nome do banco de dados para o qual o nível de compatibilidade será alterado. Os nomes de banco de dados devem obedecer às regras para identificadores. *nome* é **sysname**, com um padrão NULL.  
  
 [  **@new_cmptlevel=** ] *versão*  
 É a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual o banco de dados será compatível. *versão* é **tinyint**, com um padrão NULL. O valor deve ser um dos seguintes:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum parâmetro for especificado ou se o *nome* parâmetro não for especificado, **sp_dbcmptlevel** retornará um erro.  
  
 Se *nome* for especificado sem *versão*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] retorna uma mensagem que exibe o nível de compatibilidade atual do banco de dados especificado.  
  
## <a name="remarks"></a>Comentários  
 Para obter uma descrição de níveis de compatibilidade, consulte [nível de compatibilidade de ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o proprietário do banco de dados, os membros do **sysadmin** função fixa de servidor e o **db_owner** função de banco de dados fixa (se você estiver alterando o banco de dados atual) pode executar este procedimento.  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
