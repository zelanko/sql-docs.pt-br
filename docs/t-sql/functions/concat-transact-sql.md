---
title: CONCAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
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
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71f52ba08f2fd5fe94af4b16dbcac06746564e09
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna uma cadeia de caracteres que é o resultado da concatenação de dois ou mais valores. (Para adicionar um valor de separação durante a concatenação, consulte [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*string_value*  
Um valor de cadeia de caracteres para concatenação com outros valores.
  
## <a name="return-types"></a>Tipos de retorno
Cadeia de caracteres, comprimento e tipo dos quais a entrada depende.
  
## <a name="remarks"></a>Remarks  
**CONCAT** usa um número variável de argumentos de cadeia de caracteres e os concatena em uma única cadeia de caracteres. Exige um mínimo de dois valores de entrada; caso contrário, é gerado um erro. Todos os argumentos são convertidos implicitamente em tipos de cadeia de caracteres e depois concatenados. Os valores nulos são convertidos implicitamente em uma cadeia de caracteres vazia. Se todos os argumentos forem nulos, uma cadeia de caracteres vazia do tipo **varchar**(1) será retornada. A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Para obter mais informações sobre conversões de tipo de dados, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
O tipo de retorno depende do tipo dos argumentos. A tabela a seguir ilustra o mapeamento.
  
|Tipo de entrada|Tipo e comprimento da saída|  
|---|---|
|Se qualquer argumento for um tipo do sistema SQL-CLR, um SQL-CLR UDT ou um `nvarchar(max)`|**nvarchar(max)**|  
|Caso contrário, se qualquer argumento for **varbinary(max)** ou **varchar(max)**|**varchar(max)**, a menos que um dos parâmetros seja um **nvarchar** de qualquer comprimento. Nesse caso, o resultado será **nvarchar(max)**.|  
|Caso contrário, se qualquer argumento for **nvarchar**(<= 4000)|**nvarchar**(<= 4000)|  
|Caso contrário, em todos os outros casos|**varchar**(<= 8000), a menos que um dos parâmetros seja um nvarchar de qualquer comprimento. Nesse caso, o resultado será **nvarchar(max)**.|  
  
Quando os argumentos forem <= 4000 para **nvarchar** ou <= 8000 para **varchar**, as conversões implícitas poderão afetar o comprimento do resultado. Outros tipos de dados têm comprimentos diferentes quando eles são convertidos implicitamente em cadeias de caracteres. Por exemplo, um **int** (14) tem um comprimento de cadeia de caracteres de 12, enquanto um **float** tem um comprimento de 32. Portanto, o resultado da concatenação de dois inteiros tem um comprimento não menor que 24.
  
Se nenhum dos argumentos de entrada for de um tipo LOB (large object, objeto grande) com suporte, o tipo de retorno será truncado para 8000 de comprimento, independentemente do tipo de retorno. Esse truncamento preserva espaço e dá suporte à eficiência na geração do plano.
  
A função CONCAT pode ser executada remotamente em um servidor vinculado que seja da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e superiores. Para servidores vinculados mais antigos, a operação CONCAT será executada localmente depois que os valores não concatenados forem retornados do servidor vinculado.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-concat"></a>A. Usando CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. Usando CONCAT com valores NULL  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


