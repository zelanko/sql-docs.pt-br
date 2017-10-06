---
title: SUPERIOR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7572e82178b211fba9967a88cb16c20d059c7b52
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="upper-transact-sql"></a>UPPER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma expressão de caractere com dados de caractere em minúsculas convertidos em maiúsculas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários.  
  
 *character_expression* deve ser de um tipo de dados que é implicitamente conversível em **varchar**. Caso contrário, use [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) para converter explicitamente *character_expression*.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar** ou **nvarchar**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa as funções `UPPER` e `RTRIM` para retornar o sobrenome das pessoas na tabela `Person` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], de maneira que seja convertido em maiúsculas, cortado e concatenado com o nome.  
  
```  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM Person.Person  
ORDER BY LastName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir usa o `UPPER` e `RTRIM` funções para retornar o sobrenome das pessoas no `dbo.DimEmployee` para que ele está em letras maiusculas, cortado e concatenado com o nome de tabela.  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 Este é um conjunto de resultados parcial.  
  
 ```
Name
------------------------------
ABBAS, Syed
ABERCROMBIE, Kim
ABOLROUS, Hazem
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


