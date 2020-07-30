---
title: sys. external_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e0341c16a8aa78497aa0e1e347d5cc079a26b6b
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394068"
---
# <a name="sysexternal_tables-transact-sql"></a>sys. external_tables (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada tabela externa no banco de dados atual.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<inherited columns>||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).||  
|max_column_id_used|**int**|ID de coluna máximo que já foi usada para esta tabela.||  
|uses_ansi_nulls|**bit**|A tabela foi criada com a opção de banco de dados SET ANSI_NULLS definida como ON.||  
|data_source_id|**int**|ID de objeto para a fonte de dados externa.||  
|file_format_id|**int**|Para tabelas externas em uma fonte de dados externa do HADOOP, essa é a ID de objeto para o formato de arquivo externo.||  
|local|**nvarchar(4000)**|Para tabelas externas em uma fonte de dados externa do HADOOP, esse é o caminho dos dados externos no HDFS.||  
|reject_type|**tinyint**|Para tabelas externas em uma fonte de dados externa do HADOOP, essa é a maneira como as linhas rejeitadas são contadas ao consultar dados externos.|VALOR-o número de linhas rejeitadas.<br /><br /> PORCENTAGEM-a porcentagem de linhas rejeitadas.|  
|reject_value|**float**|Para tabelas externas em uma fonte de dados externa do HADOOP:<br /><br /> Para *reject_type =* Value, é o número de rejeições de linha a permitir antes de falhar a consulta.<br /><br /> Por *reject_type* = Percentage, essa é a porcentagem de rejeições de linha a permitir antes de falhar a consulta.||  
|reject_sample_value|**int**|Por *reject_type* = Percentage, esse é o número de linhas a serem carregadas com êxito ou não, antes de calcular a porcentagem de linhas rejeitadas.|NULL se reject_type = VALUE.|  
|distribution_type|**int**|Para tabelas externas em uma SHARD_MAP_MANAGER fonte de dados externa, essa é a distribuição de dados das linhas nas tabelas base subjacentes.|0-fragmentado<br /><br /> 1-replicado<br /><br /> 2-Round Robin|  
|distribution_desc|**nvarchar(120)**|Para tabelas externas em uma SHARD_MAP_MANAGER fonte de dados externa, esse é o tipo de distribuição exibido como uma cadeia de caracteres.||  
|sharding_column_id|**int**|Para tabelas externas em uma SHARD_MAP_MANAGER fonte de dados externa e uma distribuição fragmentada, essa é a ID de coluna da coluna que contém os valores de chave de fragmentação.||  
|remote_schema_name|**sysname**|Para tabelas externas em uma SHARD_MAP_MANAGER fonte de dados externa, esse é o esquema onde a tabela base está localizada nos bancos de dados remotos (se for diferente do esquema onde a tabela externa está definida).||  
|remote_object_name|**sysname**|Para tabelas externas em uma SHARD_MAP_MANAGER fonte de dados externa, esse é o nome da tabela base nos bancos de dados remotos (se for diferente do nome da tabela externa).||  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys. external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
