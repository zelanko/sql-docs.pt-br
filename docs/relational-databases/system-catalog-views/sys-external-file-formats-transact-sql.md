---
title: external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: dea0275fbdeea5dc413d4fc69a1da224cd2a6a04
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560516"
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada formato de arquivo externo no banco de dados atual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contém uma linha para cada formato de arquivo externo no servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|ID de objeto para o formato de arquivo externo.||  
|nome|**sysname**|Nome do formato de arquivo. na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], isso é exclusivo para o banco de dados. No [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], isso é exclusivo para o servidor.||  
|format_type|**tinyint**|O tipo de formato de arquivo.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esse é o terminador de campo.||  
|string_delimiter|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, isso é o delimitador de cadeia de caracteres.||  
|date_format|**nvarchar(50)**|Para format_type = DELIMITEDTEXT, esta é a data definida pelo usuário e o formato de hora.||  
|use_type_default|**bit**|Para format_type = delimitado por texto, especifica como tratar valores ausentes quando o PolyBase está importando dados de arquivos de texto HDFS em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|0 – armazenar valores ausentes como a cadeia de caracteres 'NULL'.<br /><br /> 1 – armazene valores ausentes como o valor padrão da coluna.|  
|serde_method|**nvarchar(255)**|Para format_type = RCFILE, esse é o método de serialização/desserialização.||  
|row_terminator|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esta é a cadeia de caracteres que termina cada linha no arquivo Hadoop externo.|Sempre '\n'.|  
|codificando|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esse é o método de codificação para o arquivo do Hadoop externo.|Sempre 'UTF8'.|  
|data_compression|**nvarchar(255)**|O método de compactação de dados para os dados externos.|Para format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Para format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Para format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Para format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
