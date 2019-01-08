---
title: Mapeando dados de parâmetro CLR | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9c4697d2dcbad80d1da0fd8ed6c81750ac90695b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534118"
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A seguinte tabela lista [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, seus equivalentes no common language runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no **SqlTypes** namespace e seus equivalentes CLR nativos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, que permite valor nulo\<Int64 >**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Booliano, que permite valor nulo\<booleano >**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**Data e hora, que permite valor nula\<DateTime >**|  
|**datetime**|**SqlDateTime**|**Data e hora, que permite valor nula\<DateTime >**|  
|**datetime2**|None|**Data e hora, que permite valor nula\<DateTime >**|  
|**DATETIMEOFFSET**|**Nenhum**|**DateTimeOffset, que permite valor nulo\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Double, que permite valor nulo\<Double >**|  
|**geografia**|**SqlGeography**<br /><br /> **SqlGeography** é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**geometria**|**SqlGeometry**<br /><br /> **SqlGeometry** é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32, que permite valor nulo\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** é uma melhor correspondência para transferência de dados e acesso, e **SQLString** é uma melhor correspondência para executar operações de cadeia de caracteres.|**String, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char [], que permite valor nulo\<char >**|  
|**real**|**SqlSingle** (o intervalo de **SqlSingle**, no entanto, é maior que **real**)|**Único, que permite valor nulo\<único >**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16, que permite valor nulo\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**sql_variant**|None|**Objeto**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan, que permite valor nulo\<TimeSpan >**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, que permite valor nulo\<Guid >**|  
|**Type(UDT) definida pelo usuário**|None|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[], Nullable\<byte>**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações para o código de chamada ou programa marcando um parâmetro de entrada com o **horizontalmente** modificador (Microsoft Visual c#) ou  **\<out () > ByRef** (Microsoft Visual Basic) Se o parâmetro de entrada é um tipo de dados CLR na **SqlTypes** namespace e o programa de chamada especifica seu equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipo de dados como o parâmetro de entrada, uma conversão de tipo ocorre automaticamente Quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o seguinte procedimento armazenado CLR tem um parâmetro de entrada **SqlInt32** tipo de dados CLR que é marcado com **out** (c#) ou  **\<out () > ByRef** ( Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 Depois que o assembly é compilado e criado no banco de dados, o procedimento armazenado é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o Transact-SQL a seguir, que especifica um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de **int** como um parâmetro de saída:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando o CLR armazenados procedimento é chamado, o **SqlInt32** tipo de dados é automaticamente convertido em um **int** tipo de dados e retornada ao programa de chamada.  
  
 Entretanto, nem todos os tipos de dados CLR podem ser automaticamente convertidos em seus tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes por um fora parâmetro out. A tabela a seguir lista estas exceções.  
  
|||  
|-|-|  
|**Tipo de dados CLR (SQL Server)**|**Tipo de dados do SQL Server**|  
|**decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionado **SqlGeography**, **SqlGeometry**, e **SqlHierarchyId** tipos à tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
