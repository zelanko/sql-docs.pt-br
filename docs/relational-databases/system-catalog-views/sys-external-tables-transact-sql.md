---
title: sys.external_tables (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4f12fb4189752b8679d1648f2246ebfd1226c42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Contém uma linha para cada tabela externa no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<herdado colunas >||Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).||  
|max_column_id_used|**int**|ID de máximo de coluna já usada para essa tabela.||  
|uses_ansi_nulls|**bit**|A tabela foi criada com a opção de banco de dados SET ANSI_NULLS definida como ON.||  
|data_source_id|**int**|Identificação do objeto de fonte de dados externa.||  
|file_format_id|**int**|Para tabelas externas em uma fonte de dados externa do HADOOP, esta é a ID de objeto para o formato de arquivo externo.||  
|local|**nvarchar(4000)**|Para tabelas externas em uma fonte de dados externa do HADOOP, este é o caminho dos dados externos no HDFS.||  
|reject_type|**tinyint**|Para tabelas externas em uma fonte de dados externa do HADOOP, essa é a maneira linhas rejeitadas são contadas ao consultar dados externos.|VALOR – o número de linhas rejeitadas.<br /><br /> Porcentagem – a porcentagem de linhas rejeitadas.|  
|reject_value|**float**|Para tabelas externas em uma fonte de dados externa do HADOOP:<br /><br /> Para *reject_type =* valor, este é o número de rejeições da linha para permitir antes da falha da consulta.<br /><br /> Para *reject_type* = porcentagem, esta é a porcentagem de rejeições da linha para permitir antes da falha da consulta.||  
|reject_sample_value|**int**|Para *reject_type* = porcentagem, este é o número de linhas a serem carregadas, com ou sem êxito, antes de calcular a porcentagem de linhas rejeitadas.|NULO se reject_type = valor.|  
|distribution_type|**int**|Para tabelas externas em uma fonte de dados externos SHARD_MAP_MANAGER, essa é a distribuição de dados das linhas em tabelas base subjacentes.|0 – Sharded<br /><br /> 1 – replicados<br /><br /> 2 – Round robin|  
|distribution_desc|**nvarchar(120)**|Para tabelas externas em uma fonte de dados externos SHARD_MAP_MANAGER, esse é o tipo de distribuição exibido como uma cadeia de caracteres.||  
|sharding_column_id|**int**|Para tabelas externas em uma fonte de dados externos SHARD_MAP_MANAGER e uma distribuição fragmentada, esta é a ID de coluna da coluna que contém os valores de chave de fragmentação.||  
|remote_schema_name|**sysname**|Para tabelas externas em uma fonte de dados externos SHARD_MAP_MANAGER, este é o esquema em que a tabela base está localizada nos bancos de dados remotos (se for diferente do esquema onde a tabela externa é definida).||  
|remote_object_name|**sysname**|Para tabelas externas em uma fonte de dados externos SHARD_MAP_MANAGER, isso é o nome da tabela base nos bancos de dados remotos (se for diferente do nome da tabela externa).||  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.external_file_formats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
