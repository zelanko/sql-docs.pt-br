---
title: JSON_MODIFY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70f2c1456da6469c39389fada6a74ccf46383582
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou uma coluna que contém o texto JSON.  
  
 **JSON_MODIFY** retornará um erro se *expressão* não contém um JSON válido.  
  
 *caminho*  
 Uma expressão de caminho JSON que especifica a propriedade para atualizar.

 *caminho* tem a seguinte sintaxe:  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *Acrescentar*  
    Modificador opcional que especifica que o novo valor deve ser acrescentado à matriz referenciada por  *\<caminho json >*.  
  
-   *incerta*  
    Especifica que a propriedade referenciada por  *\<caminho json >* não precisa existir. Se a propriedade não estiver presente, JSON_MODIFY tenta inserir o novo valor no caminho especificado. Inserção pode falhar se a propriedade não pode ser inserida no caminho. Se você não especificar *lax* ou *estrito*, *lax* é o modo padrão.  
  
-   *estrito*  
    Especifica que a propriedade referenciada por  *\<caminho json >* devem estar na expressão de JSON. Se a propriedade não estiver presente, JSON_MODIFY retornará um erro.  
  
-   *\<caminho JSON >*  
    Especifica o caminho para a propriedade atualizar. Para obter mais informações, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e em [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *caminho*.

**JSON_MODIFY** retornará um erro se o formato de *caminho* não é válido.  
  
 *newValue*  
 O novo valor para a propriedade especificada pelo *caminho*.  
  
 No modo de lax JSON_MODIFY exclui a chave especificada se o novo valor é NULL.  
  
JSON_MODIFY ignora todos os caracteres especiais no novo valor, se o tipo do valor for NVARCHAR ou VARCHAR. Um valor de texto não é ignorado se ele está corretamente formatado JSON produzida por FOR JSON, JSON_QUERY ou JSON_MODIFY.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna o valor atualizado da *expressão* como corretamente formatado texto JSON.  
  
## <a name="remarks"></a>Comentários  
 A função JSON_MODIFY permite que você atualize o valor de uma propriedade existente, insira um novo par de chave: valor ou excluir uma chave com base em uma combinação dos modos e os valores fornecidos.  
  
 A tabela a seguir compara o comportamento de **JSON_MODIFY** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (lax ou strict), consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Valor existente|Caminho existe|Modo incerto|Modo estrito|  
|--------------------|-----------------|--------------|-----------------|  
|Não nulo|Sim|Atualize o valor existente.|Atualize o valor existente.|  
|Não nulo|Não|Tente criar um novo par de chave: valor no caminho especificado.<br /><br /> Isso pode falhar. Por exemplo, se você especificar o caminho `$.user.setting.theme`, JSON_MODIFY não inserir a chave `theme` se o `$.user` ou `$.user.settings` objetos não existirem, ou se as configurações é uma matriz ou um valor escalar.|Erro – INVALID_PROPERTY|  
|NULL|Sim|Exclua a propriedade existente.|Defina o valor existente como nulo.|  
|NULL|Não|Nenhuma ação. O primeiro argumento é retornado como o resultado.|Erro – INVALID_PROPERTY|  
  
 No modo de lax JSON_MODIFY tenta criar um novo par de chave: valor, mas em alguns casos pode falhar.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example---basic-operations"></a>Exemplo – operações básicas  
 O exemplo a seguir mostra as operações básicas que podem ser feitas com texto JSON.  
  
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
 Com JSON_MODIFY, você pode atualizar apenas uma propriedade. Se você precisa fazer várias atualizações, você pode usar várias chamadas JSON_MODIFY.  
  
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
  
### <a name="example---rename-a-key"></a>Exemplo: renomear uma chave  
 O exemplo a seguir mostra como renomear uma propriedade em texto JSON com a função JSON_MODIFY. Primeiro, você pode pegar o valor de uma propriedade existente e inseri-lo como um novo par de chave: valor. Em seguida, você pode excluir a chave antiga, definindo o valor da propriedade antiga como NULL.  
  
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
  
 Se você não converter o novo valor para um tipo numérico, JSON_MODIFY a trata como texto e ao seu redor com aspas duplas.  
  
### <a name="example---increment-a-value"></a>Exemplo - um valor de incremento  
 O exemplo a seguir mostra como incrementar o valor de uma propriedade em texto JSON com a função JSON_MODIFY. Primeiro, você pode pegar o valor da propriedade existente e inseri-lo como um novo par de chave: valor. Em seguida, você pode excluir a chave antiga, definindo o valor da propriedade antiga como NULL.  
  
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
  
### <a name="example---modify-a-json-object"></a>Exemplo: modificar um objeto JSON  
 JSON_MODIFY trata o *newValue* argumento como texto sem formatação mesmo que ele contém corretamente formatado texto JSON. Como resultado, a saída JSON da função é colocada entre aspas duplas e todos os caracteres especiais são substituídos, conforme mostrado no exemplo a seguir.  
  
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
  
 Para evitar a substituição automática, fornecer *newValue* usando a função JSON_QUERY. JSON_MODIFY sabe que o valor retornado por JSON_MODIFY está corretamente formatado JSON, portanto ele não o valor de escape.  
  
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
  
### <a name="example---update-a-json-column"></a>Exemplo - atualização de uma coluna JSON  
 O exemplo a seguir atualiza o valor de uma propriedade em uma coluna de tabela que contém JSON.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

