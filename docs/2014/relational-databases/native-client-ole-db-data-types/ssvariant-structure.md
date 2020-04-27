---
title: Estrutura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff6e37986378a66d94dc113c4e3fe072fe3c077f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63062494"
---
# <a name="ssvariant-structure"></a>Estrutura SSVARIANT
  A estrutura `SSVARIANT`, definida em sqlncli.h, corresponde a um valor DBTYPE_SQLVARIANT no provedor OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 `SSVARIANT` é uma união distinta. Dependendo do valor do membro vt, o consumidor pode determinar qual membro deve ser lido. Os valores vt correspondem aos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, a estrutura `SSVARIANT` pode hospedar qualquer tipo do SQL Server. Para obter mais informações sobre a estrutura de dados para tipos OLE DB padrão, confira [Indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Comentários  
 Quando DataTypeCompat==80, vários subtipos `SSVARIANT` se tornam cadeias de caracteres. Por exemplo, os valores vt seguintes aparecerão em `SSVARIANT` como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, estes tipos aparecerão no seu formulário nativo.  
  
 Para obter mais informações sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O arquivo sqlncli.h contém macros de acesso variantes que são simplificados, eliminando a referência dos tipos de membro na estrutura `SSVARIANT`. Um exemplo é V_SS_DATETIMEOFFSET que você pode usar da seguinte maneira:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obter o conjunto completo de macros de acesso para cada membro da estrutura `SSVARIANT`, consulte o arquivo sqlncli.hi.  
  
 A tabela a seguir descreve os membros da estrutura `SSVARIANT`:  
  
|Membro|Indicador de tipo OLE DB|Tipo de dados OLE DB C|valor vt|Comentários|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica o tipo de valor contido na estrutura `SSVARIANT`.|  
|bTinyIntVal|DBTYPE_UI1|`BYTE`|`VT_SS_UI1`|Dá suporte ao tipo de dados `tinyint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|`SHORT`|`VT_SS_I2`|Dá suporte ao tipo de dados `smallint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|`LONG`|`VT_SS_I4`|Dá suporte ao tipo de dados `int`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|`LARGE_INTEGER`|`VT_SS_I8`|Dá suporte ao tipo de dados `bigint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|`float`|`VT_SS_R4`|Dá suporte ao tipo de dados `real`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|`double`|`VT_SS_R8`|Dá suporte ao tipo de dados `float`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|`LARGE_INTEGER`|**VT_SS_MONEY VT_SS_SMALLMONEY**|Dá suporte `money` aos tipos de dados e **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|fBitVal|DBTYPE_BOOL|`VARIANT_BOOL`|`VT_SS_BIT`|Dá suporte ao tipo de dados `bit`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|`GUID`|`VT_SS_GUID`|Dá suporte ao tipo de dados `uniqueidentifier`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|`DB_NUMERIC`|`VT_SS_NUMERIC`|Dá suporte ao tipo de dados `numeric`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|`DBDATE`|`VT_SS_DATE`|Dá suporte ao tipo de dados `date`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2`|Dá suporte aos tipos de dados `smalldatetime`, `datetime` e `datetime2` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|`DBTIME2`|`VT_SS_TIME2`|Dá suporte ao tipo de dados `time`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tTime2Val* (`DBTIME2`)<br /><br /> *bScale* (`BYTE`) especifica a escala para o valor de *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_DATETIME2`|Dá suporte ao tipo de dados `datetime2`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (`BYTE`) especifica a escala para o valor de *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|`DBTIMESTAMPOFFSET`|`VT_SS_DATETIMEOFFSET`|Dá suporte ao tipo de dados `datetimeoffset`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsoDateTimeOffsetVal* (`DBTIMESTAMPOFFSET`)<br /><br /> *bScale* (`BYTE`) especifica a escala para o valor de *tsoDateTimeOffsetVal* .|  
|NCharVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _NCharVal`|`VT_SS_WVARSTRING,`<br /><br /> `VT_SS_WSTRING`|Dá suporte `nchar` aos tipos de dados e **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) especifica o comprimento real para a cadeia de caracteres para a qual *pwchNCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (`SHORT`) especifica o comprimento máximo da cadeia de caracteres para a qual o *pwchNCharVal* aponta.<br /><br /> *pwchNCharVal* ponteiro pwchNCharVal`WCHAR` \*() para a cadeia de caracteres.<br /><br /> Membros não usados: *rgbReserved*, *dwReserved* e *pwchReserved*.|  
|CharVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _CharVal`|`VT_SS_STRING,`<br /><br /> `VT_SS_VARSTRING`|Dá suporte `char` aos tipos de dados e **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) especifica o comprimento real para a cadeia de caracteres para a qual *pchCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (`SHORT`) especifica o comprimento máximo da cadeia de caracteres para a qual o *pchCharVal* aponta.<br /><br /> *pchCharVal* ponteiro pchCharVal`CHAR` \*() para a cadeia de caracteres.<br /><br /> Membros não usados:<br /><br /> *rgbReserved*, *dwReserved* e *pwchReserved*.|  
|BinaryVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _BinaryVal`|`VT_SS_VARBINARY,`<br /><br /> `VT_SS_BINARY`|Dá suporte `binary` aos tipos de dados e **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) especifica o comprimento real para os dados aos quais *prgbBinaryVal* pontos.<br /><br /> *sMaxLength* (`SHORT`) especifica o comprimento máximo para os dados aos quais o *prgbBinaryVal* aponta.<br /><br /> *prgbBinaryVal* ponteiro prgbBinaryVal`BYTE` \*() para os dados binários.<br /><br /> Membro não usado: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
