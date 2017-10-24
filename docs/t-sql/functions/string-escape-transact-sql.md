---
title: STRING_ESCAPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ignora os caracteres especiais em textos e retorna o texto com caracteres de escape. **STRING_ESCAPE** é uma função determinística.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>Argumentos  
 *texto*  
 É um **nvarchar**[expressão](../../t-sql/language-elements/expressions-transact-sql.md) expressão que representa o objeto que deve ser de escape.  
  
 *tipo*  
 Regras de escape que serão aplicadas. Atualmente, o valor com suporte é `'json'`.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (max)** texto com especial com caracteres de escape e caracteres de controle. No momento **STRING_ESCAPE** somente podem escapar caracteres especiais do JSON mostrados nas tabelas a seguir.  
  
|Caractere especial|Sequência codificada|  
|-----------------------|----------------------|  
|Aspas (")|\\"|  
|barra invertida (\\)|\\\|  
|barra (/)|\\/|  
|Backspace|\b|  
|Avanço de formulário|\f|  
|Linha nova|\n|  
|Retorno de carro|\r|  
|Guia horizontal|\t|  
  
|Caractere de controle|Sequência codificada|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  Texto de acordo com a regras de formatação de JSON de escape  
 A consulta a seguir ignora os caracteres especiais usando regras JSON e retorna o texto de escape.  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. Objeto do formato JSON  
 A consulta a seguir cria o texto JSON de número e a cadeia de caracteres variáveis e ignora os caracteres especiais do JSON em variáveis.  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Subcadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

