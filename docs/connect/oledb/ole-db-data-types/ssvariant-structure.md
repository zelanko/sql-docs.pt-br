---
title: Estrutura de SSVARIANT (driver do OLE DB)
description: Estrutura SSVARIANT no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 701476b8e1cea1f84d7fdbf970a345311d686cfd
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860060"
---
# <a name="ssvariant-structure"></a>Estrutura SSVARIANT
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A estrutura **SSVARIANT**, que é definida em msoledbsql.h, corresponde a um valor DBTYPE_SQLVARIANT no Driver do OLE DB para SQL Server.  
  
 **SSVARIANT** é uma união distinta. Dependendo do valor do membro vt, o consumidor pode determinar qual membro deve ser lido. Os valores vt correspondem aos tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Portanto, a estrutura **SSVARIANT** pode manter qualquer tipo do SQL Server. Para obter mais informações sobre a estrutura de dados para tipos OLE DB padrão, confira [Indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Comentários  
 Quando DataTypeCompat==80, vários subtipos **SSVARIANT** se tornam cadeias de caracteres. Por exemplo, os seguintes valores vt serão exibidos em **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, estes tipos aparecerão no seu formulário nativo.  
  
 Para obter mais informações sobre SSPROP_INIT_DATATYPECOMPATIBILITY, confira [Como usar palavras-chave da cadeia de conexão com o Driver do OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 O arquivo msoledbsql.h contém macros de acesso a variantes que simplificam a desreferência dos tipos de membro na estrutura **SSVARIANT**. Um exemplo é V_SS_DATETIMEOFFSET que você pode usar da seguinte maneira:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obter o conjunto completo de macros de acesso para cada membro da estrutura **SSVARIANT**, veja o arquivo msoledbsql.h.  
  
 A seguinte tabela descreve os membros da estrutura **SSVARIANT**:  
  
|Membro|Indicador de tipo OLE DB|Tipo de dados OLE DB C|valor vt|Comentários|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica o tipo de valor contido no struct **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Dá suporte ao tipo de dados **tinyint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Dá suporte ao tipo de dados **smallint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Dá suporte ao tipo de dados **int**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Dá suporte ao tipo de dados **bigint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Dá suporte ao tipo de dados **real**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Dá suporte ao tipo de dados **float**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Dá suporte aos tipos de dados **money** e **smallmoney**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Dá suporte ao tipo de dados **bit**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Dá suporte ao tipo de dados **uniqueidentifier**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Dá suporte ao tipo de dados **numeric**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Dá suporte ao tipo de dados **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Dá suporte aos tipos de dados **smalldatetime**, **datetime** e **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Dá suporte ao tipo de dados **time**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) Especifica a escala para o valor *tTime2Val*.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Dá suporte ao tipo de dados **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) Especifica a escala para o valor *tsDataTimeVal*.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Dá suporte ao tipo de dados **datetimeoffset**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) Especifica a escala para o valor *tsoDateTimeOffsetVal*.|  
|NCharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Dá suporte aos tipos de dados **nchar** e **nvarchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**SHORT**) especifica o comprimento real da cadeia de caracteres para a qual *pwchNCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (**SHORT**) especifica o comprimento máximo da cadeia de caracteres para a qual *pwchNCharVal* aponta.<br /><br /> *pwchNCharVal* (**WCHAR** \*) Ponteiro para a cadeia de caracteres.<br /><br /> *rgbReserved* (**BYTE [5]** ) especifica as informações de ordenação.<br /><br /> Membros não usados: *dwReserved* e *pwchReserved*.|  
|CharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Dá suporte aos tipos de dados **char** e **varchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**SHORT**) especifica o comprimento real da cadeia de caracteres para a qual *pchCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (**SHORT**) especifica o comprimento máximo da cadeia de caracteres para a qual *pchCharVal* aponta.<br /><br /> *pchCharVal* (**CHAR** \*) Ponteiro para a cadeia de caracteres.<br /><br /> *rgbReserved* (**BYTE [5]** ) especifica as informações de ordenação.<br /><br /> Membros não usados:<br /><br /> *dwReserved* e *pwchReserved*.|  
|BinaryVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Dá suporte aos tipos de dados **binary** e **varbinary**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**SHORT**) especifica o comprimento real dos dados para os quais *prgbBinaryVal* aponta.<br /><br /> *sMaxLength* (**SHORT**) especifica o comprimento máximo dos dados para os quais *prgbBinaryVal* aponta.<br /><br /> *prgbBinaryVal* (**BYTE** \*) Ponteiro para os dados binários.<br /><br /> Membro não usado: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="known-issues"></a>Problemas conhecidos
### <a name="possible-narrow-string-data-corruption"></a>Possibilidade de dados corrompidos na cadeia de caracteres estreita
Antes da versão 18.4 do driver do OLE DB, a inserção em uma coluna `sql_variant` poderia resultar em dados corrompidos no servidor se todas as seguintes condições fossem verdadeiras:
- A página de código do computador cliente não correspondia à página de código de ordenação do banco de dados.
- O buffer do cliente para inserção de caracteres não ASCII contidos de cadeia de caracteres estreita era codificado na página de código do cliente.
- Uma das destas condições era verdadeira:
  - O campo `pwszDataSourceType` na estrutura `DBPARAMBINDINFO` descrevendo o parâmetro correspondente à coluna `sql_variant` era definido como `L"DBTYPE_SQLVARIANT"`, `L"DBTYPE_VARIANT"` ou `L"sql_variant"`. Para obter detalhes, confira: [ICommandWithParameters::SetParameterInfo](https://docs.microsoft.com/previous-versions/windows/desktop/ms725393(v=vs.85)).

    *or*
  - A consulta SQL parametrizada usada para inserção era preparada.

Mais especificamente, o driver do OLE DB não convertia os dados para a página de código de ordenação do banco de dados antes de inseri-los. No entanto, o driver indicava incorretamente para o servidor que os dados haviam sido codificados na página de código de ordenação do banco de dados. Esse comportamento levava a uma incompatibilidade entre os dados e sua página de código correspondente armazenada na coluna `sql_variant`.

De maneira semelhante, após a recuperação do mesmo valor, o driver do OLE DB não convertia cadeias de caracteres na página de código do cliente. No entanto, como os dados inseridos já estavam na página de código do cliente (consulte o parágrafo acima), o aplicativo cliente podia interpretar os dados corretamente. Mesmo assim, aplicativos que usassem outros drivers recuperariam esses valores em um formato corrompido. A corrupção ocorria porque outros drivers interpretavam a cadeia de caracteres na página de código de ordenação do banco de dados e tentavam convertê-los na página de código do cliente.

Começando com a versão 18.4, o driver do OLE DB converte as cadeias de caracteres estreitas para a página de código de ordenação do banco de dados antes da inserção. Da mesma forma, o driver converte os dados de volta para a página de código do cliente após a recuperação. Como resultado, aplicativos cliente que dependem do bug mencionado acima podem enfrentar problemas ao recuperar dados inseridos usando uma versão anterior do driver do OLE DB. O [procedimento de recuperação](#recovery-procedure) a seguir destina-se a fornecer diretrizes para resolver esses problemas.

### <a name="recovery-procedure"></a>Procedimento de recuperação
> [!IMPORTANT]  
> Antes de executar as etapas de recuperação abaixo, faça backup dos dados existentes.

Se o seu aplicativo apresentar problemas ao recuperar dados de uma coluna `sql_variant` depois de alternar para a versão 18.4 do driver do OLE DB, os dados corrompidos precisarão ser modificados para ter a mesma ordenação que a do banco de dados no qual estão armazenados. O script a seguir pode ser usado para recuperar um só valor de uma coluna `sql_variant`. O script é um modelo e você precisa ajustá-lo ao seu cenário.

> [!IMPORTANT]  
> Como a página de código original dos dados não é armazenada, você precisa informar ao servidor como os dados foram codificados inicialmente. Para fazer isso, execute o script no contexto de um banco de dados que tenha a mesma página de código que a do cliente que inseriu os dados primeiro. Por exemplo, se os dados corrompidos tiverem sido inseridos de um cliente configurado com a página de código `932`, o script a seguir precisará ser executado dentro do contexto de um banco de dados com uma ordenação em japonês (por exemplo, `Japanese_XJIS_100_CS_AI`).

```sql
/*
    Description:
        Template that can be used to recover the corrupted value inserted into the sql_variant column.

    Scenario:
        The database is named [YourDatabase] and it contains a table named [YourTable], which contains the corrupted value.
        Schema is named [dbo].
        The corrupted value is stored in a column of type sql_variant named [YourColumn].
        The corrupted value is sql_variant of BaseType char. For details on sql_variant properties, see:
            https://docs.microsoft.com/sql/t-sql/functions/sql-variant-property-transact-sql
*/

-- Base type in sql_variant can hold a maximum of 8000 bytes
-- For details see: 
--  https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql#remarks
DECLARE @bin VARBINARY(8000)

-- In the following lines we convert the sql_variant base type to binary.
-- <FilterExpression>
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
SET @bin = (SELECT CAST([YourColumn] AS VARBINARY(8000)) FROM [YourDatabase].[dbo].[YourTable] WHERE <FilterExpression>)

-- In the following lines we store the binary value in char(59) (a fixed-size character data type).
-- IMPORTANT NOTE: 
--      This example assumes the corrupted sql_variant's base type is char(59).
--      You MUST adjust the type (that is, char/varchar) and size to match your scenario exactly.
DECLARE @char CHAR(59)
SET @char = CAST((@bin) AS CHAR(59))
DECLARE @sqlvariant sql_variant

-- The following lines recover the corrupted value by translating the value to the collation of the database.
-- <DBCollation>
--      Must be replaced with the collation (for example, Latin1_General_100_CI_AS_SC_UTF8) of the database holding the data.
SET @sqlvariant = @char collate <DBCollation>

-- Finally, we update the corrupted value with the recovered value.
-- "<FilterExpression>"
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
UPDATE [YourDatabase].[dbo].[YourTable] SET [YourColumn] = @sqlvariant WHERE <FilterExpression>
```

## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
