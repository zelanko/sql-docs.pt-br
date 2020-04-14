---
title: REPLACE (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a função REPLACE, que substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93ab1cb4930e90973a88487d72effaa863aa6c36
ms.sourcegitcommit: 2426a5e1abf6ecf35b1e0c062dc1e1225494cbb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80517492"
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Substitui todas as ocorrências de um valor da cadeia de caracteres especificado por outro valor de cadeia de caracteres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 É a [expression](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres a ser pesquisada. *string_expression* pode ser de um tipo de dados de caractere ou binários.  
  
 *string\_pattern*  
 É a subcadeia de caracteres a ser localizada. *string_pattern* pode ser de um caractere ou de tipo de dados binários. *string_pattern* não pode ser uma cadeia de caracteres vazia (") e não deve exceder o número máximo de bytes que cabem em uma página.  
  
 *string\_replacement*  
 É a cadeia de caracteres de substituição. *string_replacement* pode ser de um tipo de dados de caractere ou binários.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **nvarchar** se um dos argumentos de entrada é do tipo de dados **nvarchar**; caso contrário, REPLACE retorna **varchar**.  
  
 Retornará NULL se qualquer um dos argumentos for NULL.  
  
 Se *string_expression* não for do tipo **varchar(max)** ou **nvarchar(max), REPLACE** truncará o valor retornado em 8.000 bytes. Para retornar valores com mais de 8.000 bytes, *string_expression* deve ser convertida explicitamente em um tipo de dados de valor grande.  
  
## <a name="remarks"></a>Comentários  
 REPLACE efetua comparações com base na ordenação da entrada. Para fazer uma comparação em uma ordenação especificada, use [COLLATE](~/t-sql/statements/collations.md) para aplicar uma ordenação explícita à entrada.  
  
 0x0000 (**char(0)** ) é um caractere indefinido em ordenações do Windows e não pode ser incluído em REPLACE.  
  
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

  
## <a name="see-also"></a>Consulte Também  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
