---
description: Constantes (Transact-SQL)
title: Constantes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a715f64c0d6c1adf8ec3bc55b851848dfd1ae2e
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125009"
---
# <a name="constants-transact-sql"></a>Constantes (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Uma constante, também conhecida como uma literal ou um valor escalar, é um símbolo que representa um valor de dados específico. O formato de uma constante depende do tipo de dados do valor que representa.
  
## <a name="character-string-constants"></a>Constantes de cadeia de caracteres
As constantes de cadeias de caracteres são incluídas entre aspas simples e incluem caracteres alfanuméricos (a-z, A-Z e 0-9) e caracteres especiais, como ponto de exclamação (!), arroba (@) e sinal numérico (#). As constantes de cadeia de caracteres são atribuídas à ordenação padrão do banco de dados atual. Se a cláusula COLLATE for usada, a conversão para a página de código padrão do banco de dados ainda ocorrerá antes da conversão para a ordenação especificada pela cláusula COLLATE. As cadeias de caracteres digitadas por usuários são avaliadas pela página de código do computador e são convertidas na página de código padrão do banco de dados, se isso for necessário.

> [!NOTE]
> Quando uma [ordenação habilitada para UTF8](../../relational-databases/collations/collation-and-unicode-support.md#utf8) é especificada usando a cláusula COLLATE, a conversão para a página de código padrão do banco de dados ainda ocorre antes da conversão para a ordenação especificada pela cláusula COLLATE. A conversão não é feita diretamente para a ordenação habilitada para Unicode especificada. Para obter mais informações, consulte [Cadeia de caracteres Unicode](#unicode-strings).
  
Se a opção QUOTED_IDENTIFIER foi definida como OFF para uma conexão, as cadeias de caracteres também podem ser incluídas entre aspas duplas, mas o [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) e o [ODBC Driver for SQL Server](../../connect/odbc/download-odbc-driver-for-sql-server.md) usam automaticamente `SET QUOTED_IDENTIFIER ON`. Recomenda-se usar aspas simples.
  
Se uma cadeia de caracteres incluída entre aspas simples contiver uma aspa inserida, represente a aspa simples inserida com duas aspas simples. Isso não é necessário em cadeias de caracteres inseridas em aspas duplas.
  
Os seguintes são exemplos de cadeias de caracteres:
  
```
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
As cadeias de caracteres vazias são representadas como duas aspas simples sem nada entre elas. No modo de compatibilidade 6.x, uma cadeia de caracteres vazia é tratada como um único espaço.
  
As constantes de cadeia de caracteres oferecem suporte a [ordenações](../../relational-databases/collations/collation-and-unicode-support.md) avançadas.
  
> [!NOTE]  
> As constantes de caractere maiores que 8.000 bytes são tipadas como dados **varchar(max)**.  
  
## <a name="unicode-strings"></a>Cadeias de caracteres Unicode
As cadeias de caracteres Unicode têm um formato semelhante ao das cadeias de caracteres, mas são precedidas por um identificador N (N significa National Language no padrão SQL-92). 

> [!IMPORTANT]  
> O prefixo N deve ser maiúsculo. 

Por exemplo, `'Michél'` é uma constante de caractere enquanto `N'Michél'` é uma constante Unicode. As constantes Unicode são interpretadas como dados Unicode e não são avaliadas com o uso de uma página de código. As constantes Unicode têm uma ordenação. Esse ordenação controla principalmente comparações e diferenciação de maiúsculas e minúsculas. As constantes Unicode são atribuídas à ordenação padrão do banco de dados atual. Se a cláusula COLLATE for usada, a conversão para a ordenação padrão do banco de dados ainda ocorrerá antes da conversão para a ordenação especificada pela cláusula COLLATE. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).
  
As constantes da cadeira de caracteres Unicode oferecem suporte a ordenações avançados.
  
> [!NOTE]  
> As constantes Unicode maiores que 8.000 bytes são tipadas como dados **nvarchar(max)**.  
  
## <a name="binary-constants"></a>Constantes binárias
As constantes binárias têm o prefixo `0x` e são uma cadeia de números hexadecimais. Elas não são incluídas entre aspas.
  
Os seguintes são exemplos de cadeias binárias:
  
```
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  As constantes binárias maiores que 8.000 bytes são tipadas como dados **varbinary(max)**.  
  
## <a name="bit-constants"></a>Constantes bit
As constantes **bit** são representadas pelos números 0 ou 1 e não são incluídas entre aspas. Se um número maior que um for usado, ele será convertido em um.
  
## <a name="datetime-constants"></a>Constantes datetime
As constantes **datetime** são representadas usando valores de data de caractere em formatos específicos, incluídos entre aspas simples.
  
Estes são exemplos de constantes **datetime**:
  
```
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Exemplos de constantes datetime são:
  
```
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>constantes de número inteiro
As constantes **integer** são representadas por uma cadeia de números que não são incluídos entre aspas e que não contêm pontos decimais. As constantes **integer** devem ser números inteiros; elas não podem conter decimais.
  
Estes são exemplos de constantes **integer**:
  
```
1894  
2  
```  
  
## <a name="decimal-constants"></a>Constantes decimal
As constantes **decimal** são representadas por uma cadeia de números que não são incluídos entre aspas e que contêm um ponto decimal.
  
Estes são exemplos de constantes **decimal**:
  
```
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>Constantes float e real
As constantes **float** e **real** são representadas com notação científica.
  
Estes são exemplos de valores **float** ou **real**:
  
```
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>Constantes money
As constantes **money** são representadas como cadeias de números com um ponto decimal opcional e um símbolo da moeda opcional como prefixo. As constantes **money** não são incluídas entre aspas.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não impõe nenhum tipo de regra de agrupamento, tal como a inserção de uma vírgula (,) a cada três dígitos em cadeias que representam dinheiro.
  
> [!NOTE]  
>  As vírgulas são ignoradas em qualquer lugar no literal **money** especificado.  
  
Estes são exemplos de constantes **money**:
  
```
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>Constantes uniqueidentifier
As constantes **uniqueidentifier** são uma cadeia de caracteres que representa um GUID. Elas podem ser especificadas em um formato de caractere ou cadeia de binários.
  
Os exemplos a seguir especificam o mesmo GUID:
  
```
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Especificando números negativos e positivos  
Para indicar se um número é positivo ou negativo, aplique os operadores unários **+** ou **-** a uma constante numérica. Isso cria uma expressão numérica que representa o valor numérico com sinal. As constantes numéricas usam positivo quando os operadores unários **+** ou **-** não são aplicados.
  
Expressões de **integer** com sinal:  
  
```
+145345234
-2147483648
```
Expressões de **decimal** com sinal:  
  
```
+145345234.2234
-2147483648.10
```
  
Expressões **float** com sinal:  
  
```
+123E-3
-12E5
```
  
Expressões **money** com sinal:  
  
```
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Ordenações avançadas  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] dá suporte a constantes de cadeias de caractere e Unicode que aceitam ordenações avançadas. Para obter mais informações, consulte a cláusula [COLLATE &#40;Transact-SQL&#41;](../../t-sql/statements/collations.md).
  
## <a name="see-also"></a>Confira também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)
[Suporte para Unicode e ordenação](../../relational-databases/collations/collation-and-unicode-support.md)  
[Precedência de ordenação](../../t-sql/statements/collation-precedence-transact-sql.md)    
  
