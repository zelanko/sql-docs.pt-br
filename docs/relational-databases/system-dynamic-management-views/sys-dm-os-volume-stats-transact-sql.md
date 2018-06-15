---
title: sys.DM os_volume_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5fcc94554408ed68988ddbdf34422078ca31dd4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34468302"
---
# <a name="sysdmosvolumestats-transact-sql"></a>sys.dm_os_volume_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o volume do sistema operacional (diretório) no qual os bancos de dados especificados e arquivos são armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use essa função de gerenciamento dinâmico para verificar os atributos da unidade de disco físico ou retornar informações de espaço livre disponível sobre o diretório.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_os_volume_stats (database_id, file_id)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *database_id*  
 ID do banco de dados. *database_id* é **int**, sem padrão. Não pode ser NULL.  
  
 *file_id*  
 ID do arquivo. *file_id* é **int**, sem padrão. Não pode ser NULL.  
  
## <a name="table-returned"></a>Tabela retornada  
  
||||  
|-|-|-|  
|**Coluna**|**Tipo de dados**|**Descrição**|  
|**database_id**|**Int**|ID do banco de dados. Não pode ser nulo.|  
|**file_id**|**Int**|ID do arquivo. Não pode ser nulo.|  
|**volume_mount_point**|**nvarchar(512)**|Ponto de montagem no qual o volume está na raiz. Pode retornar uma cadeia de caracteres vazia.|  
|**volume_id**|**nvarchar(512)**|ID de volume do sistema operacional. Pode retornar uma cadeia de caracteres vazia|  
|**logical_volume_name**|**nvarchar(512)**|Nome lógico do volume. Pode retornar uma cadeia de caracteres vazia|  
|**file_system_type**|**nvarchar(512)**|Tipo de volume de sistema de arquivo (por exemplo, NTFS, FAT, RAW). Pode retornar uma cadeia de caracteres vazia|  
|**total_bytes**|**bigint**|Tamanho total em bytes do volume. Não pode ser nulo.|  
|**available_bytes**|**bigint**|Espaço em disco disponível no volume. Não pode ser nulo.|  
|**supports_compression**|**bit**|Indica se o volume dá suporte a compressão do sistema operacional. Não pode ser nulo.|  
|**supports_alternate_streams**|**bit**|Indica se o volume dá suporte a fluxos alternativos. Não pode ser nulo.|  
|**supports_sparse_files**|**bit**|Indica se o volume dá suporte a arquivos esparsos.  Não pode ser nulo.|  
|**is_read_only**|**bit**|Indica se o volume está marcado como somente leitura no momento. Não pode ser nulo.|  
|**is_compressed**|**bit**|Indica se esse volume está compactado no momento. Não pode ser nulo.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-total-space-and-available-space-for-all-database-files"></a>A. Retornar espaço total e disponível para todos os arquivos de banco de dados  
 O exemplo a seguir retorna o espaço total e disponível (em bytes) para todos os arquivos de banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT f.database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.master_files AS f  
CROSS APPLY sys.dm_os_volume_stats(f.database_id, f.file_id);  
```  
  
### <a name="b-return-total-space-and-available-space-for-the-current-database"></a>B. Retornar espaço total e disponível para o banco de dados atual  
 O exemplo a seguir retorna o espaço total e disponível (em bytes) para os arquivos de banco de dados no banco de dados atual.  
  
```  
SELECT database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.database_files AS f  
CROSS APPLY sys.dm_os_volume_stats(DB_ID(f.name), f.file_id);  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
