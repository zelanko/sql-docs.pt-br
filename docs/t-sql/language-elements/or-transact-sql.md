---
title: OU (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR_TSQL
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], combining
- combining conditions
- OR operator
ms.assetid: b730a256-4a63-4880-9906-65b05cd9caf2
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 590410dd84275f63bc610ac436410c7d323eb8e3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="or-transact-sql"></a>OR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Combina duas condições. Quando mais de um operador lógico é usado em uma instrução, operadores OR são avaliados depois de operadores AND. Entretanto, é possível alterar a ordem de avaliação usando parênteses.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
boolean_expression OR boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que retorna TRUE, FALSE ou UNKNOWN.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 OR retorna TRUE quando qualquer uma das condições é TRUE.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o resultado do operador OR.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|UNKNOWN|  
|**DESCONHECIDO**|TRUE|UNKNOWN|UNKNOWN|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a exibição `vEmployeeDepartmentHistory` para recuperar os nomes dos funcionários de `Quality Assurance` que trabalham no turno da tarde ou da noite. Se os parênteses forem omitidos, a consulta retornará funcionários de `Quality Assurance` que trabalham no turno da tarde e todos os funcionários que trabalham no turno da noite.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Shift   
FROM HumanResources.vEmployeeDepartmentHistory  
WHERE Department = 'Quality Assurance'  
   AND (Shift = 'Evening' OR Shift = 'Night');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName    LastName         Shift 
 ------------ ---------------- ------- 
 Andreas      Berglund         Evening 
 Sootha       Charncherngkha   Night
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera os nomes de funcionários que a ganhar um `BaseRate` menos de 20 ou tem um `HireDate` 1 de janeiro de 2001 ou posterior.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, BaseRate, HireDate   
FROM DimEmployee  
WHERE BaseRate < 10 OR HireDate >= '2001-01-01';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



