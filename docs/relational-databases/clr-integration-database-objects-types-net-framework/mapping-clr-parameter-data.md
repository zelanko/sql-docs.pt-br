---
title: "Mapeamento de dados de parâmetro CLR | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "71"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bee49e277d3492dc93bcdf29b65c1c3007cebe50
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-clr-parameter-data"></a>Mapeando dados de parâmetro CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]A seguinte tabela lista [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, seus equivalentes no common language runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no **SqlTypes** namespace e seus equivalentes CLR nativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Do .NET framework.  
  
||||  
|-|-|-|  
|**Tipo de dados do SQL Server**|Tipo (em System.Data.SqlTypes ou Microsoft.SqlServer.Types)|**Tipo de dados CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, anulável\<Int64 >**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte]**|  
|**bit**|**SqlBoolean**|**Booliano, anulável\<booliana >**|  
|**char**|Nenhuma|Nenhuma|  
|**cursor**|Nenhuma|Nenhuma|  
|**date**|**SqlDateTime**|**DateTime, anulável\<DateTime >**|  
|**datetime**|**SqlDateTime**|**DateTime, anulável\<DateTime >**|  
|**datetime2**|Nenhuma|**DateTime, anulável\<DateTime >**|  
|**DATETIMEOFFSET**|**Nenhuma**|**DateTimeOffset, anulável\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal, anulável\<Decimal >**|  
|**float**|**SqlDouble**|**Duplo, anulável\<duplo >**|  
|**geografia**|**SqlGeography**<br /><br /> **SqlGeography** é definido no Microsoft.SqlServer.Types.dll, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhuma|  
|**geometria**|**SqlGeometry**<br /><br /> **SqlGeometry** é definido no Microsoft.SqlServer.Types.dll, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhuma|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** é definido no Microsoft.SqlServer.Types.dll, que é instalado com o SQL Server e pode ser baixado do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack do](https://www.microsoft.com/download/details.aspx?id=52676).|Nenhuma|  
|**imagem**|Nenhuma|Nenhuma|  
|**int**|**SqlInt32**|**Int32, anulável\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal, anulável\<Decimal >**|  
|**nchar**|**SqlChars, SqlString**|**Cadeia de caracteres, Char]**|  
|**ntext**|Nenhuma|Nenhuma|  
|**numeric**|**SqlDecimal**|**Decimal, anulável\<Decimal >**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** é uma melhor correspondência para transferência de dados e acesso, e **SQLString** é uma melhor correspondência para executar operações de cadeia de caracteres.|**Cadeia de caracteres, Char]**|  
|**nvarchar(1), nchar (1)**|**SqlChars, SqlString**|**Char, String, Char [], Nullable\<char >**|  
|**real**|**SqlSingle** (o intervalo de **SqlSingle**, no entanto, é maior do que **real**)|**Único, anulável\<único >**|  
|**rowversion**|Nenhuma|**Byte]**|  
|**smallint**|**SqlInt16**|**Int16, anulável\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal, anulável\<Decimal >**|  
|**sql_variant**|Nenhuma|**Objeto**|  
|**table**|Nenhuma|Nenhuma|  
|**texto**|Nenhuma|Nenhuma|  
|**time**|Nenhuma|**Período de tempo, anulável\<TimeSpan >**|  
|**timestamp**|Nenhuma|Nenhuma|  
|**tinyint**|**SqlByte**|**Byte, anulável\<bytes >**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, anulável\<Guid >**|  
|**Type(UDT) definida pelo usuário**|Nenhuma|A mesma classe que é associada ao tipo definido pelo usuário no mesmo assembly ou em um assembly dependente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte [], Nullable\<bytes >**|  
|**varchar**|Nenhuma|Nenhuma|  
|**xml**|**SqlXml**|Nenhuma|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversão automática de tipo de dados com parâmetros out  
 Um método CLR pode retornar informações para o código de chamada ou programa marcando um parâmetro de entrada com o **out** modificador (Microsoft Visual c#) ou  **\<out () > ByRef** (Microsoft Visual Basic) Se o parâmetro de entrada é um tipo de dados CLR no **SqlTypes** namespace e o programa de chamada especifica seu equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados como o parâmetro de entrada, uma conversão de tipo ocorre automaticamente Quando o método CLR retorna o tipo de dados.  
  
 Por exemplo, o seguinte procedimento armazenado CLR tem um parâmetro de entrada de **SqlInt32** tipo de dados CLR que está marcado com **out** (c#) ou  **\<out () > ByRef** ( Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 Depois que o assembly é criado e é criado no banco de dados, o procedimento armazenado é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o Transact-SQL a seguir, que especifica um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de **int** como um parâmetro de saída:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando o CLR armazenado procedimento é chamado, o **SqlInt32** tipo de dados é automaticamente convertido em um **int** tipo de dados e retornada ao programa de chamada.  
  
 Entretanto, nem todos os tipos de dados CLR podem ser automaticamente convertidos em seus tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes por um fora parâmetro out. A tabela a seguir lista estas exceções.  
  
|||  
|-|-|  
|**Tipo de dados CLR (SQL Server)**|**Tipo de dados do SQL Server**|  
|**Decimal**|smallmoney|  
|**SqlMoney**|smallmoney|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionado **SqlGeography**, **SqlGeometry**, e **SqlHierarchyId** tipos para a tabela de mapeamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
