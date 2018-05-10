---
title: Barra estrela (comentário de bloco) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: db614b063ac6b5f92da2f3af53d61ef10755b1d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="slash-star-block-comment-transact-sql"></a>Barra estrela (comentário de bloco) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  Indica texto fornecido pelo usuário. O texto entre /* e \*/ não é avaliado pelo servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>Argumentos  
 *text_of_comment*  
 É o texto do comentário. É composto de uma ou mais cadeias de caracteres.  
  
## <a name="remarks"></a>Remarks  
 Os comentários podem ser inseridos em uma linha separada ou dentro de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Os comentários de várias linhas precisam ser indicados por /* e \*/. Uma convenção de estilo geralmente usada para comentários de várias linhas é começar a primeira linha com /\*, as próximas linhas com \*\* e terminar com \*/.  
  
 Não há comprimento máximo para comentários.  
  
 É oferecido suporte a comentários aninhados. Se o padrão de caracteres /* ocorrer em qualquer lugar dentro de um comentário existente, ele será tratado como o início de um comentário aninhado e, portanto, exigirá uma marca de comentário \*/ de fechamento. Se a marca de comentário de fechamento não existir, um erro será gerado.  
  
 Por exemplo, o código a seguir gera um erro.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 Para solucionar esse erro, faça a seguinte alteração.  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa comentários para explicar o que a seção do código é suposta a fazer.  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [-- &#40;Comment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [Linguagem de controle de fluxo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

