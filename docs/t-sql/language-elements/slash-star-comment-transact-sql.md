---
title: "Barra de comentário estrela (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e617c6f0108906046d6c6ea983d1bbc26082709
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="slash-star-comment-transact-sql"></a>Comentário de estrela de barra (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica texto fornecido pelo usuário. O texto entre o / * e \*/ não é avaliado pelo servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>Argumentos  
 *text_of_comment*  
 É o texto do comentário. É composto de uma ou mais cadeias de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Os comentários podem ser inseridos em uma linha separada ou dentro de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. Comentários de várias linhas devem ser indicados por / * e \*/. Uma convenção de estilo frequentemente usada para comentários de várias linhas é começar a primeira linha com /\*, subsequentes linhas com \* \*e terminar com \*/.  
  
 Não há comprimento máximo para comentários.  
  
 É oferecido suporte a comentários aninhados. Se o / * padrão de caracteres ocorre em qualquer lugar dentro de um comentário existente, ele será tratado como o início de um comentário aninhado e, portanto, requer um fechamento \*/ marca de comentário. Se a marca de comentário de fechamento não existir, um erro será gerado.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [– &#40; Comentário &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [Linguagem de controle de fluxo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  


