---
title: STUFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46ccac4e4cdacea4caa8be6d31561ceb145f1969
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111326"
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A função STUFF insere uma cadeia de caracteres em outra cadeia de caracteres. Ela exclui um comprimento especificado de caracteres da primeira cadeia na posição inicial e, em seguida, insere a segunda cadeia na primeira, na posição inicial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *character_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caractere. *character_expression* pode ser uma constante, uma variável ou uma coluna de dados binários ou de caracteres.  
  
 *start*  
 É um valor de inteiro que especifica o local para iniciar a exclusão e a inserção. Se *start* for negativo ou zero, uma cadeia de caracteres nula será retornada. Se *start* for maior que a primeira *character_expression*, uma cadeia de caracteres nula será retornada. *start* pode ser do tipo **bigint**.  
  
 *length*  
 É um inteiro que especifica o número de caracteres a serem excluídos. Se *length* for negativo, uma cadeia de caracteres nula será retornada. Se *length* for maior que a primeira *character_expression*, a exclusão ocorrerá até o último caractere da última *character_expression*.  Se *length* for zero, a inserção ocorrerá no local *start* e nenhum caractere será excluído. *length* pode ser do tipo **bigint**.

 *replaceWith_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caractere. *character_expression* pode ser uma constante, uma variável ou uma coluna de dados binários ou de caracteres. Essa expressão substitui os caracteres de *length* da *character_expression* começando em *start*. Fornecer `NULL` como a *replaceWith_expression* remove os caracteres sem inserir nada.   
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna dados de caractere se *character_expression* é um dos tipos de dados de caractere compatíveis. Retorna dados binários se *character_expression* é um dos tipos de dados binários compatíveis.  
  
## <a name="remarks"></a>Comentários  
 Se a posição inicial ou o comprimento forem negativos, ou se a posição inicial for maior do que o comprimento da primeira cadeia de caracteres, uma cadeia nula será retornada. Se a posição de início for 0, um valor nulo será retornado. Se o comprimento a ser excluído for maior que a primeira cadeia de caracteres, a exclusão ocorrerá no primeiro caractere da primeira cadeia.  

Um erro será gerado se o valor resultante for maior que o máximo suportado pelo tipo de retorno.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 Ao usar ordenações SC, *character_expression* e *replaceWith_expression* podem incluir pares alternativos. O parâmetro de comprimento contará cada par alternativo na *character_expression* como um único caractere.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma cadeia de caracteres criada ao excluir três caracteres da primeira cadeia, `abcdef`, começando na posição `2`, em `b`, e ao inserir a segunda cadeia de caracteres no ponto de exclusão.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
