---
title: SELECT @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44fd55346e8a4a27f1d3301d6cb3c6bdf7bdf548
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="select-localvariable-transact-sql"></a>SELECT @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define uma variável local com o valor de uma expressão.  
  
 Para atribuir variáveis, recomendamos o uso de [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md), em vez de SELECT @*local_variable*.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
@*local_variable*  
 É uma variável declarada para a qual um valor será atribuído.  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
Atribui o valor à direita à variável da esquerda.  
  
Operador de atribuição composto:  
  |operador |action |   
  |-----|-----|  
  | = | Atribui a expressão a seguir à variável. |  
  | += | Adicionar e atribuir |   
  | -= | Subtrair e atribuir |  
  | \*= | Multiplicar e atribuir |  
  | /= | Dividir e atribuir |  
  | %= | Módulo e atribuir |  
  | &= | AND bit a bit e atribuir |  
  | ^= | XOR bit a bit e atribuir |  
  | \|= | OR bit a bit e atribuir |  
  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida. Isso inclui uma subconsulta escalar.  
  
## <a name="remarks"></a>Remarks  
 SELECT @*local_variable* normalmente é usado para retornar um único valor na variável. No entanto, quando *expression* é o nome de uma coluna, ela pode retornar vários valores. Se a instrução SELECT retornar mais de um valor, à variável será atribuído o último valor retornado.  
  
 Se a instrução SELECT não retornar nenhuma linha, a variável reterá seu valor atual. Se *expression* for uma subconsulta escalar que não retorna nenhum valor, a variável será definida como NULL.  
  
 Uma instrução SELECT pode inicializar várias variáveis locais.  
  
> [!NOTE]  
>  Uma instrução SELECT que contém uma atribuição de variável não pode ser usada também para executar operações típicas de recuperação de conjunto de resultados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. Usar SELECT @local_variable para retornar um único valor  
 No exemplo a seguir, a variável `@var1` recebe `Generic Name` com seu valor. A consulta na tabela `Store` não retorna linhas porque o valor especificado para `CustomerID` não existe na tabela. A variável retém o valor `Generic Name`.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>B. Usar SELECT @local_variable para retornar nulo  
 No exemplo a seguir, uma subconsulta é usada para atribuir um valor a `@var1`. Como o valor solicitado para `CustomerID` não existe, a subconsulta não retorna valores e a variável é definida como `NULL`.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
