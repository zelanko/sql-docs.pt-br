---
title: sys.external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0cea1fb2dbb0175fcf69708ef2f3e2ae6cb50e11
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada formato de arquivo externo no banco de dados atual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contém uma linha para cada formato de arquivo externo no servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**Int**|ID de objeto para o formato de arquivo externo.||  
|nome|**sysname**|Nome do formato de arquivo. em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], isso é exclusivo para o banco de dados. Em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], isso é exclusivo para o servidor.||  
|format_type|**tinyint**|O tipo de formato de arquivo.|PARQUET DELIMITEDTEXT, RCFILE, ORC,|  
|field_terminator|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esse é o terminador de campo.||  
|string_delimiter|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, este é o delimitador de cadeia de caracteres.||  
|date_format|**nvarchar(50)**|Para format_type = DELIMITEDTEXT, isso é o formato de hora e data definido pelo usuário.||  
|use_type_default|**bit**|Para format_type = texto DELIMITADO, especifica como tratar valores ausentes quando PolyBase está importando dados de arquivos de texto HDFS para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|0 – armazenar valores ausentes como a cadeia de caracteres 'Nulo'.<br /><br /> 1 – armazene valores ausentes como o valor padrão da coluna.|  
|serde_method|**nvarchar(255)**|Para format_type = RCFILE, esse é o método de serialização/desserialização.||  
|row_terminator|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esta é a cadeia de caracteres que termina cada linha no arquivo Hadoop externo.|Sempre '\n'.|  
|codificando|**nvarchar(10)**|Para format_type = DELIMITEDTEXT, esse é o método de codificação para o arquivo do Hadoop externo.|Sempre 'UTF8'.|  
|data_compression|**nvarchar(255)**|O método de compactação de dados para dados externos.|Para format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Para format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Para format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Para format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
