---
title: Mapeamento dos dados do parâmetro CLR | Microsoft Docs
description: Este artigo lista os tipos de dados do Microsoft SQL Server, equivalentes no CLR para SQL Server e equivalentes CLR nativos no .NET Framework.
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
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488442"
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A tabela [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir lista os tipos de dados, seus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes no tempo de execução do idioma comum (CLR) para o **namespace System.Data.SqlTypes** e seus equivalentes CLR nativos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Quadro .NET.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nulo\<Int64>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Booleano booleano e booleano\<>**|  
|**char**|Nenhum|Nenhum|  
|**cursor**|Nenhum|Nenhum|  
|**date**|**Sqldatetime**|**DateTime, Nullable\<DateTime>**|  
|**datetime**|**Sqldatetime**|**DateTime, Nullable\<DateTime>**|  
|**datetime2**|Nenhum|**DateTime, Nullable\<DateTime>**|  
|**Datetimeoffset**|**Nenhum**|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|**decimal**|**Sqldecimal**|**Decimal, Nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Duplo, duplo\<duplo>duplo**|  
|**Geografia**|**SqlGeography**<br /><br /> **SqlGeography** é definido em Microsoft.SqlServer.Types.dll, que é instalado com o SQL Server e pode ser baixado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pacote de [recursos](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**Geometria**|**SqlGeometry**<br /><br /> **O SqlGeometry** é definido em Microsoft.SqlServer.Types.dll, que é instalado com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server e pode ser baixado no [pacote de recursos](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** é definido em Microsoft.SqlServer.Types.dll, que é instalado com o SQL Server e pode ser baixado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pacote de [recursos](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**imagem**|Nenhum|Nenhum|  
|**int**|**SqlInt32**|**Int32,>\<Nulaível Int32**|  
|**money**|**Sqlmoney**|**Decimal, Nullable\<Decimal>**|  
|**nchar**|**SqlChars**|**String, Char[]**|  
|**ntext**|Nenhum|Nenhum|  
|**numeric**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**nvarchar**|**SqlChars**<br /><br /> **SQLChars** é uma combinação melhor para transferência e acesso de dados, e **SQLString** é uma combinação melhor para realizar operações string.|**String, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars**|**Char, String, Char[],\<Nullable char>**|  
|**real**|**SqlSingle** (o intervalo de **SqlSingle,** no entanto, é maior que **o real)**|**Único,>\<único e anulado**|  
|**rowversion**|Nenhum|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16,>\<Nulo Int16**|  
|**smallmoney**|**Sqlmoney**|**Decimal, Nullable\<Decimal>**|  
|**sql_variant**|Nenhum|**Objeto**|  
|**table**|Nenhum|Nenhum|  
|**text**|Nenhum|Nenhum|  
|**time**|Nenhum|**TimeSpan,\<timespan anulado>**|  
|**timestamp**|Nenhum|Nenhum|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid,>\<De Guid Anulado**|  
|**Tipo definido pelo usuário (UDT)**|Nenhum|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[], Nullable\<byte>**|  
|**varchar**|Nenhum|Nenhum|  
|**xml**|**Sqlxml**|Nenhum|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações ao código de chamada ou programa marcando um parâmetro de entrada com o modificador **de saída** (Microsoft Visual C#) ou ** \<Out()> ByRef** (Microsoft Visual Basic) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Se o parâmetro de entrada for um tipo de dados CLR no **system.Data.SqlTypes** namespace, e o programa de chamada especificar seu tipo de dados equivalente como parâmetro de entrada, uma conversão de tipo ocorre automaticamente quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o procedimento armazenado clr a seguir tem um parâmetro de entrada do tipo de dados **SqlInt32** CLR que está marcado com **out** (C#) ou ** \<Out()> ByRef** (Visual Basic):  
  
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
  
 Depois que o conjunto é construído e criado no banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados, o procedimento armazenado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado com o seguinte Transact-SQL, que especifica um tipo de dados de **int** como um parâmetro OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando o procedimento armazenado clr é chamado, o tipo de dados **SqlInt32** é automaticamente convertido para um tipo de dados **int** e retornado ao programa de chamada.  
  
 Entretanto, nem todos os tipos de dados CLR podem ser automaticamente convertidos em seus tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes por um fora parâmetro out. A tabela a seguir lista estas exceções.  
  
|||  
|-|-|  
|**Tipo de dados CLR (SQL Server)**|**Tipo de dados do SQL Server**|  
|**Decimal**|SMALLMONEY|  
|**Sqlmoney**|SMALLMONEY|  
|**Decimal**|money|  
|**Datetime**|smalldatetime|  
|**Sqldatetime**|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionado **sqlGeography,** **SqlGeometry**e **sqlHierarchyId** tipos à tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
