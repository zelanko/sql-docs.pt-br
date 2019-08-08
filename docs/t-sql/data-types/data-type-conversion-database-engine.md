---
title: Conversão de tipo de dados (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a9ef3df75a54b6565b1d71c0a9e4557f752f95b
ms.sourcegitcommit: 182ed49fa5a463147273b58ab99dc228413975b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68697500"
---
# <a name="data-type-conversion-database-engine"></a>Conversão de tipo de dados (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Os tipos de dados podem ser convertidos nos seguintes cenários:
-   Quando os dados de um objeto são movidos, comparados ou combinados com dados de outro objeto, eles podem ser convertidos de um tipo de dados de um objeto em um tipo de dados de outro objeto.  
-   Quando os dados de uma coluna de resultado, um código de retorno ou um parâmetro de saída [!INCLUDE[tsql](../../includes/tsql-md.md)] são movidos para uma variável de programa, os dados devem ser convertidos de tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipo de dados da variável.  
  
Ao fazer a conversão entre uma variável de aplicativo e uma coluna de conjunto de resultados, um código de retorno, um parâmetro ou um marcador de parâmetro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as conversões de tipo de dados com suporte são definidas pela API do banco de dados.
  
## <a name="implicit-and-explicit-conversion"></a>Conversões implícita e explícita
Os tipos de dados podem ser convertidos implícita ou explicitamente.
  
As conversões implícitas não são visíveis ao usuário. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte automaticamente os dados de um tipo de dados em outro. Por exemplo, quando **smallint** é comparado com **int**, **smallint** é convertido implicitamente em **int** antes que a comparação continue.
  
**GETDATE()** é implicitamente convertido no estilo de data 0. **SYSDATETIME()** é implicitamente convertido em estilo de data 21.
  
As conversões explícitas usam as funções CAST ou CONVERT.
  
As funções [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) convertem um valor (uma variável local, uma coluna ou outra expressão) de um tipo de dados em outro. Por exemplo, a seguinte função `CAST` converte o valor numérico de `$157.27` em uma cadeia de caracteres de `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Use CAST em vez de CONVERT se quiser que o código do programa [!INCLUDE[tsql](../../includes/tsql-md.md)] esteja de acordo com ISO. Use CONVERT em vez de CAST para se beneficiar da funcionalidade de estilo de CONVERT.
  
A ilustração a seguir mostra todas as conversões de tipos de dados explícitas e implícitas que são permitidas para tipos de dados fornecidos pelo sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso inclui **xml**, **bigint** e **sql_variant**. Não há nenhuma conversão implícita na atribuição do tipo de dados **sql_variant**, mas há uma conversão implícita em **sql_variant**.
  
![Tabela de conversão de tipo de dados](../../t-sql/data-types/media/lrdatahd.png "Data type conversion table")

Embora o gráfico acima ilustre todas as conversões explícitas e implícitas permitidas no SQL Server, ele não indica o tipo de dados resultante da conversão. Quando o SQL Server executa uma conversão explícita, a instrução em si determina o tipo de dados resultante. Para conversões implícitas, instruções de atribuição como definir o valor de uma variável ou inserir um valor em uma coluna resultam no tipo de dados que foi definido pela declaração de variável ou definição de coluna. Para operadores de comparação ou outras expressões, o tipo de dados resultante depende das regras de precedência de tipo de dados.

Por exemplo, o script a seguir define uma variável do tipo `varchar`, atribui um valor do tipo `int` à variável e, em seguida, seleciona uma concatenação da variável com uma cadeia de caracteres.

```sql
DECLARE @string varchar(10);
SET @string = 1;
SELECT @string + ' is a string.'
```

O valor `int` de `1` é convertido em um `varchar`, portanto, a instrução `SELECT` retorna o valor `1 is a string.`.

O exemplo a seguir mostra um script semelhante com uma variável `int`:

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + ' is not a string.'
```

Nesse caso, a instrução `SELECT` gera o seguinte erro:

`Msg 245, Level 16, State 1, Line 3`
`Conversion failed when converting the varchar value ' is not a string.' to data type int.`

Para avaliar a expressão `@notastring + ' is not a string.'`, o SQL Server segue as regras de precedência de tipo de dados para concluir a conversão implícita antes que o resultado da expressão possa ser calculado. Como `int` tem uma precedência mais alta do que `varchar`, o SQL Server tenta converter a cadeia de caracteres em um inteiro e falha porque essa cadeia de caracteres não pode ser convertida em um inteiro. Se a expressão fornecer uma cadeia de caracteres que pode ser convertida, a instrução terá sucesso, como no exemplo a seguir:

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + '1'
```

Nesse caso, a cadeia de caracteres `1` pode ser convertida para o valor inteiro `1`, de modo que essa instrução `SELECT` retorna o valor `2`. Observe que o operador `+` se torna uma adição em vez de uma concatenação quando os tipos de dados fornecidos são inteiros.

## <a name="data-type-conversion-behaviors"></a>Comportamentos de conversão de tipo de dados

Algumas conversões de tipo de dados implícitas e explícitas não têm suporte quando você está convertendo o tipo de dados de um objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro. Por exemplo, um valor **nchar** não pode ser convertido em um valor **image**. Um valor **nchar** só pode ser convertido em **binary** usando uma conversão explícita; uma conversão implícita em **binary** não tem suporte. No entanto, um **nchar** pode ser explícita ou implicitamente convertido em **nvarchar**.
  
Os tópicos a seguir descrevem os comportamentos de conversão exibidos pelos tipos de dados correspondentes:
  
 - [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money e smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Convertendo tipos de dados usando procedimentos armazenados de automação OLE  
Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] e a Automação OLE usa tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], os procedimentos armazenados de Automação OLE devem converter os dados que passam entre eles.
  
A tabela a seguir descreve as conversões de tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo de dados do SQL Server|Tipo de dados do Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Booliano**|  
|**binary**, **varbinary**, **image**|Matriz **Byte()** unidimensional|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**, **smallmoney**|**Moeda**|  
|**datetime**, **smalldatetime**|**Data**|  
|Tudo definido como NULL|**Variant** definida como Null|  
  
Todos os valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] únicos são convertidos em um valor [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] único, com a exceção dos valores **binary**, **varbinary** e **image**. Esses valores são convertidos em uma matriz **Byte()** unidimensional em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Essa matriz tem um intervalo de **Byte(** 0 to _length_ 1 **)** em que *length* é o número de bytes nos valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary**, **varbinary** ou **image**.
  
Estas são as conversões de tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo de dados do Visual Basic|Tipo de dados do SQL Server|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Moeda**|**money**|  
|**Data**|**datetime**|  
|**String** com 4.000 caracteres ou menos|**varchar**/**nvarchar**|  
|**String** com mais de 4.000 caracteres|**text**/**ntext**|  
|Matriz **Byte()** unidimensional com 8.000 bytes ou menos|**varbinary**|  
|Matriz **Byte()** unidimensional com mais de 8.000 bytes|**imagem**|  
  
## <a name="see-also"></a>Confira também
[Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
