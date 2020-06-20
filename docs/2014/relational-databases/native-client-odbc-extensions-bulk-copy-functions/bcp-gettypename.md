---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0341d9ba11cd66fdbfb72a05521028098c56c400
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019436"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
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
  
 *campo*  
 Indica se o token solicitado é do tipo max.  
  
## <a name="returns"></a>Retornos  
 Uma cadeia de caracteres que contém o nome do tipo SQL que corresponde ao tipo BCP. Se um for especificado um tipo BCP inválido, uma cadeia de caracteres vazia será retornada.  
  
## <a name="remarks"></a>Comentários  
 Os tokens do tipo BCP são definidos arquivo do cabeçalho sqlncli.h e na biblioteca sqlncli11.lib.  
  
 A tabela a seguir especifica os possíveis tipos BCP, se eles são ou não tipos max e a saída esperada.  
  
|Nome do tipo BCP|MaxType|Saída|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|Você pode usar o|**decimal**|  
|`SQLNUMERIC`|Você pode usar o|**numeric**|  
|`SQLINT1`|Você pode usar o|**tinyint**|  
|`SQLINT2`|Você pode usar o|**smallint**|  
|`SQLINT4`|Você pode usar o|**int**|  
|`SQLMONEY`|Você pode usar o|**money**|  
|`SQLFLT8`|Você pode usar o|**float**|  
|`SQLDATETIME`|Você pode usar o|**datetime**|  
|`SQLBITN`|Você pode usar o|**bit-null**|  
|`SQLBIT`|Você pode usar o|**bit**|  
|`SQLBIGCHAR`|Não|**char**|  
|`SQLCHARACTER`|Não|**char**|  
|`SQLBIGVARCHAR`|Não|**varchar**|  
|`SQLVARCHAR`|Não|**varchar**|  
|`SQLTEXT`|Você pode usar o|**text**|  
|`SQLBIGBINARY`|Não|**binary**|  
|`SQLBINARY`|Não|**Binary**|  
|`SQLBIGVARBINARY`|Não|**Varbinary**|  
|`SQLVARBINARY`|Não|**Varbinary**|  
|`SQLIMAGE`|Você pode usar o|**Imagem**|  
|`SQLINTN`|Você pode usar o|**int-null**|  
|`SQLDATETIMN`|Você pode usar o|**datetime-null**|  
|`SQLMONEYN`|Você pode usar o|**money-null**|  
|`SQLFLTN`|Você pode usar o|**float-null**|  
|`SQLAOPSUM`|Você pode usar o|**SUM**|  
|`SQLAOPAVG`|Você pode usar o|**Média**|  
|`SQLAOPCNT`|Você pode usar o|**Count**|  
|`SQLAOPMIN`|Você pode usar o|**Min**|  
|`SQLAOPMAX`|Você pode usar o|**Maximizar**|  
|`SQLDATETIM4`|Você pode usar o|**smalldatetime**|  
|`SQLMONEY4`|Você pode usar o|**Smallmoney**|  
|`SQLFLT4`|Você pode usar o|**Foto**|  
|`SQLUNIQUEID`|Você pode usar o|**uniqueidentifier**|  
|`SQLNCHAR`|Não|**Nchar**|  
|`SQLNVARCHAR`|Não|**Nvarchar**|  
|`SQLNTEXT`|Você pode usar o|**Ntext**|  
|`SQLVARIANT`|Você pode usar o|**sql_variant**|  
|`SQLINT8`|Você pode usar o|**Bigint**|  
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
|`SQLUDT`|Você pode usar o|**UDT**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_gettypename a recursos aprimorados de data e hora  
 Os valores de parâmetro de token para tipos de data/hora são descritos na coluna "Type in sqlncli. h" da tabela em [alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). O valor retornado está na linha correspondente da coluna "Tipo de armazenamento de arquivo" coluna.  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
