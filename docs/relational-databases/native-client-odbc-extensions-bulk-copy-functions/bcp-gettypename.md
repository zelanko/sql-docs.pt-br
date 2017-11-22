---
title: bcp_gettypename | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_gettypename
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f452b3c5e12b76ba2d1327b59f1cfa17f16bb46
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
 *campo*  
 Indica se o token solicitado é do tipo max.  
  
## <a name="returns"></a>Retorna  
 Uma cadeia de caracteres que contém o nome do tipo SQL que corresponde ao tipo BCP. Se um for especificado um tipo BCP inválido, uma cadeia de caracteres vazia será retornada.  
  
## <a name="remarks"></a>Comentários  
 Os tokens do tipo BCP são definidos arquivo do cabeçalho sqlncli.h e na biblioteca sqlncli11.lib.  
  
 A tabela a seguir especifica os possíveis tipos BCP, se eles são ou não tipos max e a saída esperada.  
  
|Nome do tipo BCP|MaxType|Saída|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|Qualquer|**decimal**|  
|**SQLNUMERIC**|Qualquer|**numeric**|  
|**SQLINT1**|Qualquer|**tinyint**|  
|**SQLINT2**|Qualquer|**smallint**|  
|**SQLINT4**|Qualquer|**int**|  
|**SQLMONEY**|Qualquer|**money**|  
|**SQLFLT8**|Qualquer|**float**|  
|**SQLDATETIME**|Qualquer|**datetime**|  
|**SQLBITN**|Qualquer|**bit nulo**|  
|**SQLBIT**|Qualquer|**bit**|  
|**SQLBIGCHAR**|Não|**char**|  
|**SQLCHARACTER**|Não|**char**|  
|**SQLBIGVARCHAR**|Não|**varchar**|  
|**SQLVARCHAR**|Não|**varchar**|  
|**SQLTEXT**|Qualquer|**texto**|  
|**SQLBIGBINARY**|Não|**binary**|  
|**SQLBINARY**|Não|**Binary**|  
|**SQLBIGVARBINARY**|Não|**Varbinary**|  
|**SQLVARBINARY**|Não|**Varbinary**|  
|**SQLIMAGE**|Qualquer|**Imagem**|  
|**SQLINTN**|Qualquer|**int null**|  
|**SQLDATETIMN**|Qualquer|**DateTime null**|  
|**SQLMONEYN**|Qualquer|**Money null**|  
|**SQLFLTN**|Qualquer|**float null**|  
|**SQLAOPSUM**|Qualquer|**Sum**|  
|**SQLAOPAVG**|Qualquer|**Avg**|  
|**SQLAOPCNT**|Qualquer|**Contagem**|  
|**SQLAOPMIN**|Qualquer|**Min**|  
|**SQLAOPMAX**|Qualquer|**Max**|  
|**SQLDATETIM4**|Qualquer|**smalldatetime**|  
|**SQLMONEY4**|Qualquer|**Smallmoney**|  
|**SQLFLT4**|Qualquer|**Real**|  
|**SQLUNIQUEID**|Qualquer|**uniqueidentifier**|  
|**SQLNCHAR**|Não|**Nchar**|  
|**SQLNVARCHAR**|Não|**Nvarchar**|  
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
 Os valores de parâmetro de token para tipos de data/hora são descritos na coluna "Tipo em SQLNCLI. h" da tabela na [alterações de cópia em massa para aprimorados de data e hora tipos &#40; OLE DB e ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). O valor retornado está na linha correspondente da coluna "Tipo de armazenamento de arquivo" coluna.  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
