---
title: "Operadores de comparação (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: cd8dcf23064d6caae62d10065c9aa3731823e99b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="comparison-operators-transact-sql"></a>Operadores de comparação (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os operadores de comparação testam se duas expressões são iguais. Os operadores de comparação podem ser usados em todas as expressões, exceto em expressões dos tipos de dados **text**, **ntext** ou **image**. A tabela a seguir lista os operadores de comparação [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Operador|Significado|  
|--------------|-------------|  
|[= (Igual a)](../../t-sql/language-elements/equals-transact-sql.md)|Igual a|  
|[> (Maior que)](../../t-sql/language-elements/greater-than-transact-sql.md)|Maior que|  
|[< (Menor que)](../../t-sql/language-elements/less-than-transact-sql.md)|Menor que|  
|[>= (Maior ou igual a)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|Maior que ou igual a|  
|[<= (Menor ou igual a)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|Menor que ou igual a|  
|[<> (Diferente de)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|É diferente de|  
|[!= (Não é igual a)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|Diferente de (não é padrão ISO)|  
|[!< (Não é menor que)](../../t-sql/language-elements/not-less-than-transact-sql.md)|Não é menor que (não é padrão ISO)|  
|[!> (Não é maior que)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|Não é maior que (não é padrão ISO)|  
  
## <a name="boolean-data-type"></a>Tipo de dados boolianos  
 O resultado de um operador de comparação tem o tipo de dados **Boolean**. Ele tem três valores: TRUE, FALSE e UNKNOWN. Expressões que retornam um tipo de dados **Boolean** são conhecidas como expressões boolianas.  
  
 Ao contrário de outros tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um tipo de dados **Boolean** não pode ser especificado como o tipo de dados de uma variável ou coluna de tabela e não pode ser retornado em um conjunto de resultados.  
  
 Quando SET ANSI_NULLS é ON, um operador com uma ou duas expressões NULL retorna UNKNOWN. Quando SET ANSI_NULLS é OFF, as mesmas regras se aplicam, exceto que um operador igual (=) retorna TRUE quando as duas expressões são NULL. Por exemplo, NULL = NULL retorna TRUE quando SET ANSI_NULLS é OFF.  
  
 Expressões com tipos de dados **Boolean** são usadas na cláusula WHERE para filtrar as linhas que se qualificam para os critérios de pesquisa e nas instruções de linguagem de controle de fluxo, como IF e WHILE, por exemplo:  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
