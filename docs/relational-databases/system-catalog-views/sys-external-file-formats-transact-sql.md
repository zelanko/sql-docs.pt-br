---
title: sys. external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae119fe16b916f47f1acdcd2ebe15efd96e51e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68048393"
---
# <a name="sysexternal_file_formats-transact-sql"></a>sys. external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada formato de arquivo externo no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]atual [!INCLUDE[ssSDS](../../includes/sssds-md.md)]para, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]e.  
  
 Contém uma linha para cada formato de arquivo externo no servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]o.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|ID de objeto para o formato de arquivo externo.||  
|name|**sysname**|Nome do formato de arquivo. no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], isso é exclusivo para o banco de dados. No [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], isso é exclusivo para o servidor.||  
|format_type|**tinyint**|O tipo de formato de arquivo.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar (10)**|Para format_type = DELIMITEDTEXT, esse é o terminador de campo.||  
|string_delimiter|**nvarchar (10)**|Para format_type = DELIMITEDTEXT, esse é o delimitador de cadeia de caracteres.||  
|date_format|**nvarchar(50)**|Para format_type = DELIMITEDTEXT, este é o formato de data e hora definido pelo usuário.||  
|use_type_default|**bit**|Por format_type = texto delimitado, especifica como lidar com valores ausentes quando o polybase está importando dados de arquivos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]de texto do HDFS para o.|0-armazenar valores ausentes como a cadeia de caracteres ' NULL '.<br /><br /> 1-armazenar valores ausentes como o valor padrão da coluna.|  
|serde_method|**nvarchar (255)**|Para format_type = RCFILE, esse é o método de serialização/desserialização.||  
|row_terminator|**nvarchar (10)**|Para format_type = DELIMITEDTEXT, essa é a cadeia de caracteres que encerra cada linha no arquivo do Hadoop externo.|Sempre ' \n '.|  
|codificando|**nvarchar (10)**|Para format_type = DELIMITEDTEXT, esse é o método de codificação para o arquivo do Hadoop externo.|Sempre ' UTF8 '.|  
|data_compression|**nvarchar (255)**|O método de compactação de dados para os dados externos.|Para format_type = DELIMITEDTEXT:<br /><br /> -' org. Apache. Hadoop. IO. compress. defaultcodec '<br />-' org. Apache. Hadoop. IO. compress. GzipCodec '<br /><br /> Para format_type = RCFILE:<br /><br /> -' org. Apache. Hadoop. IO. compress. defaultcodec '<br /><br /> Para format_type = ORC:<br /><br /> -' org. Apache. Hadoop. IO. compress. defaultcodec '<br />-' org. Apache. Hadoop. IO. compress. SnappyCodec '<br /><br /> Para format_type = PARQUET:<br /><br /> -' org. Apache. Hadoop. IO. compress. GzipCodec '<br />-' org. Apache. Hadoop. IO. compress. SnappyCodec '|  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão.  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys. external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
