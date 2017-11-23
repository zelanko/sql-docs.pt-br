---
title: Substituir (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs: TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a50c0b7220eba654df21349e2fd3cd57b9a0d7d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Substitui todas as ocorrências de um valor da cadeia de caracteres especificado por outro valor de cadeia de caracteres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 É a cadeia de caracteres [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser pesquisada. *string_expression* pode ser de um tipo de dados caractere ou binário.  
  
 *string_*padrão  
 É a subcadeia de caracteres a ser localizada. *string_pattern* pode ser de um tipo de dados caractere ou binário. *string_pattern* não pode ser uma cadeia de caracteres vazia (") e não deve exceder o número máximo de bytes que cabe em uma página.  
  
 *string_*substituição  
 É a cadeia de caracteres de substituição. *string_replacement* pode ser de um tipo de dados caractere ou binário.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **nvarchar** se um dos argumentos de entrada é do **nvarchar** o tipo de dados; caso contrário, REPLACE retornará **varchar**.  
  
 Retornará NULL se qualquer um dos argumentos for NULL.  
  
 Se *string_expression* não é do tipo **varchar (max)** ou **nvarchar (max), REPLACE** trunca o valor de retorno em 8.000 bytes. Para retornar valores maiores que 8.000 bytes, *string_expression* devem ser convertidos explicitamente a um tipo de dados de valor grande.  
  
## <a name="remarks"></a>Comentários  
 REPLACE efetua comparações com base no agrupamento da entrada. Para realizar uma comparação em um agrupamento especificado, você pode usar [COLLATE](~/t-sql/statements/collations.md) para aplicar um agrupamento explícito à entrada.  
  
 0x0000 (**char(0)**) é um caractere indefinido em agrupamentos do Windows e não pode ser incluído em REPLACE.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir substitui a cadeia de caracteres `cde` em `abcdefghi` por `xxx`.  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 O exemplo a seguir usa a função `COLLATE`.  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
