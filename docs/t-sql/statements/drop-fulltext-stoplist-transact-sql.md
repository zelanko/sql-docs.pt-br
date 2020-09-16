---
description: DROP FULLTEXT STOPLIST (Transact-SQL)
title: DROP FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dd3cc4e5679a5f766f02d7630b3b760290203d43
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549290"
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Descarta uma lista de palavras irrelevantes (stoplist) de texto completo do banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  Só há suporte para CREATE FULLTEXT STOPLIST no nível de compatibilidade 100 e superior. Nos níveis de compatibilidade 80 e 90, a lista de palavras irrelevantes do sistema sempre é atribuída ao banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *stoplist_name*  
 É o nome da lista de palavras irrelevantes de texto completo a ser descartada do banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Haverá falha em DROP FULLTEXT STOPLIST se qualquer índice de texto completo fizer referência à lista de palavras irrelevantes de texto completo que está sendo descartada.  
  
## <a name="permissions"></a>Permissões  
 Para remover uma lista de palavras irrelevantes, é necessário ter permissão DROP na lista de palavras irrelevantes ou associação nas funções fixas **db_owner** ou **db_ddladmin** do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta uma lista de palavras irrelevantes de texto completo denominada `myStoplist`.  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  
