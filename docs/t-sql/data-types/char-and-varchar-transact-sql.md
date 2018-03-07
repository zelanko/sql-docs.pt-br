---
title: char e varchar (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c383e3b3ff5b79604454f80443c9042633797bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="char-and-varchar-transact-sql"></a>char e varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esses tipos de dados são de comprimento fixo ou comprimento variável.  
  
## <a name="arguments"></a>Argumentos  
**char** [(  *n*  )] comprimento fixo, dados de cadeia de caracteres não Unicode. *n*Define o comprimento da cadeia de caracteres e deve ser um valor de 1 a 8.000. O tamanho de armazenamento é  *n*  bytes. O sinônimo ISO para **char** é **caracteres**.
  
**varchar** [(  *n*   |  **max** )] comprimento variável, dados de cadeia de caracteres não Unicode. *n*Define o comprimento da cadeia de caracteres e pode ser um valor de 1 a 8.000. **Max** indica que o tamanho máximo de armazenamento é 2 ^ 31-1 bytes (2 GB). O tamanho de armazenamento é o comprimento real dos dados inseridos + 2 bytes. Os sinônimos ISO para **varchar** são **charvarying** ou **charactervarying**.
  
## <a name="remarks"></a>Comentários  
Quando  *n*  não for especificado em uma definição de dados ou uma instrução de declaração de variável, o comprimento padrão é 1. Quando  *n*  não for especificado ao usar as funções CAST e CONVERT, o comprimento padrão é 30.
  
Objetos que usam **char** ou **varchar** recebem o agrupamento padrão do banco de dados, a menos que um agrupamento específico é atribuído usando a cláusula COLLATE. O agrupamento controla a página de código que é usada para armazenar os dados de caractere.
  
Se você tiver sites que dão suporte a vários idiomas, considere usar o Unicode **nchar** ou **nvarchar** tipos de dados para minimizar problemas de conversão de caracteres. Se você usar **char** ou **varchar**, recomendamos o seguinte:
- Use **char** quando os tamanhos das entradas de dados de coluna são consistentes.  
- Use **varchar** quando os tamanhos das entradas de dados de coluna variarem consideravelmente.  
- Use **varchar (max)** quando os tamanhos das entradas de dados de coluna variarem consideravelmente e o tamanho puder exceder 8.000 bytes.  
  
Se SET ANSI_PADDING é OFF quando CREATE TABLE ou ALTER TABLE é executada, uma **char** coluna definida como NULL é tratado como **varchar**.
  
Quando a página de código do agrupamento usa caracteres de byte duplo, o tamanho de armazenamento ainda será  *n*  bytes. Dependendo da cadeia de caracteres, o tamanho do armazenamento de  *n*  bytes pode ser menor que  *n*  caracteres.

> [!WARNING]
> Cada nulos varchar (max) ou uma coluna nvarchar (max) requer 24 bytes de alocação fixa adicional que conta em relação ao limite de linha de 8.060 bytes durante uma operação de classificação. Isso pode criar um limite implícito para o número de colunas de nvarchar (max) que podem ser criadas em uma tabela ou não nulos varchar (max).  
Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8060 bytes) ou no momento da inserção de dados. Esse tamanho de linha pode causar erros (por exemplo, o erro 512) durante algumas operações normais, como uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo, que os usuários não podem prever até que uma operação seja executada.
  
##  <a name="_character"></a>Converter dados de caracteres  
Quando são convertidas expressões character a um tipo de dados character de um tamanho diferente, os valores muito longos para o novo tipo de dados são truncados. O **uniqueidentifier** tipo é considerado um tipo de caractere para fins de conversão de uma expressão de caractere e, portanto, está sujeito às regras de truncamento para conversão em um tipo de caractere. Consulte a seção de Exemplos a seguir.
  
Quando uma expressão de caractere é convertida em uma expressão de caractere de um tipo de dados diferente ou o tamanho, como de **char (5)** para **varchar(5)**, ou **char(20)** para **char(15)**, o agrupamento do valor de entrada é atribuído ao valor convertido. Se uma expressão noncharacter for convertida em um tipo de dados character, o agrupamento padrão do banco de dados atual será atribuído ao valor convertido. Em ambos os casos, você pode atribuir um agrupamento específico usando o [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) cláusula.
  
> [!NOTE]  
>  Conversões de página de código têm suporte para **char** e **varchar** tipos de dados, mas não para **texto** tipo de dados. Como em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a perda de dados não é informada durante as conversões de página de código.  
  
Expressões Character que estão sendo convertidas a um aproximado **numérico** tipo de dados pode incluir notação exponencial opcional (um e minúsculo ou um E maiusculo seguido por um sinal de adição opcional (+) ou menos (-) e, depois, um número).
  
Expressões Character que estão sendo convertidas a um exata **numérico** tipo de dados deve consistir em dígitos, um ponto decimal e um sinal de adição (+) ou menos (-). Os espaços em branco à esquerda são ignorados. Na cadeia de caracteres não são permitidos separadores de vírgula, como o separador de milhar em 123,456.00.
  
Expressões Character convertidas para **money** ou **smallmoney** tipos de dados também podem incluir um ponto decimal opcional e um sinal de cifrão ($). São permitidos separadores de vírgula, como em $123,456.00.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. Mostrando o valor padrão de n quando usado em declaração variável.  
O exemplo a seguir mostra o valor padrão de  *n*  é 1 para o `char` e `varchar` tipos de dados quando eles são usados na declaração de variável.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. Mostrando o valor padrão de n quando varchar é usado com CAST e CONVERT.  
O exemplo a seguir mostra que o valor padrão de  *n*  é 30 quando o `char` ou `varchar` tipos de dados são usados com o `CAST` e `CONVERT` funções.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. Convertendo dados para fins de exibição  
O exemplo a seguir converte duas colunas em tipos de caracteres e aplica um estilo que se aplica a um formato específico aos dados exibidos. Um **money** tipo é convertido em dados de caractere e estilo 1 é aplicado, que exibe os valores com vírgulas a cada três dígitos à esquerda do ponto decimal e dois dígitos à direita da vírgula decimal. Um **datetime** tipo é convertido em dados de caractere e estilo 3 é aplicado, que exibe os dados no formato dd/mm/aa. Na cláusula WHERE, uma **money** tipo é convertido em um tipo de caractere para executar uma operação de comparação de cadeia de caracteres.
  
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
  
O exemplo a seguir demonstra o truncamento de dados quando o valor é muito longo para o tipo de dados da conversão. Porque o **uniqueidentifier** tipo é limitado a 36 caracteres, os caracteres que excedem esse comprimento ficam truncados.
  
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
  
## <a name="see-also"></a>Consulte também
[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
