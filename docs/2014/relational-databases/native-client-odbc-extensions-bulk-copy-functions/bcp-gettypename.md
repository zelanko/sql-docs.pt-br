---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: afea684549765bac4c24679cc65d74bb4dfa47df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013333"
---
# <a name="bcpgettypename"></a>bcp_gettypename
  Retorna o nome do tipo SQL para um token do tipo BCP especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
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
|`SQLDECIMAL`|Qualquer|**decimal**|  
|`SQLNUMERIC`|Qualquer|**numeric**|  
|`SQLINT1`|Qualquer|**tinyint**|  
|`SQLINT2`|Qualquer|**smallint**|  
|`SQLINT4`|Qualquer|**int**|  
|`SQLMONEY`|Qualquer|**money**|  
|`SQLFLT8`|Qualquer|**float**|  
|`SQLDATETIME`|Qualquer|**datetime**|  
|`SQLBITN`|Qualquer|**bit-null**|  
|`SQLBIT`|Qualquer|**bit**|  
|`SQLBIGCHAR`|não|**char**|  
|`SQLCHARACTER`|não|**char**|  
|`SQLBIGVARCHAR`|não|**varchar**|  
|`SQLVARCHAR`|não|**varchar**|  
|`SQLTEXT`|Qualquer|**text**|  
|`SQLBIGBINARY`|não|**binary**|  
|`SQLBINARY`|não|**Binary**|  
|`SQLBIGVARBINARY`|não|**varbinary**|  
|`SQLVARBINARY`|não|**varbinary**|  
|`SQLIMAGE`|Qualquer|**Imagem**|  
|`SQLINTN`|Qualquer|**int-null**|  
|`SQLDATETIMN`|Qualquer|**datetime-null**|  
|`SQLMONEYN`|Qualquer|**money-null**|  
|`SQLFLTN`|Qualquer|**float-null**|  
|`SQLAOPSUM`|Qualquer|**Sum**|  
|`SQLAOPAVG`|Qualquer|**Avg**|  
|`SQLAOPCNT`|Qualquer|**Contagem**|  
|`SQLAOPMIN`|Qualquer|**Min**|  
|`SQLAOPMAX`|Qualquer|**Max**|  
|`SQLDATETIM4`|Qualquer|**smalldatetime**|  
|`SQLMONEY4`|Qualquer|**Smallmoney**|  
|`SQLFLT4`|Qualquer|**real**|  
|`SQLUNIQUEID`|Qualquer|**uniqueidentifier**|  
|`SQLNCHAR`|não|**nchar**|  
|`SQLNVARCHAR`|não|**Nvarchar**|  
|`SQLNTEXT`|Qualquer|**Ntext**|  
|`SQLVARIANT`|Qualquer|**sql_variant**|  
|`SQLINT8`|Qualquer|**Bigint**|  
|`SQLCHARACTER`|Sim|**varchar(max)**|  
|`SQLBIGCHAR`|Sim|**varchar(max)**|  
|`SQLBIGVARCHAR`|Sim|**varchar(max)**|  
|`SQLVARCHAR`|Sim|**varchar(max)**|  
|`SQLBINARY`|Sim|**varbinary(max)**|  
|`SQLBIGBINARY`|Sim|**varbinary(max)**|  
|`SQLBIGVARBINARY`|Sim|**varbinary(max)**|  
|`SQLVARBINARY`|Sim|**varbinary(max)**|  
|`SQLNCHAR`|Sim|**nvarchar(max)**|  
|`SQLNVARCHAR`|Sim|**nvarchar(max)**|  
|`SQLXML`|Sim|**Xml**|  
|`SQLUDT`|Qualquer|**UDT**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_gettypename a recursos aprimorados de data e hora  
 Os valores de parâmetro de token para tipos de data/hora são descritos na coluna "Tipo em SQLNCLI. h" da tabela na [alterações de cópia em massa para tipos aprimorados de data e hora &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). O valor retornado está na linha correspondente da coluna "Tipo de armazenamento de arquivo" coluna.  
  
 Para obter mais informações, consulte [data e hora melhorias &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  