---
title: "Expressões de caminho JSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 829f7d57569e55eed5bc50634c5a9baad6f7d8ee
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="json-path-expressions-sql-server"></a>Expressões de demarcador JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use demarcadores JSON para fazer referência às propriedades de objetos JSON. Demarcadores JSON usam uma sintaxe semelhante a Javascript.  
  
 Você precisa fornecer uma expressão de demarcador ao chamar as funções a seguir.  
  
-   Quando você chama **OPENJSON** para criar uma exibição relacional de dados JSON. Para obter mais informações, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Quando você chama **JSON_VALUE** para extrair um valor de texto JSON. Para obter mais informações, veja [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Quando você chama **JSON_QUERY** para extrair um objeto ou uma matriz JSON. Para obter mais informações, veja [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Quando você chama **JSON_MODIFY** para atualizar o valor de uma propriedade em uma cadeia de caracteres JSON. Para obter mais informações, veja [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Partes de uma expressão de caminho
 Uma expressão de demarcador tem dois componentes.  
  
1.  O [modo demarcador](#PATHMODE) opcional, **lax** ou **strict**.  
  
2.  O [demarcador](#PATH) em si.  
  
##  <a name="PATHMODE"></a> Path mode  
 No início da expressão de demarcador, opcionalmente, declare o modo demarcador especificando a palavra-chave **lax** ou **strict**. O padrão é **lax**.  
  
-   No modo **lax** , as funções retornam valores vazios se a expressão do demarcador contiver um erro. Por exemplo, se você solicitar o valor **$.name**, e o texto JSON não contiver uma chave **name** , a função retornará nula.  
  
-   No modo **strict** , as funções gerarão erros se a expressão do demarcador contiver um erro.  
  
##  <a name="PATH"></a> Path  
 Após a declaração de modo de demarcador opcional, especifique o demarcador em si.  
  
-   O símbolo de cifrão (`$`) representa o item de contexto.  
  
-   O demarcador de propriedade é um conjunto de etapas de demarcador. As etapas do demarcador podem conter os seguintes elementos e operadores.  
  
    -   Nomes de chave. Por exemplo, `$.name` e `$."first name"`. Se o nome da chave começar com um sinal de cifrão ou contiver caracteres especiais como espaços, coloque-o entre aspas.   
  
    -   Elementos da matriz. Por exemplo, `$.product[3]`. Matrizes são baseadas em zero.  
  
    -   O operador ponto (`.`) indica um membro de um objeto.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos nesta seção fazem referência ao texto JSON a seguir.  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 A tabela a seguir mostra alguns exemplos de expressões de demarcador.  
  
|Expressão de demarcador|Valor|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane", "surname": null, "active": true }|  
|$.people[1].surname|nulo|  
|$|{ "people": [ { "name": "John", "surname": "Doe" },<br />   { "name": "Jane", "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Como as funções internas tratam caminhos duplicados  
 Se o texto JSON contiver propriedades duplicadas – por exemplo, duas chaves com o mesmo nome no mesmo nível –, as funções JSON_VALUE e JSON_QUERY retornarão o primeiro valor que corresponde ao caminho. Para analisar um objeto JSON que contém chaves duplicadas, use OPENJSON, conforme mostrado no exemplo a seguir.  
  
```tsql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  
  
## <a name="see-also"></a>Consulte também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

