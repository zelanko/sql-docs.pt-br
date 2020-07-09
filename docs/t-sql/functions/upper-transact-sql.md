---
title: UPPER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc6822f890ba66df1f2d7945e411a4cd334de1bc
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004077"
---
# <a name="upper-transact-sql"></a>UPPER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma expressão de caractere com dados de caractere em minúsculas convertidos em maiúsculas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caractere. *character_expression* pode ser uma constante, uma variável ou uma coluna de dados binários ou de caracteres.  
  
 *character_expression* deve ser um tipo de dados implicitamente conversível em **varchar**. Caso contrário, use [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) para converter *character_expression* explicitamente.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar** ou **nvarchar**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa as funções `UPPER` e `RTRIM` para retornar o sobrenome das pessoas na tabela `dbo.DimEmployee`, de maneira que seja convertido em maiúsculas, cortado e concatenado com o nome.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [LOWER &#40;Transact-SQL&#41;](../../t-sql/functions/lower-transact-sql.md)  
  
  

