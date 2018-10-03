---
title: char e varchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6699c1b1c02f071dd95cd642f15a9b449de8e815
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824778"
---
# <a name="char-and-varchar-transact-sql"></a>char e varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esses tipos de dados são de comprimento variável ou fixo.  
  
## <a name="arguments"></a>Argumentos  
**char** [ ( *n* ) ] Dados de cadeia de caracteres não Unicode de comprimento fixo. *n* define o tamanho da cadeia de caracteres e deve ser um valor de 1 a 8.000. O tamanho do armazenamento é *n* bytes. O sinônimo ISO para **char** é **character**.
  
**varchar** [ ( *n* | **max** ) ] Dados de cadeia de caracteres não Unicode de tamanho variável. *n* define o tamanho da cadeia de caracteres e pode ser um valor de 1 a 8.000. **max** indica que o tamanho de armazenamento máximo é 2^31-1 bytes (2 GB). O tamanho do armazenamento é o tamanho real dos dados inseridos + 2 bytes. Os sinônimos ISO para **varchar** são **charvarying** ou **charactervarying**.
  
## <a name="remarks"></a>Remarks  
Quando *n* não é especificado em uma definição de dados ou instrução de declaração de variável, o tamanho padrão é 1. Quando *n* não é especificado ao usar as funções CAST e CONVERT, o tamanho padrão é 30.
  
Os objetos que usam **char** ou **varchar** são atribuídos ao agrupamento padrão do banco de dados, a menos que um agrupamento específico seja atribuído usando da cláusula COLLATE. O agrupamento controla a página de código que é usada para armazenar os dados de caractere.
  
Se você tiver sites compatíveis com vários idiomas, considere usar tipos de dados Unicode **nchar** ou **nvarchar** para minimizar problemas de conversão de caracteres. Se você usar **char** ou **varchar**, recomendamos o seguinte:
- Use **char** quando os tamanhos das entradas de dados de coluna forem consistentes.  
- Use **varchar** quando os tamanhos das entradas de dados de coluna variarem consideravelmente.  
- Use **varchar(max)** quando os tamanhos das entradas de dados de coluna variarem consideravelmente e o tamanho puder exceder 8.000 bytes.  
  
Se SET ANSI_PADDING for OFF quando CREATE TABLE ou ALTER TABLE for executada, uma coluna **char** definida como NULL será tratada como **varchar**.
  
Quando a página de código de agrupamento usar caracteres de dois bytes, o tamanho do armazenamento ainda será *n* bytes. Dependendo da cadeia de caracteres, o tamanho de armazenamento de *n* bytes pode ser menor que *n* caracteres.

> [!WARNING]
> Cada coluna varchar(max) ou nvarchar(max) não nula requer 24 bytes de alocação fixa adicional que conta para o limite de linha de 8.060 bytes durante uma operação de classificação. Isso pode criar um limite implícito para o número de colunas varchar(max) ou nvarchar(max) não nulas que podem ser criadas em uma tabela.  
Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8060 bytes) ou no momento da inserção de dados. Esse tamanho de linha pode causar erros (por exemplo, o erro 512) durante algumas operações normais, como uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo, que os usuários não podem prever até que uma operação seja executada.
  
##  <a name="_character"></a> Convertendo dados de caractere  
Quando são convertidas expressões character a um tipo de dados character de um tamanho diferente, os valores muito longos para o novo tipo de dados são truncados. O tipo **uniqueidentifier** é considerado um tipo de caractere para fins de conversão de uma expressão de caractere e, portanto, está sujeito às regras de truncamento para conversão em um tipo de caractere. Consulte a seção de Exemplos a seguir.
  
Quando uma expressão character é convertida em uma expressão character de um tipo de dados ou tamanho diferente, como de **char(5)** em **varchar(5)** ou **char(20)** para **char(15)**, o agrupamento do valor de entrada é atribuído ao valor convertido. Se uma expressão noncharacter for convertida em um tipo de dados character, o agrupamento padrão do banco de dados atual será atribuído ao valor convertido. Em qualquer caso, você pode atribuir um agrupamento específico usando a cláusula [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9).
  
> [!NOTE]  
>  Há suporte para conversões de página de código em tipos de dados **char** e **varchar**, mas não no tipo de dados **text**. Como em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a perda de dados não é informada durante as conversões de página de código.  
  
As expressões character que estão sendo convertidas em um tipo de dados **numeric** aproximado podem incluir notação exponencial opcional (um e minúsculo ou um E maiúsculo seguido por um sinal de mais (+) ou menos (-) opcional e, depois, um número).
  
As expressões character que estão sendo convertidas a um tipo de dados **numeric** exato devem consistir em dígitos, um ponto decimal e um sinal opcional de mais (+) ou menos (-). Os espaços em branco à esquerda são ignorados. Na cadeia de caracteres não são permitidos separadores de vírgula, como o separador de milhar em 123,456.00.
  
As expressões character que estão sendo convertidas em tipo de dados **money** ou **smallmoney** também podem incluir um separador decimal opcional e o sinal monetário ($). São permitidos separadores de vírgula, como em $123,456.00.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. Mostrando o valor padrão de n quando usado em declaração variável.  
O exemplo a seguir mostra que o valor padrão de *n* é 1 para os tipos de dados `char` e `varchar` quando eles são usados em uma declaração de variável.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. Mostrando o valor padrão de n quando varchar é usado com CAST e CONVERT.  
O exemplo a seguir mostra que o valor padrão de *n* é 30 quando os tipos de dados `char` ou `varchar` são usados com as funções `CAST` e `CONVERT`.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. Convertendo dados para fins de exibição  
O exemplo a seguir converte duas colunas em tipos de caracteres e aplica um estilo que se aplica a um formato específico aos dados exibidos. Um tipo **money** é convertido em dados de caractere e o estilo 1 é aplicado, o que exibe os valores com vírgulas a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita do ponto decimal. Um tipo **datatime** é convertido em dados de caractere e o estilo 3 é aplicado, o que exibe os dados no formato dd/mm/aa. Na cláusula WHERE, um tipo **money** é convertido em um tipo de caractere para executar uma operação de comparação de cadeia de caracteres.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. Convertendo dados Uniqueidentifer  
O exemplo a seguir converte um valor `uniqueidentifier` em um tipo de dados `char`.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
O exemplo a seguir demonstra o truncamento de dados quando o valor é muito longo para o tipo de dados da conversão. Como o tipo **uniqueidentifier** é limitado a 36 caracteres, os caracteres que excedem esse comprimento ficam truncados.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
