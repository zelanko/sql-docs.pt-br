---
title: DROP FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf761059b932045cffe635fb169684718e612402
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descarta uma lista de palavras irrelevantes (stoplist) de texto completo do banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  Só há suporte para CREATE FULLTEXT STOPLIST no nível de compatibilidade 100 e superior. Nos níveis de compatibilidade 80 e 90, a lista de palavras irrelevantes do sistema sempre é atribuída ao banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 É o nome da lista de palavras irrelevantes de texto completo a ser descartada do banco de dados.  
  
## <a name="remarks"></a>Remarks  
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
  
  
