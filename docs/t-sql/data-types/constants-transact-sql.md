---
title: Constantes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aae955a177f637e3c359eabf02679025cbecdb3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="constants-transact-sql"></a>Constantes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma constante, também conhecida como uma literal ou um valor escalar, é um símbolo que representa um valor de dados específico. O formato de uma constante depende do tipo de dados do valor que representa.
  
## <a name="character-string-constants"></a>Constantes de cadeia de caracteres
As constantes de cadeias de caracteres são incluídas entre aspas simples e incluem caracteres alfanuméricos (a-z, A-Z e 0-9) e caracteres especiais, como ponto de exclamação (!), arroba (@) e sinal numérico (#). Às constantes de cadeias de caracteres é atribuído o agrupamento padrão do banco de dados atual, a menos que a cláusula COLLATE seja usada para especificar um agrupamento. As cadeias de caracteres digitadas por usuários são avaliadas pela página de código do computador e são convertidas na página de código padrão do banco de dados, se isso for necessário.
  
Se a opção QUOTED_IDENTIFIER foi definida como OFF para uma conexão, as cadeias de caracteres também podem ser incluídas entre aspas duplas, mas o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provider e o driver ODBC usam automaticamente SET QUOTED_IDENTIFIER ON. Recomenda-se usar aspas simples.
  
Se uma cadeia de caracteres incluída entre aspas simples contiver uma aspa inserida, represente a aspa simples inserida com duas aspas simples. Isso não é necessário em cadeias de caracteres inseridas em aspas duplas.
  
Os seguintes são exemplos de cadeias de caracteres:
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
As cadeias de caracteres vazias são representadas como duas aspas simples sem nada entre elas. No modo de compatibilidade 6.x, uma cadeia de caracteres vazia é tratada como um único espaço.
  
As constantes de cadeia de caracteres oferecem suporte a agrupamentos avançados.
  
> [!NOTE]  
>  As constantes de caractere maiores que 8.000 bytes são tipadas como dados **varchar(max)**.  
  
## <a name="unicode-strings"></a>Cadeias de caracteres Unicode
As cadeias de caracteres Unicode têm um formato semelhante ao das cadeias de caracteres, mas são precedidas por um identificador N (N significa National Language no padrão SQL-92). O prefixo N deve ser maiúsculo. Por exemplo, 'Michél' é uma constante de caracteres, enquanto N'Michél' é uma constante Unicode. As constantes Unicode são interpretadas como dados Unicode e não são avaliadas com o uso de uma página de código. As constantes Unicode têm um agrupamento. Esse agrupamento controla principalmente comparações e diferenciação de maiúsculas e minúsculas. Às constantes Unicode é atribuído o agrupamento padrão do banco de dados atual, a menos que a cláusula COLLATE seja usada para especificar um agrupamento. Os dados Unicode são armazenados usando 2 bytes por caractere, em vez de 1 byte por caractere para dados de caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
As constantes da cadeira de caracteres Unicode oferecem suporte a agrupamentos avançados.
  
> [!NOTE]  
>  As constantes Unicode maiores que 8.000 bytes são tipadas como dados **nvarchar(max)**.  
  
## <a name="binary-constants"></a>Constantes binárias
As constantes binárias têm o prefixo `0x` e são uma cadeia de números hexadecimais. Elas não são incluídas entre aspas.
  
Os seguintes são exemplos de cadeias binárias:
  
```sql
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
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Exemplos de constantes datetime são:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>constantes de número inteiro
As constantes **integer** são representadas por uma cadeia de números que não são incluídos entre aspas e que não contêm pontos decimais. As constantes **integer** devem ser números inteiros; elas não podem conter decimais.
  
Estes são exemplos de constantes **integer**:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>Constantes decimal
As constantes **decimal** são representadas por uma cadeia de números que não são incluídos entre aspas e que contêm um ponto decimal.
  
Estes são exemplos de constantes **decimal**:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>Constantes float e real
As constantes **float** e **real** são representadas com notação científica.
  
Estes são exemplos de valores **float** ou **real**:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>Constantes money
As constantes **money** são representadas como cadeias de números com um ponto decimal opcional e um símbolo da moeda opcional como prefixo. As constantes **money** não são incluídas entre aspas.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não impõe nenhum tipo de regra de agrupamento, tal como a inserção de uma vírgula (,) a cada três dígitos em cadeias que representam dinheiro.
  
> [!NOTE]  
>  As vírgulas são ignoradas em qualquer lugar no literal **money** especificado.  
  
Estes são exemplos de constantes **money**:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>Constantes uniqueidentifier
As constantes **uniqueidentifier** são uma cadeia de caracteres que representa um GUID. Elas podem ser especificadas em um formato de caractere ou cadeia de binários.
  
Os exemplos a seguir especificam o mesmo GUID:
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Especificando números negativos e positivos  
Para indicar se um número é positivo ou negativo, aplique os operadores unários **+** ou **-** a uma constante numérica. Isso cria uma expressão numérica que representa o valor numérico com sinal. As constantes numéricas usam positivo quando os operadores unários **+** ou **-** não são aplicados.
  
Expressões de **integer** com sinal:  
  
```sql
+145345234
-2147483648
```
Expressões de **decimal** com sinal:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Expressões **float** com sinal:  
  
```sql
+123E-3
-12E5
```
  
Expressões **money** com sinal:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Agrupamentos avançados  
O SQL Server oferece suporte a constantes de cadeias de caractere e Unicode que aceitam agrupamentos avançados. Para obter mais informações, consulte a cláusula [COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9).
  
## <a name="see-also"></a>Consulte também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  
