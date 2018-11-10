---
title: char e varchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
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
- utf8
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6bba11fe5be282ad804fc6dee03229312ec1d37
ms.sourcegitcommit: b58d514879f182fac74d9819918188f1688889f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50970908"
---
# <a name="char-and-varchar-transact-sql"></a>char e varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [Ajude a aprimorar os documentos do SQL Server!](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

Tipos de dados de caractere que sejam de comprimento fixo, **char** ou de comprimento variável, **varchar**. A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], quando uma ordenação habilitada por UTF-8 é usada, esses tipos de dados armazenam o intervalo completo de dados de caractere [Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) e usam a codificação de caracteres [UTF-8](http://www.wikipedia.org/wiki/UTF-8). Se uma ordenação não UTF-8 for especificada, esses tipos de dados armazenarão apenas um subconjunto de caracteres compatíveis com a página de código correspondente dessa ordenação.
  
## <a name="arguments"></a>Argumentos  
**char** [ ( *n* ) ] Dados de cadeia de caracteres de comprimento fixo. *n* define o tamanho da cadeia de caracteres em bytes e deve ser um valor entre 1 a 8.000. Para conjuntos de caracteres de codificação de byte único, como *Latino*, o tamanho de armazenamento é *n* bytes e a quantidade de caracteres que pode ser armazenada também é *n*. Para conjuntos de caracteres de codificação multibyte, o tamanho de armazenamento ainda será *n* bytes, mas a quantidade de caracteres que pode ser armazenada pode ser menor que *n*. O sinônimo ISO para **char** é **character**. Para saber mais sobre conjuntos de caracteres, consulte [Conjuntos de caracteres multibyte e de byte único](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets).

**varchar** [ ( *n* | **max** ) ] dados de cadeia de caracteres de comprimento variável. *n* define o tamanho da cadeia de caracteres em bytes e pode ser um valor entre 1 a 8.000. **max** indica que o tamanho de armazenamento máximo é 2^31-1 bytes (2 GB). Para conjuntos de caracteres de codificação de byte único, como *Latino*, o tamanho de armazenamento é *n* bytes + 2 bytes e a quantidade de caracteres que pode ser armazenada também é *n*. Para codificação de conjuntos de caracteres multibyte, o tamanho de armazenamento ainda será *n* bytes + 2 bytes, mas a quantidade de caracteres que pode ser armazenada pode ser menor que *n*. Os sinônimos ISO para **varchar** são **charvarying** ou **charactervarying**. Para saber mais sobre conjuntos de caracteres, consulte [Conjuntos de caracteres multibyte e de byte único](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets).

## <a name="remarks"></a>Remarks  
Quando *n* não é especificado em uma definição de dados ou instrução de declaração de variável, o tamanho padrão é 1. Quando *n* não é especificado ao usar as funções CAST e CONVERT, o tamanho padrão é 30.
  
Os objetos que usam **char** ou **varchar** são atribuídos à ordenação padrão do banco de dados, a menos que uma ordenação específica seja atribuída usando da cláusula COLLATE. A ordenação controla a página de código que é usada para armazenar os dados de caractere.

As codificações multibyte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluem:
-   Conjuntos de caracteres de byte duplo (DBCS) para alguns idiomas do Leste Asiático que usam páginas de código 936 e 950 (chinês), 932 (japonês) ou 949 (coreano).
-   UTF-8 com página de código 65001. **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir do[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]))

Se você tiver sites compatíveis com vários idiomas:
- A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], considere o uso de uma ordenação habilitada para UTF-8 para dar suporte a Unicode e minimizar os problemas de conversão de caracteres. 
- Caso use uma versão inferior do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], considere usar os tipos de dados **nchar** ou **nvarchar** Unicode para minimizar problemas de conversão de caracteres.   

Caso use **char** ou **varchar**, recomendamos que:
- Use **char** quando os tamanhos das entradas de dados de coluna forem consistentes.  
- Use **varchar** quando os tamanhos das entradas de dados de coluna variarem consideravelmente.  
- Use **varchar(max)** quando os tamanhos das entradas de dados de coluna variarem consideravelmente e o tamanho da cadeia de caracteres puder exceder 8.000 bytes.  
  
Se SET ANSI_PADDING for OFF quando CREATE TABLE ou ALTER TABLE for executada, uma coluna **char** definida como NULL será tratada como **varchar**.
  
> [!WARNING]
> Cada coluna varchar(max) ou nvarchar(max) não nula requer 24 bytes de alocação fixa adicional que conta para o limite de linha de 8.060 bytes durante uma operação de classificação. Isso pode criar um limite implícito para o número de colunas varchar(max) ou nvarchar(max) não nulas que podem ser criadas em uma tabela.  
Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8.060 bytes) ou no momento da inserção de dados. Esse tamanho de linha pode causar erros (por exemplo, o erro 512) durante algumas operações normais, como uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo, que os usuários não podem prever até que uma operação seja executada.
  
##  <a name="_character"></a> Convertendo dados de caractere  
Quando são convertidas expressões character a um tipo de dados character de um tamanho diferente, os valores muito longos para o novo tipo de dados são truncados. O tipo **uniqueidentifier** é considerado um tipo de caractere para fins de conversão de uma expressão de caractere e, portanto, está sujeito às regras de truncamento para conversão em um tipo de caractere. Consulte a seção de Exemplos a seguir.
  
Quando uma expressão character é convertida em uma expressão character de um tipo de dados ou tamanho diferente, como de **char(5)** em **varchar(5)** ou **char(20)** para **char(15)**, a ordenação do valor de entrada é atribuída ao valor convertido. Se uma expressão noncharacter for convertida em um tipo de dados character, a ordenação padrão do banco de dados atual será atribuída ao valor convertido. Em qualquer caso, você pode atribuir uma ordenação específica usando a cláusula [COLLATE](../../t-sql/statements/collations.md).
  
> [!NOTE]  
> Há suporte para conversões de página de código em tipos de dados **char** e **varchar**, mas não no tipo de dados **text**. Como em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a perda de dados não é informada durante as conversões de página de código.  
  
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
  
```
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
  
```
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](../../t-sql/statements/collations.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)     
[Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)    
[Conjuntos de caracteres multibyte e de byte único](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)
  
