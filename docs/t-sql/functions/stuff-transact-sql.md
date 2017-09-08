---
title: COISAS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: df9a3d019f22ec8a0ba610f2dd694e45a8bd9da3
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  A função STUFF insere uma cadeia de caracteres em outra cadeia de caracteres. Ela exclui um comprimento especificado de caracteres da primeira cadeia na posição inicial e, em seguida, insere a segunda cadeia na primeira, na posição inicial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários.  
  
 *Iniciar*  
 É um valor de inteiro que especifica o local para iniciar a exclusão e a inserção. Se *iniciar* ou *comprimento* é negativo, uma cadeia de caracteres nula será retornada. Se *iniciar* é maior do que o primeiro *character_expression*, uma cadeia de caracteres nula será retornada. *Iniciar* pode ser do tipo **bigint**.  
  
 *length*  
 É um inteiro que especifica o número de caracteres a serem excluídos. Se *comprimento* é maior do que o primeiro *character_expression*, exclusão ocorrerá até para o último caractere na última *character_expression*. *comprimento* pode ser do tipo **bigint**.  
  
 *replaceWith_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários. Essa expressão substitui *comprimento* caracteres de *character_expression* começando no *iniciar*. Fornecendo `NULL` como o *replaceWith_expression*, remove os caracteres sem inserir nada.   
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna dados de caractere se *character_expression* é um dos tipos de dados de caracteres com suporte. Retorna dados binários se *character_expression* é um dos tipos de dados binários com suporte.  
  
## <a name="remarks"></a>Comentários  
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
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

