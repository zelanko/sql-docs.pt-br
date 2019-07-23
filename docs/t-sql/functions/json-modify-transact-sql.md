---
title: JSON_MODIFY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: d340d362301698f7dfaef28476ea659b948163bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109377"
---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>Argumentos

 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou de uma coluna que contém o texto JSON.  
  
 **JSON_MODIFY** retornará um erro se *expression* não contiver um JSON válido.  
  
 *path*  
 Uma expressão de caminho JSON que especifica a propriedade a ser atualizada.

 *path* tem a seguinte sintaxe:  
  
 `[append] [ lax | strict ] $.<json path>`  
  
- *append*  
    Modificador opcional que especifica que o novo valor deve ser acrescentado à matriz referenciada por *\<json path>* .  
  
- *lax*  
    Especifica que a propriedade referenciada por *\<json path>* não precisa existir. Se a propriedade não estiver presente, JSON_MODIFY tentará inserir o novo valor no caminho especificado. A inserção poderá falhar se a propriedade não puder ser inserida no caminho. Se você não especificar *lax* ou *strict*, *lax* será o modo padrão.  
  
- *strict*  
    Especifica que a propriedade referenciada por *\<json path>* deve estar na expressão JSON. Se a propriedade não estiver presente, JSON_MODIFY retornará um erro.  
  
- *\<json path>*  
    Especifica o caminho para a propriedade a ser atualizado. Para obter mais informações, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e no [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *path*.

**JSON_MODIFY** retornará um erro se o formato de *path* não for válido.  
  
 *newValue*  
 O novo valor para a propriedade especificada por *path*.  
  
 No modo incerto, JSON_MODIFY exclui a chave especificada se o novo valor é NULL.  
  
JSON_MODIFY faz o escape de todos os caracteres especiais no novo valor se o tipo do valor é NVARCHAR ou VARCHAR. Um valor de texto não é seguido de caracteres de escape se ele é um JSON formatado corretamente produzido por FOR JSON, JSON_QUERY ou JSON_MODIFY.  
  
## <a name="return-value"></a>Valor retornado

 Retorna o valor atualizado de *expression* como um texto JSON formatado corretamente.  
  
## <a name="remarks"></a>Remarks

 A função JSON_MODIFY permite atualizar o valor de uma propriedade existente, inserir um novo par de chave/valor ou excluir uma chave com base em uma combinação de modos e valores fornecidos.  
  
 A tabela a seguir compara o comportamento de **JSON_MODIFY** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (incerto ou estrito), confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Valor existente|O caminho existe|Modo incerto|Modo estrito|  
|--------------------|-----------------|--------------|-----------------|  
|Não NULL|Sim|Atualize o valor existente.|Atualize o valor existente.|  
|Não NULL|Não|Tente criar um novo par de chave/valor no caminho especificado.<br /><br /> Isso poderá falhar. Por exemplo, se você especificar o caminho `$.user.setting.theme`, JSON_MODIFY não inserirá a chave `theme`, caso os objetos `$.user` ou `$.user.settings` não existam ou caso as configurações sejam uma matriz ou um valor escalar.|Erro – INVALID_PROPERTY|  
|NULL|Sim|Exclua a propriedade existente.|Defina o valor existente como nulo.|  
|NULL|Não|Nenhuma ação. O primeiro argumento é retornado como o resultado.|Erro – INVALID_PROPERTY|  
  
 No modo incerto, JSON_MODIFY tenta criar um novo par de chave/valor, mas em alguns casos, ele pode falhar.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example---basic-operations"></a>Exemplo – operações básicas

 O exemplo a seguir mostra as operações básicas que podem ser executadas com um texto JSON.  
  
 **Consulta**
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **Resultados**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>Exemplo – várias atualizações

 Com JSON_MODIFY, você pode atualizar apenas uma propriedade. Se precisar fazer várias atualizações, use várias chamadas JSON_MODIFY.  
  
 **Consulta**
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **Resultados**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>Exemplo – renomear uma chave  
 O exemplo a seguir mostra como renomear uma propriedade em texto JSON com a função JSON_MODIFY. Primeiro, você pode usar o valor de uma propriedade existente e inseri-lo como um novo par de chave/valor. Em seguida, exclua a chave antiga definindo o valor da propriedade antiga como NULL.  
  
 **Consulta**
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **Resultados**
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 Se você não converter o novo valor em um tipo numérico, JSON_MODIFY o tratará como texto e o colocará entre aspas duplas.  
  
### <a name="example---increment-a-value"></a>Exemplo – incrementar um valor

 O exemplo a seguir mostra como incrementar o valor de uma propriedade em texto JSON com a função JSON_MODIFY. Primeiro, você pode usar o valor da propriedade existente e inseri-lo como um novo par de chave/valor. Em seguida, exclua a chave antiga definindo o valor da propriedade antiga como NULL.  
  
 **Consulta**
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **Resultados**
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>Exemplo – modificar um objeto JSON

 JSON_MODIFY trata o argumento *newValue* como um texto sem formatação, mesmo que ele contém um texto JSON formatado corretamente. Como resultado, a saída JSON da função é colocada entre aspas duplas e todos os caracteres especiais têm escape, conforme mostrado no exemplo a seguir.  
  
 **Consulta**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **Resultados**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 Para evitar o escape automático, forneça *newValue* usando a função JSON_QUERY. JSON_MODIFY sabe que o valor retornado por JSON_MODIFY é um JSON formatado corretamente e, portanto, ele não faz o escape do valor.  
  
 **Consulta**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **Resultados**
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>Exemplo – atualizar uma coluna JSON

 O exemplo a seguir atualiza o valor de uma propriedade em uma coluna de tabela que contém JSON.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>Consulte Também

 [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  