---
description: sp_dbcmptlevel (Transact-SQL)
title: sp_dbcmptlevel (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b1571beb279f20cd5f887589b11c8fc72bec41a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493372"
---
# <a name="sp_dbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define certos comportamentos de banco de dados como sendo compatíveis com a versão especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use o [nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] name` É o nome do banco de dados para o qual o nível de compatibilidade deve ser alterado. Os nomes de banco de dados devem obedecer às regras para identificadores. o *nome* é **sysname**, com um padrão de NULL.  
  
`[ @new_cmptlevel = ] version` É a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual o banco de dados deve ser tornado compatível. a *versão* é **tinyint**, com um padrão de NULL. O valor deve ser um dos seguintes:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum parâmetro for especificado ou se o parâmetro *Name* não for especificado, **sp_dbcmptlevel** retornará um erro.  
  
 Se *Name* for especificado sem *version*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará uma mensagem exibindo o nível de compatibilidade atual do banco de dados especificado.  
  
## <a name="remarks"></a>Comentários  
 Para obter uma descrição dos níveis de compatibilidade, consulte [nível de compatibilidade de ALTER DATABASE &#40;&#41;Transact-SQL ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o proprietário do banco de dados, os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** (se você estiver alterando o banco de dados atual) podem executar este procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
