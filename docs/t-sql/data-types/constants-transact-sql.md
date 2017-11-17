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
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b212354492b96ca69ebf29afbc39c8ed1de6e3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
>  Constantes de caracteres maiores que 8000 bytes recebem o tipo **varchar (max)** dados.  
  
## <a name="unicode-strings"></a>Cadeias de caracteres Unicode
As cadeias de caracteres Unicode têm um formato semelhante ao das cadeias de caracteres, mas são precedidas por um identificador N (N significa National Language no padrão SQL-92). O prefixo N deve ser maiúsculo. Por exemplo, 'Michél' é uma constante de caracteres, enquanto N'Michél' é uma constante Unicode. As constantes Unicode são interpretadas como dados Unicode e não são avaliadas com o uso de uma página de código. As constantes Unicode têm um agrupamento. Esse agrupamento controla principalmente comparações e diferenciação de maiúsculas e minúsculas. Às constantes Unicode é atribuído o agrupamento padrão do banco de dados atual, a menos que a cláusula COLLATE seja usada para especificar um agrupamento. Os dados Unicode são armazenados usando 2 bytes por caractere, em vez de 1 byte por caractere para dados de caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
As constantes da cadeira de caracteres Unicode oferecem suporte a agrupamentos avançados.
  
> [!NOTE]  
>  Constantes Unicode maiores que 8000 bytes recebem o tipo **nvarchar (max)** dados.  
  
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
>  Constantes binárias maiores que 8000 bytes recebem o tipo **varbinary (max)** dados.  
  
## <a name="bit-constants"></a>constantes de bit
**bit** constantes são representadas pelos números 0 ou 1 e não são colocadas entre aspas. Se um número maior que um for usado, ele será convertido em um.
  
## <a name="datetime-constants"></a>constantes de data e hora
**DateTime** constantes são representadas usando valores de data de caractere em formatos específicos, incluídos entre aspas.
  
Os seguintes são exemplos de **datetime** constantes:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Exemplos de constantes de data e hora são:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>constantes de número inteiro
**inteiro** constantes são representadas por uma cadeia de números que não são incluídos entre aspas e não contêm pontos decimais. **inteiro** constantes devem ser números inteiros; elas não podem conter decimais.
  
Os seguintes são exemplos de **inteiro** constantes:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>constantes decimais
**decimal** constantes são representadas por uma cadeia de números que não estão entre aspas e contêm um ponto decimal.
  
Os seguintes são exemplos de **decimal** constantes:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>constantes de float e real
**float** e **real** constantes são representadas usando notação científica.
  
Os seguintes são exemplos de **float** ou **real** valores:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>constantes de dinheiro
**Money** constantes são representadas como cadeia de caracteres de números com um ponto decimal opcional e um símbolo monetário opcional como prefixo. **Money** constantes não são colocados entre aspas.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não impõe nenhum tipo de regra de agrupamento, tal como a inserção de uma vírgula (,) a cada três dígitos em cadeias que representam dinheiro.
  
> [!NOTE]  
>  Vírgulas são ignoradas em qualquer lugar do **money** literal.  
  
Os seguintes são exemplos de **money** constantes:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>constantes uniqueidentifier
**uniqueidentifier** constantes são uma cadeia de caracteres que representa um GUID. Elas podem ser especificadas em um formato de caractere ou cadeia de binários.
  
Os exemplos a seguir especificam o mesmo GUID:
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Especificando números negativos e positivos  
Para indicar se um número é positivo ou negativo, aplique o  **+**  ou  **-**  operadores unários para uma constante numérica. Isso cria uma expressão numérica que representa o valor numérico com sinal. Constantes numéricas usam positivo quando o  **+**  ou  **-**  operadores unários não são aplicados.
  
Assinado **inteiro** expressões:  
  
```sql
+145345234
-2147483648
```
Assinado **decimal** expressões:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Assinado **float** expressões:  
  
```sql
+123E-3
-12E5
```
  
Assinado **money** expressões:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Agrupamentos avançados  
O SQL Server oferece suporte a constantes de cadeias de caractere e Unicode que aceitam agrupamentos avançados. Para obter mais informações, consulte o [COLLATE &#40; Transact-SQL &#41; ](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) cláusula.
  
## <a name="see-also"></a>Consulte também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  

