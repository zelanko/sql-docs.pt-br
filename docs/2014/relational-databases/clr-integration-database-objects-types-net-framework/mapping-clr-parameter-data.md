---
title: Mapeando dados de parâmetro CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
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
caps.latest.revision: 69
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 34d30e57908e8cd44eefa43d6f2d030ae0d102f7
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354518"
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
  A seguinte tabela lista [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, seus equivalentes no common language runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no `System.Data.SqlTypes` namespace e seus equivalentes CLR nativos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] do .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64, que permite valor nulo\<Int64 >**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**Booliano, que permite valor nulo\<booleano >**|  
|`char`|Nenhum|Nenhum|  
|`cursor`|Nenhum|Nenhum|  
|`date`|`SqlDateTime`|**Data e hora, que permite valor nula\<DateTime >**|  
|`datetime`|`SqlDateTime`|**Data e hora, que permite valor nula\<DateTime >**|  
|`datetime2`|Nenhum|**Data e hora, que permite valor nula\<DateTime >**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, que permite valor nulo\<DateTimeOffset >**|  
|`decimal`|`SqlDecimal`|**Decimal, Nullable\<Decimal>**|  
|`float`|`SqlDouble`|**Double, que permite valor nulo\<Double >**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography` é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](http://go.microsoft.com/fwlink/?LinkId=131220).|Nenhum|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry` é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](http://go.microsoft.com/fwlink/?LinkId=131220).|Nenhum|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId` é definido em Types, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](http://go.microsoft.com/fwlink/?LinkId=131220).|Nenhum|  
|`image`|Nenhum|Nenhum|  
|`int`|`SqlInt32`|**Int32, que permite valor nulo\<Int32 >**|  
|`money`|`SqlMoney`|**Decimal, Nullable\<Decimal>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|Nenhum|Nenhum|  
|`numeric`|`SqlDecimal`|**Decimal, Nullable\<Decimal>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars` é uma melhor correspondência para transferência e acesso a dados, e `SQLString` é uma melhor correspondência para executar operações de cadeia de caracteres.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, String, Char [], que permite valor nulo\<char >**|  
|`real`|`SqlSingle` (o intervalo de `SqlSingle`, no entanto, é maior que `real`)|**Único, que permite valor nulo\<único >**|  
|`rowversion`|Nenhum|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, que permite valor nulo\<Int16 >**|  
|`smallmoney`|`SqlMoney`|**Decimal, Nullable\<Decimal>**|  
|`sql_variant`|Nenhum|`Object`|  
|`table`|Nenhum|Nenhum|  
|`text`|Nenhum|Nenhum|  
|`time`|Nenhum|**TimeSpan, que permite valor nulo\<TimeSpan >**|  
|`timestamp`|Nenhum|Nenhum|  
|`tinyint`|`SqlByte`|**Byte, Nullable\<Byte>**|  
|`uniqueidentifier`|`SqlGuid`|**GUID, que permite valor nulo\<Guid >**|  
|`User-defined type(UDT)`|Nenhum|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte, Byte[], Nullable\<byte>**|  
|`varchar`|Nenhum|Nenhum|  
|`xml`|`SqlXml`|Nenhum|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações para o código de chamada ou programa marcando um parâmetro input com o modificador `out` (Microsoft Visual C#) ou `<Out()> ByRef` (Microsoft Visual Basic). Se o parâmetro input for um tipo de dados CLR no namespace `System.Data.SqlTypes`, e o programa de chamada especificar seu tipo de dados equivalente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o parâmetro input, uma conversão de tipo ocorrerá automaticamente quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o seguinte procedimento armazenado CLR tem um parâmetro input do tipo de dados CLR `SqlInt32` que é marcado com `out` (C#) ou `<Out()> ByRef` (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 Depois que o assembly é criado no banco de dados, o procedimento armazenado é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a seguinte Transact-SQL, que especifica um tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de `int` como um parâmetro OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando o procedimento armazenado CLR é chamado, o tipo de dados `SqlInt32` é automaticamente convertido em um tipo de dados `int` e retornado para o programa de chamada.  
  
 Entretanto, nem todos os tipos de dados CLR podem ser automaticamente convertidos em seus tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes por um fora parâmetro out. A tabela a seguir lista estas exceções.  
  
|||  
|-|-|  
|**Tipo de dados CLR (SQL Server)**|**Tipo de dados do SQL Server**|  
|`Decimal`|SMALLMONEY|  
|`SqlMoney`|SMALLMONEY|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionados os tipos `SqlGeography`, `SqlGeometry` e `SqlHierarchyId` à tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
