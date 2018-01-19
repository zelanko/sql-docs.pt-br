---
title: STUFF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2017
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
- STUFF
- STUFF_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 10edb8b1b1e3008321bc03e2e65419dca8956f86
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  A função STUFF insere uma cadeia de caracteres em outra cadeia de caracteres. Ela exclui um comprimento especificado de caracteres da primeira cadeia na posição inicial e, em seguida, insere a segunda cadeia na primeira, na posição inicial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários.  
  
 *start*  
 É um valor de inteiro que especifica o local para iniciar a exclusão e a inserção. Se *iniciar* for negativo ou zero, uma cadeia de caracteres nula será retornada. Se *iniciar* é maior do que o primeiro *character_expression*, uma cadeia de caracteres nula será retornada. *Iniciar* pode ser do tipo **bigint**.  
  
 *comprimento*  
 É um inteiro que especifica o número de caracteres a serem excluídos. Se *comprimento* é negativo, uma cadeia de caracteres nula será retornada. Se *comprimento* é maior do que o primeiro *character_expression*, exclusão ocorrerá até para o último caractere na última *character_expression*.  Se *comprimento* for zero, a inserção ocorre antes do primeiro caractere na cadeia de caracteres. *comprimento* pode ser do tipo **bigint**.

 *replaceWith_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários. Essa expressão substitui *comprimento* caracteres de *character_expression* começando no *iniciar*. Fornecendo `NULL` como o *replaceWith_expression*, remove os caracteres sem inserir nada.   
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna dados de caractere se *character_expression* é um dos tipos de dados de caracteres com suporte. Retorna dados binários se *character_expression* é um dos tipos de dados binários com suporte.  
  
## <a name="remarks"></a>Remarks  
 Se a posição inicial ou o comprimento forem negativos, ou se a posição inicial for maior do que o comprimento da primeira cadeia de caracteres, uma cadeia nula será retornada. Se a posição de início for 0, um valor nulo será retornado. Se o comprimento a ser excluído for maior que a primeira cadeia de caracteres, a exclusão ocorrerá no primeiro caractere da primeira cadeia.  

Um erro será gerado se o valor resultante for maior que o máximo suportado pelo tipo de retorno.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 Ao usar agrupamentos SC, ambos *character_expression* e *replaceWith_expression* podem incluir pares substitutos. O parâmetro de comprimento contará cada substituto *character_expression* como um único caractere.  
  
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
  
## <a name="see-also"></a>Consulte também  
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
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
