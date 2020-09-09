---
description: sys.dm_os_volume_stats (Transact-SQL)
title: sys. dm_os_volume_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_volume_stats_TSQL
- dm_os_volume_stats
- sys.dm_os_volume_stats
- sys.dm_os_volume_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_volume_stats dynamic management function
ms.assetid: fa1c58ad-8487-42ad-956c-983f2229025f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d6e6eb3ccf2823af437fc37cdddfa2b0b640ae12
ms.sourcegitcommit: 71a334c5120a1bc3809d7657294fe44f6c909282
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89614603"
---
# <a name="sysdm_os_volume_stats-transact-sql"></a>sys.dm_os_volume_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-2008R2SP1-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-2008R2sp1-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o volume do sistema operacional (diretório) no qual os bancos de dados especificados e arquivos são armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use essa função de gerenciamento dinâmico para verificar os atributos da unidade de disco físico ou retornar informações de espaço livre disponível sobre o diretório.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_os_volume_stats (database_id, file_id)  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argumentos  
 *database_id*  
 ID do banco de dados. *database_id* é **int**, sem padrão. Não pode ser NULL.  
  
 *file_id*  
 ID do arquivo. *file_id* é **int**, sem padrão. Não pode ser NULL.  
  
## <a name="table-returned"></a>Tabela retornada  
  
||||  
|-|-|-|  
|**Coluna**|**Data type**|**Descrição**|  
|**database_id**|**int**|ID do banco de dados. Não pode ser nulo.|  
|**file_id**|**int**|ID do arquivo. Não pode ser nulo.|  
|**volume_mount_point**|**nvarchar(512)**|Ponto de montagem no qual o volume está na raiz. Pode retornar uma cadeia de caracteres vazia. Retorna NULL no sistema operacional Linux.|  
|**volume_id**|**nvarchar(512)**|ID de volume do sistema operacional. Pode retornar uma cadeia de caracteres vazia. Retorna NULL no sistema operacional Linux.|  
|**logical_volume_name**|**nvarchar(512)**|Nome lógico do volume. Pode retornar uma cadeia de caracteres vazia. Retorna NULL no sistema operacional Linux.|  
|**file_system_type**|**nvarchar(512)**|Tipo de volume de sistema de arquivo (por exemplo, NTFS, FAT, RAW). Pode retornar uma cadeia de caracteres vazia. Retorna NULL no sistema operacional Linux.|  
|**total_bytes**|**bigint**|Tamanho total em bytes do volume. Não pode ser nulo.|  
|**available_bytes**|**bigint**|Espaço em disco disponível no volume. Não pode ser nulo.|  
|**supports_compression**|**tinyint**|Indica se o volume dá suporte a compressão do sistema operacional. Não pode ser nulo no Windows e retorna NULL no sistema operacional Linux.|  
|**supports_alternate_streams**|**tinyint**|Indica se o volume dá suporte a fluxos alternativos. Não pode ser nulo no Windows e retorna NULL no sistema operacional Linux.|  
|**supports_sparse_files**|**tinyint**|Indica se o volume dá suporte a arquivos esparsos.  Não pode ser nulo no Windows e retorna NULL no sistema operacional Linux.|  
|**is_read_only**|**tinyint**|Indica se o volume está marcado como somente leitura no momento. Não pode ser nulo.|  
|**is_compressed**|**tinyint**|Indica se esse volume está compactado no momento. Não pode ser nulo no Windows e retorna NULL no sistema operacional Linux.|  
|**incurs_seek_penalty**|**tinyint**|Indica o tipo de armazenamento que dá suporte a esse volume. Os valores possíveis são:<br /><br />0: nenhuma penalidade de busca neste volume, normalmente quando o dispositivo de armazenamento é PMM ou SSD<br /><br />1: busca de penalidade neste volume, normalmente quando o dispositivo de armazenamento é HDD<br /><br />2: o tipo de armazenamento não pode ser determinado quando o volume está em um caminho UNC ou em compartilhamentos montados<br /><br />NULL: o tipo de armazenamento não pode ser determinado no sistema operacional Linux<br /><br />**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] )|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-total-space-and-available-space-for-all-database-files"></a>a. Retornar espaço total e disponível para todos os arquivos de banco de dados  
 O exemplo a seguir retorna o espaço total e disponível (em bytes) para todos os arquivos de banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT f.database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.master_files AS f  
CROSS APPLY sys.dm_os_volume_stats(f.database_id, f.file_id);  
```  
  
### <a name="b-return-total-space-and-available-space-for-the-current-database"></a>B. Retornar espaço total e disponível para o banco de dados atual  
 O exemplo a seguir retorna o espaço total e disponível (em bytes) para os arquivos de banco de dados no banco de dados atual.  
  
```sql  
SELECT database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.database_files AS f  
CROSS APPLY sys.dm_os_volume_stats(DB_ID(f.name), f.file_id);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
