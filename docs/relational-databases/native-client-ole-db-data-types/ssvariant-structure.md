---
title: Estrutura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 6c15bfc29ae02e362ea1010ef67b0a99e4b05dc0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551126"
---
# <a name="ssvariant-structure"></a>Estrutura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O **SSVARIANT** estrutura, que é definida em SQLNCLI. h, corresponde a um valor DBTYPE_SQLVARIANT no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLEDB.  
  
 **SSVARIANT** é uma união distinta. Dependendo do valor do membro vt, o consumidor pode determinar qual membro deve ser lido. Os valores vt correspondem aos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, a estrutura **SSVARIANT** pode manter qualquer tipo do SQL Server. Para obter mais informações sobre a estrutura de dados para tipos OLE DB padrão, consulte [indicadores de tipo](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Remarks  
 Quando DataTypeCompat==80, vários subtipos **SSVARIANT** se tornam cadeias de caracteres. Por exemplo, os seguintes valores vt serão exibidos em **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, estes tipos aparecerão no seu formulário nativo.  
  
 Para obter mais informações sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [usando Conexão String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O arquivo SQLNCLI. h contém macros do acesso variantes que simplificam a remoção de referência os tipos de membro na **SSVARIANT** estrutura. Um exemplo é V_SS_DATETIMEOFFSET que você pode usar da seguinte maneira:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para o conjunto completo de macros de acesso para cada membro do **SSVARIANT** estrutura, consulte o arquivo Hi.  
  
 A seguinte tabela descreve os membros da estrutura **SSVARIANT**:  
  
|Membro|Indicador de tipo OLE DB|Tipo de dados OLE DB C|valor vt|Comentários|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Especifica o tipo de valor contido no struct **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Dá suporte a **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Dá suporte a **smallint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Dá suporte a **int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Dá suporte a **bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Dá suporte a **reais** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Dá suporte a **float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Dá suporte a **dinheiro** e **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Dá suporte a **bits** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Dá suporte a **uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Dá suporte a **numéricos** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Dá suporte ao tipo de dados **date**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Dá suporte a **smalldatetime**, **datetime**, e **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Dá suporte a **tempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**bytes**) Especifica a escala de *tTime2Val* valor.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Dá suporte a **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**bytes**) Especifica a escala de *tsDataTimeVal* valor.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Dá suporte a **datetimeoffset** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**bytes**) Especifica a escala de *tsoDateTimeOffsetVal* valor.|  
|NCharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Dá suporte a **nchar** e **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**CURTO**) Especifica o comprimento real para a cadeia de caracteres *pwchNCharVal* pontos. Não inclui o zero final.<br /><br /> *sMaxLength* (**CURTO**) Especifica o comprimento máximo para a cadeia de caracteres *pwchNCharVal* pontos.<br /><br /> *pwchNCharVal* (**WCHAR** \*) ponteiro para a cadeia de caracteres.<br /><br /> Membros não usados: *rgbReserved*, *dwReserved*, e *pwchReserved*.|  
|CharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Dá suporte a **char** e **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**CURTO**) Especifica o comprimento real da cadeia de caracteres que *pchCharVal* pontos. Não inclui o zero final.<br /><br /> *sMaxLength* (**CURTO**) Especifica o comprimento máximo da cadeia de caracteres que *pchCharVal* pontos.<br /><br /> *pchCharVal* (**CHAR** \*) ponteiro para a cadeia de caracteres.<br /><br /> Membros não usados:<br /><br /> *rgbReserved*, *dwReserved*, e *pwchReserved*.|  
|BinaryVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Dá suporte a **binário** e **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**CURTO**) Especifica o comprimento real para os dados para o qual *prgbBinaryVal* pontos.<br /><br /> *sMaxLength* (**CURTO**) Especifica o comprimento máximo para os dados para o qual *prgbBinaryVal* pontos.<br /><br /> *prgbBinaryVal* (**bytes** \*) ponteiro para os dados binários.<br /><br /> Membro não utilizado: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
