---
title: CONCAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6968766b2d7d447f21fccc6425935017a6943778
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70122952"
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Essa função retorna uma cadeia de caracteres resultante de concatenação ou junção de dois ou mais valores de cadeia de caracteres de ponta a ponta. (Para adicionar um valor de separação durante a concatenação, consulte [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*string_value*  
Um valor de cadeia de caracteres para concatenação com outros valores. A função `CONCAT` requer pelo menos dois argumentos *string_value* e não mais do que 254 argumentos *string_value*.
  
## <a name="return-types"></a>Tipos de retorno  
*string_value*  
Um valor de cadeia de caracteres cujos comprimento e tipo dependem da entrada.
  
## <a name="remarks"></a>Comentários  
`CONCAT` usa um número variável de argumentos de cadeia de caracteres e os concatena em uma única cadeia de caracteres. Exige um mínimo de dois valores de entrada; caso contrário, `CONCAT` gerará um erro. `CONCAT` converte implicitamente todos os argumentos nos tipos de cadeia de caracteres antes da concatenação. `CONCAT` converte implicitamente os valores nulos em cadeias de caracteres vazias. Se `CONCAT` receber argumentos com todos os valores **nulo**, retornará uma cadeia de caracteres vazia do tipo **varchar**(1). A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) para obter mais informações sobre conversões de tipo de dados.
  
O tipo de retorno depende do tipo dos argumentos. Esta tabela ilustra o mapeamento:
  
|Tipo de entrada|Tipo e comprimento da saída|  
|---|---|
|1. Qualquer argumento de<br><br />um tipo de sistema do SQL-CLR<br><br />a UDT SQL-CLR<br><br />ou<br><br />`nvarchar(max)`|**nvarchar(max)**|  
|2. Caso contrário, qualquer argumento de tipo<br><br />**varbinary(max)**<br><br />ou<br><br />**varchar(max)**|**varchar(max)** , a menos que um dos parâmetros seja um **nvarchar** de qualquer comprimento. Nesse caso, `CONCAT` retorna um resultado do tipo **nvarchar(max)** .|  
|3. Caso contrário, qualquer argumento de tipo **nvarchar** de no máximo 4.000 caracteres<br><br />( **nvarchar**(<= 4000) )|**nvarchar**(<= 4000)|  
|4. Em todos os outros casos|**varchar**(<=8.000) (um **varchar** de no máximo 8.000 caracteres), a menos que um dos parâmetros seja um nvarchar de qualquer comprimento. Naquele caso, `CONCAT` retorna um resultado do tipo **nvarchar(max)** .|  
  
Quando `CONCAT` recebe argumentos de entrada **nvarchar** de comprimento <=4.000 caracteres, ou argumentos de entrada **varchar** de comprimento <=8.000 caracteres, conversões implícitas poderão afetar o comprimento das resultado. Outros tipos de dados têm comprimentos diferentes quando são convertidos implicitamente em cadeias de caracteres. Por exemplo, um **int** (14) tem um comprimento de cadeia de caracteres de 12, enquanto um **float** tem um comprimento de 32. Portanto, uma concatenação de dois inteiros retornará um resultado com um comprimento não inferior a 24.
  
Se nenhum dos argumentos de entrada tiver um tipo LOB (objeto grande) com suporte, o tipo retornado será truncado para 8.000 caracteres, independentemente do tipo retornado. Esse truncamento preserva espaço e dá suporte à eficiência na geração do plano.
  
A função CONCAT pode ser executada remotamente em um servidor vinculado da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e superiores. Para servidores vinculados mais antigos, a operação CONCAT ocorrerá localmente, depois que o servidor vinculado retornar os valores não concatenados.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-concat"></a>a. Usando CONCAT  
  
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
  


