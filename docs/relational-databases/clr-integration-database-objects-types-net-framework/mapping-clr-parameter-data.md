---
title: Mapeando dados de parâmetro CLR | Microsoft Docs
description: Este artigo lista Microsoft SQL Server tipos de dados, equivalentes no CLR para SQL Server e equivalentes CLR nativos no .NET Framework.
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488442"
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A tabela a seguir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lista os tipos de dados, seus equivalentes no Common Language Runtime (CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) para no namespace **System. Data. SqlTypes** e seus equivalentes nativos CLR no [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64,>\<Int64 anulável**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**Booliano,\<booleano anulável>**|  
|**char**|Nenhum|Nenhum|  
|**cursor**|Nenhum|Nenhum|  
|**date**|**SqlDateTime**|**DateTime, data\<e hora anuláveis>**|  
|**datetime**|**SqlDateTime**|**DateTime, data\<e hora anuláveis>**|  
|**datetime2**|Nenhum|**DateTime, data\<e hora anuláveis>**|  
|**DATETIMEOFFSET**|**Nenhum**|**DateTimeOffset, DateTimeOffset\<anulável>**|  
|**decimal**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Duplo,>\<duplo anulável**|  
|**geografia**|**SqlGeography**<br /><br /> **Geography** é definido em Microsoft. SqlServer. Types. dll, que é instalado com SQL Server e pode ser baixado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**geometria**|**SqlGeometry**<br /><br /> **SqlGeometry** é definido em Microsoft. SqlServer. Types. dll, que é instalado com SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** é definido em Microsoft. SqlServer. Types. dll, que é instalado com SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhum|  
|**imagem**|Nenhum|Nenhum|  
|**int**|**SqlInt32**|**Int32,>\<Int32 anulável**|  
|**money**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**nchar**|**SqlChars, SqlString**|**Cadeia de caracteres, Char []**|  
|**ntext**|Nenhum|Nenhum|  
|**numeric**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SqlChars** é uma correspondência melhor para transferência e acesso de dados, e **SqlString** é uma correspondência melhor para executar operações de cadeia de caracteres.|**Cadeia de caracteres, Char []**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char [], Char\<anulável>**|  
|**real**|**SqlSingle** (o intervalo de **SqlSingle**, no entanto, é maior do que o **real**)|**Único>Anulável\<**|  
|**rowversion**|Nenhum|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16, Int16\<anulável>**|  
|**smallmoney**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**sql_variant**|Nenhum|**Objeto**|  
|**table**|Nenhum|Nenhum|  
|**text**|Nenhum|Nenhum|  
|**time**|Nenhum|**TimeSpan, TimeSpan\<anulável>**|  
|**timestamp**|Nenhum|Nenhum|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, GUID\<anulável>**|  
|**Tipo definido pelo usuário (UDT)**|Nenhum|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[], Nullable\<byte>**|  
|**varchar**|Nenhum|Nenhum|  
|**xml**|**SqlXml**|Nenhum|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações para o código ou programa de chamada, marcando um parâmetro de entrada com o modificador **out** (Microsoft Visual C#) ou ** \<out () > ByRef** (Microsoft Visual Basic) se o parâmetro de entrada for um tipo de dados CLR no **sistema. o namespace Data. SqlTypes** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa de chamada especifica seu tipo de dados equivalente como o parâmetro de entrada, uma conversão de tipo ocorre automaticamente quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o procedimento armazenado CLR a seguir tem um parâmetro de entrada de tipo de dados CLR **SqlInt32** que é marcado com **out** (C#) ou ** \<out () > ByRef** (Visual Basic):  
  
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
  
 Depois que o assembly é compilado e criado no banco de dados, o procedimento armazenado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado com o TRANSACT-SQL a seguir, que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica um tipo de dados **int** como um parâmetro de saída:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando o procedimento CLR armazenado é chamado, o tipo de dados **SqlInt32** é convertido automaticamente em um tipo de dados **int** e retornado ao programa de chamada.  
  
 Entretanto, nem todos os tipos de dados CLR podem ser automaticamente convertidos em seus tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes por um fora parâmetro out. A tabela a seguir lista estas exceções.  
  
|||  
|-|-|  
|**Tipo de dados CLR (SQL Server)**|**Tipo de dados do SQL Server**|  
|**Decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**Horário**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Os tipos **geography**, **SqlGeometry**e **SqlHierarchyId** foram adicionados à tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
