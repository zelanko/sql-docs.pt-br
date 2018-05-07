---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_gettypename
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3a7f4e8a8b6813eecf74fbc4e932296d3eff4631
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bcpgettypename"></a>bcp_gettypename
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Retorna o nome do tipo SQL para um token do tipo BCP especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *token*  
 Um valor que indica um token do tipo BCP.  
  
 *field*  
 Indica se o token solicitado é do tipo max.  
  
## <a name="returns"></a>Retorna  
 Uma cadeia de caracteres que contém o nome do tipo SQL que corresponde ao tipo BCP. Se um for especificado um tipo BCP inválido, uma cadeia de caracteres vazia será retornada.  
  
## <a name="remarks"></a>Remarks  
 Os tokens do tipo BCP são definidos arquivo do cabeçalho sqlncli.h e na biblioteca sqlncli11.lib.  
  
 A tabela a seguir especifica os possíveis tipos BCP, se eles são ou não tipos max e a saída esperada.  
  
|Nome do tipo BCP|MaxType|Saída|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|Qualquer|**decimal**|  
|**SQLNUMERIC**|Qualquer|**numeric**|  
|**SQLINT1**|Qualquer|**tinyint**|  
|**SQLINT2**|Qualquer|**smallint**|  
|**SQLINT4**|Qualquer|**Int**|  
|**SQLMONEY**|Qualquer|**money**|  
|**SQLFLT8**|Qualquer|**float**|  
|**SQLDATETIME**|Qualquer|**datetime**|  
|**SQLBITN**|Qualquer|**bit-null**|  
|**SQLBIT**|Qualquer|**bit**|  
|**SQLBIGCHAR**|não|**char**|  
|**SQLCHARACTER**|não|**char**|  
|**SQLBIGVARCHAR**|não|**varchar**|  
|**SQLVARCHAR**|não|**varchar**|  
|**SQLTEXT**|Qualquer|**text**|  
|**SQLBIGBINARY**|não|**binary**|  
|**SQLBINARY**|não|**Binary**|  
|**SQLBIGVARBINARY**|não|**varbinary**|  
|**SQLVARBINARY**|não|**varbinary**|  
|**SQLIMAGE**|Qualquer|**Imagem**|  
|**SQLINTN**|Qualquer|**int-null**|  
|**SQLDATETIMN**|Qualquer|**datetime-null**|  
|**SQLMONEYN**|Qualquer|**money-null**|  
|**SQLFLTN**|Qualquer|**float-null**|  
|**SQLAOPSUM**|Qualquer|**Sum**|  
|**SQLAOPAVG**|Qualquer|**Avg**|  
|**SQLAOPCNT**|Qualquer|**Count**|  
|**SQLAOPMIN**|Qualquer|**Min**|  
|**SQLAOPMAX**|Qualquer|**Max**|  
|**SQLDATETIM4**|Qualquer|**smalldatetime**|  
|**SQLMONEY4**|Qualquer|**Smallmoney**|  
|**SQLFLT4**|Qualquer|**Real**|  
|**SQLUNIQUEID**|Qualquer|**uniqueidentifier**|  
|**SQLNCHAR**|não|**nchar**|  
|**SQLNVARCHAR**|não|**Nvarchar**|  
|**SQLNTEXT**|Qualquer|**Ntext**|  
|**SQLVARIANT**|Qualquer|**sql_variant**|  
|**SQLINT8**|Qualquer|**Bigint**|  
|**SQLCHARACTER**|Sim|**varchar(max)**|  
|**SQLBIGCHAR**|Sim|**varchar(max)**|  
|**SQLBIGVARCHAR**|Sim|**varchar(max)**|  
|**SQLVARCHAR**|Sim|**varchar(max)**|  
|**SQLBINARY**|Sim|**varbinary(max)**|  
|**SQLBIGBINARY**|Sim|**varbinary(max)**|  
|**SQLBIGVARBINARY**|Sim|**varbinary(max)**|  
|**SQLVARBINARY**|Sim|**varbinary(max)**|  
|**SQLNCHAR**|Sim|**nvarchar(max)**|  
|**SQLNVARCHAR**|Sim|**nvarchar(max)**|  
|**SQLXML**|Sim|**Xml**|  
|**SQLUDT**|Qualquer|**UDT**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_gettypename a recursos aprimorados de data e hora  
 Os valores de parâmetro de token para tipos de data/hora são descritos na coluna "Tipo em SQLNCLI. h" da tabela na [alterações de cópia em massa para tipos aprimorados de data e hora &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). O valor retornado está na linha correspondente da coluna "Tipo de armazenamento de arquivo" coluna.  
  
 Para obter mais informações, consulte [data e hora melhorias & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
