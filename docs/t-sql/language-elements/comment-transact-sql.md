---
title: "-(Comentário) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs: TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a5615aa149b6f7a36b962550fa6094d3badae0a2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="---comment-transact-sql"></a>-- (Comentário) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
 Para comentários de várias linhas, consulte [estrela de barra &#40; Bloco de comentário &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
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
  
  
