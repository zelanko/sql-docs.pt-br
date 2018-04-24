---
title: REPLACE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a3543a88968e8728550b4c845c8e776d03908af0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Substitui todas as ocorrências de um valor da cadeia de caracteres especificado por outro valor de cadeia de caracteres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 É a [expression](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres a ser pesquisada. *string_expression* pode ser de um tipo de dados de caractere ou binários.  
  
 *string_* pattern  
 É a subcadeia de caracteres a ser localizada. *string_pattern* pode ser de um caractere ou de tipo de dados binários. *string_pattern* não pode ser uma cadeia de caracteres vazia (") e não deve exceder o número máximo de bytes que cabem em uma página.  
  
 *string_* replacement  
 É a cadeia de caracteres de substituição. *string_replacement* pode ser de um tipo de dados de caractere ou binários.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **nvarchar** se um dos argumentos de entrada é do tipo de dados **nvarchar**; caso contrário, REPLACE retorna **varchar**.  
  
 Retornará NULL se qualquer um dos argumentos for NULL.  
  
 Se *string_expression* não for do tipo **varchar(max)** ou **nvarchar(max), REPLACE** truncará o valor retornado em 8.000 bytes. Para retornar valores com mais de 8.000 bytes, *string_expression* deve ser convertida explicitamente em um tipo de dados de valor grande.  
  
## <a name="remarks"></a>Remarks  
 REPLACE efetua comparações com base no agrupamento da entrada. Para fazer uma comparação em um agrupamento especificado, use [COLLATE](~/t-sql/statements/collations.md) para aplicar um agrupamento explícito à entrada.  
  
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
  
