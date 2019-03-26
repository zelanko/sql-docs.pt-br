---
title: STRING_ESCAPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current||>= sql-server-2016||=azure-sqldw-latest||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 8c283fd85aedec31f8774145155fe3b1d7ac9c10
ms.sourcegitcommit: 1a182443e4f70f4632617cfef4efa56d898e64e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58342938"
---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Faz o escape dos caracteres especiais em textos e retorna o texto com caracteres com escape. **STRING_ESCAPE** é uma função determinística.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>Argumentos  
 *text*  
 É uma expressão **nvarchar**[expression](../../t-sql/language-elements/expressions-transact-sql.md) que representa o objeto que deve ter escape.  
  
 *type*  
 Regras de escape que serão aplicadas. Atualmente, o valor com suporte é `'json'`.  
  
## <a name="return-types"></a>Tipos de retorno  
 Texto **nvarchar(max)** com caracteres especiais e de controle com escape. No momento, **STRING_ESCAPE** somente pode fazer o escape de caracteres especiais JSON mostrados nas tabelas a seguir.  
  
|Caractere especial|Sequência codificada|  
|-----------------------|----------------------|  
|Aspas (")|\\"|  
|Barra invertida (\\)|\\\|  
|Barra "/"|\\/|  
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
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  Fazer o escape do texto de acordo com as regras de formatação do JSON  
 A consulta a seguir faz o escape de caracteres especiais usando regras do JSON e retorna o texto com escape.  
  
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
  
### <a name="b-format-json-object"></a>b. Formatar objeto JSON  
 A consulta a seguir cria o texto JSON com base nas variáveis de número e cadeia de caracteres e faz o escape dos caracteres JSON especiais em variáveis.  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
