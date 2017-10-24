---
title: "-(Comentário) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a03aff79db25c07fc828145177e29196405a9264
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="---comment-transact-sql"></a>-- (Comentário) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica texto fornecido pelo usuário. Os comentários podem ser inseridos em uma linha separada, aninhados no final de uma linha de comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] ou em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. O servidor não avalia o comentário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>Argumentos  
 *text_of_comment*  
 É a cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
 Use dois hífens (--) para comentários de uma linha ou aninhados. Comentários inseridos com -- são finalizados pelo caractere de nova linha. Não há comprimento máximo para comentários. A tabela a seguir lista os atalhos do teclado que podem ser usados para comentar ou remover comentários do texto.  
  
|Ação|Standard|  
|------------|--------------|  
|Transformar o texto selecionado em um comentário|CTRL+K, CTRL+C|  
|Remover comentário do texto selecionado|CTRL+K, CTRL+U|  
  
 Para obter mais informações sobre atalhos de teclado, consulte [atalhos de teclado do SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Para comentários de várias linhas, consulte [barra estrela de comentário &#40; Transact-SQL &#41; ](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa os caracteres de comentário --.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem de controle de fluxo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

