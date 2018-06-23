---
title: Estrutura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8c8d98a54155179fe481fc0a7202a07e6cbf2aff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117213"
---
# <a name="ssvariant-structure"></a>Estrutura SSVARIANT
  A estrutura `SSVARIANT`, definida em sqlncli.h, corresponde a um valor DBTYPE_SQLVARIANT no provedor OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 `SSVARIANT` é uma união distinta. Dependendo do valor do membro vt, o consumidor pode determinar qual membro deve ser lido. os valores VT correspondem aos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados. Portanto, a estrutura `SSVARIANT` pode hospedar qualquer tipo do SQL Server. Para obter mais informações sobre a estrutura de dados para tipos de OLE DB padrão, consulte [indicadores de tipo](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Remarks  
 Quando DataTypeCompat==80, vários subtipos `SSVARIANT` se tornam cadeias de caracteres. Por exemplo, os valores vt seguintes aparecerão em `SSVARIANT` como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, estes tipos aparecerão no seu formulário nativo.  
  
 Para obter mais informações sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [usando Conexão String Keywords with SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O arquivo sqlncli.h contém macros de acesso variantes que são simplificados, eliminando a referência dos tipos de membro na estrutura `SSVARIANT`. Um exemplo é V_SS_DATETIMEOFFSET que você pode usar da seguinte maneira:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obter o conjunto completo de macros de acesso para cada membro da estrutura `SSVARIANT`, consulte o arquivo sqlncli.hi.  
  
 A tabela a seguir descreve os membros da estrutura `SSVARIANT`:  
  
|Membro|Indicador de tipo OLE DB|Tipo de dados OLE DB C|valor vt|Comentários|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Especifica o tipo de valor contido na estrutura `SSVARIANT`.|  
|bTinyIntVal|DBTYPE_UI1|`BYTE`|`VT_SS_UI1`|Oferece suporte a `tinyint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|sShortIntVal|DBTYPE_I2|`SHORT`|`VT_SS_I2`|Oferece suporte a `smallint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|lIntVal|DBTYPE_I4|`LONG`|`VT_SS_I4`|Oferece suporte a `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|llBigIntVal|DBTYPE_I8|`LARGE_INTEGER`|`VT_SS_I8`|Oferece suporte a `bigint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|fltRealVal|DBTYPE_R4|`float`|`VT_SS_R4`|Oferece suporte a `real` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|dblFloatVal|DBTYPE_R8|`double`|`VT_SS_R8`|Oferece suporte a `float` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|cyMoneyVal|DBTYPE_CY|`LARGE_INTEGER`|**VT_SS_MONEY VT_SS_SMALLMONEY**|Oferece suporte a `money` e **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.|  
|fBitVal|DBTYPE_BOOL|`VARIANT_BOOL`|`VT_SS_BIT`|Oferece suporte a `bit` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|rgbGuidVal|DBTYPE_GUID|`GUID`|`VT_SS_GUID`|Oferece suporte a `uniqueidentifier` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|numNumericVal|DBTYPE_NUMERIC|`DB_NUMERIC`|`VT_SS_NUMERIC`|Oferece suporte a `numeric` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|dDateVal|DBTYPE_DATE|`DBDATE`|`VT_SS_DATE`|Oferece suporte a `date` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2`|Oferece suporte a `smalldatetime`, `datetime`, e `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.|  
|Time2Val|DBTYPE_DBTIME2|`DBTIME2`|`VT_SS_TIME2`|Oferece suporte a `time` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tTime2Val* (`DBTIME2`)<br /><br /> *bScale* (`BYTE`) Especifica a escala de *tTime2Val* valor.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_DATETIME2`|Oferece suporte a `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (`BYTE`) Especifica a escala de *tsDataTimeVal* valor.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|`DBTIMESTAMPOFFSET`|`VT_SS_DATETIMEOFFSET`|Oferece suporte a `datetimeoffset` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tsoDateTimeOffsetVal* (`DBTIMESTAMPOFFSET`)<br /><br /> *bScale* (`BYTE`) Especifica a escala de *tsoDateTimeOffsetVal* valor.|  
|NCharVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _NCharVal`|`VT_SS_WVARSTRING,`<br /><br /> `VT_SS_WSTRING`|Oferece suporte a `nchar` e **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) Especifica o comprimento real para a cadeia de caracteres para o qual *pwchNCharVal* pontos. Não inclui o zero final.<br /><br /> *sMaxLength* (`SHORT`) Especifica o comprimento máximo para a cadeia de caracteres para o qual *pwchNCharVal* pontos.<br /><br /> *pwchNCharVal* (`WCHAR` \*) ponteiro para a cadeia de caracteres.<br /><br /> Membros não usados: *rgbReserved*, *dwReserved*, e *pwchReserved*.|  
|CharVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _CharVal`|`VT_SS_STRING,`<br /><br /> `VT_SS_VARSTRING`|Oferece suporte a `char` e **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) Especifica o comprimento real para a cadeia de caracteres para o qual *pchCharVal* pontos. Não inclui o zero final.<br /><br /> *sMaxLength* (`SHORT`) Especifica o comprimento máximo para a cadeia de caracteres para o qual *pchCharVal* pontos.<br /><br /> *pchCharVal* (`CHAR` \*) ponteiro para a cadeia de caracteres.<br /><br /> Membros não usados:<br /><br /> *rgbReserved*, *dwReserved*, e *pwchReserved*.|  
|BinaryVal|Não existe um indicador de tipo OLE DB correspondente.|`struct _BinaryVal`|`VT_SS_VARBINARY,`<br /><br /> `VT_SS_BINARY`|Oferece suporte a `binary` e **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (`SHORT`) Especifica o comprimento real dos dados para o qual *prgbBinaryVal* pontos.<br /><br /> *sMaxLength* (`SHORT`) Especifica o comprimento máximo para os dados para o qual *prgbBinaryVal* pontos.<br /><br /> *prgbBinaryVal* (`BYTE` \*) ponteiro para os dados binários.<br /><br /> Membro não usado: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  