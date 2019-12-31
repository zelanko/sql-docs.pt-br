---
title: Mapeando dados de parâmetro CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 17eeefbe125722c666f9f56394028da8c66a66b3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232276"
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
  A tabela a seguir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lista os tipos de dados, seus equivalentes no Common Language Runtime (CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) para `System.Data.SqlTypes` no namespace e seus equivalentes CLR nativos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64,>\<Int64 anulável**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**Booliano,\<booleano anulável>**|  
|`char`|Não|Não|  
|`cursor`|Não|Não|  
|`date`|`SqlDateTime`|**DateTime, data\<e hora anuláveis>**|  
|`datetime`|`SqlDateTime`|**DateTime, data\<e hora anuláveis>**|  
|`datetime2`|Não|**DateTime, data\<e hora anuláveis>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, DateTimeOffset\<anulável>**|  
|`decimal`|`SqlDecimal`|**Decimal, decimal\<anulável>**|  
|`float`|`SqlDouble`|**Duplo,>\<duplo anulável**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography`é definido em Microsoft. SqlServer. Types. dll, que é instalado com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]SQL Server e pode ser baixado do [Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164).|Não|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry`é definido em Microsoft. SqlServer. Types. dll, que é instalado com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]SQL Server e pode ser baixado do [Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164).|Não|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId`é definido em Microsoft. SqlServer. Types. dll, que é instalado com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]SQL Server e pode ser baixado do [Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164).|Não|  
|`image`|Não|Não|  
|`int`|`SqlInt32`|**Int32,>\<Int32 anulável**|  
|`money`|`SqlMoney`|**Decimal, decimal\<anulável>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|Não|Não|  
|`numeric`|`SqlDecimal`|**Decimal, decimal\<anulável>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> 
  `SQLChars` é uma melhor correspondência para transferência e acesso a dados, e `SQLString` é uma melhor correspondência para executar operações de cadeia de caracteres.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, String, Char [], Char\<anulável>**|  
|`real`|
  `SqlSingle` (o intervalo de `SqlSingle`, no entanto, é maior que `real`)|**Único>Anulável\<**|  
|`rowversion`|Não|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, Int16\<anulável>**|  
|`smallmoney`|`SqlMoney`|**Decimal, decimal\<anulável>**|  
|`sql_variant`|Não|`Object`|  
|`table`|Não|Não|  
|`text`|Não|Não|  
|`time`|Não|**TimeSpan, TimeSpan\<anulável>**|  
|`timestamp`|Não|Não|  
|`tinyint`|`SqlByte`|**Byte,>\<de bytes anuláveis**|  
|`uniqueidentifier`|`SqlGuid`|**GUID, GUID\<anulável>**|  
|`User-defined type(UDT)`|Não|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte, Byte [],>\<de bytes anuláveis**|  
|`varchar`|Não|Não|  
|`xml`|`SqlXml`|Não|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações para o código de chamada ou programa marcando um parâmetro input com o modificador `out` (Microsoft Visual C#) ou `<Out()> ByRef` (Microsoft Visual Basic). Se o parâmetro input for um tipo de dados CLR no namespace `System.Data.SqlTypes`, e o programa de chamada especificar seu tipo de dados equivalente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o parâmetro input, uma conversão de tipo ocorrerá automaticamente quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o seguinte procedimento armazenado CLR tem um parâmetro input do tipo de dados CLR `SqlInt32` que é marcado com `out` (C#) ou `<Out()> ByRef` (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
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
|`Decimal`|smallmoney|  
|`SqlMoney`|smallmoney|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionados os tipos `SqlGeography`, `SqlGeometry` e `SqlHierarchyId` à tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
