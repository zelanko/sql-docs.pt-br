---
title: sys.dm_repl_schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2aa0b4e885d586e64c6c613e07d2969d77885715
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763374"
---
# <a name="sysdmreplschemas-transact-sql"></a>sys.dm_repl_schemas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre colunas de tabela publicadas por replicação.  
  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary(8)**|Endereço na memória da estrutura de esquema em cache para o artigo de tabela publicado.|  
|**tabid**|**bigint**|ID da tabela replicada.|  
|**indexid**|**smallint**|ID de um índice clusterizado na tabela publicada.|  
|**idSch**|**bigint**|ID do esquema da tabela.|  
|**tabschema**|**nvarchar(510)**|Nome do esquema da tabela.|  
|**ccTabschema**|**smallint**|Comprimento de caracteres do esquema da tabela.|  
|**tabname**|**nvarchar(510)**|Nome da tabela publicada.|  
|**ccTabname**|**smallint**|Comprimento de caracteres do nome da tabela publicado.|  
|**rowsetid_delete**|**bigint**|ID da linha excluída.|  
|**rowsetid_insert**|**bigint**|ID da linha inserida.|  
|**num_pk_cols**|**int**|Número de colunas de chave primária.|  
|**pcitee**|**binary(8000)**|Pointeiro para a estrutura de expressão de consulta usada para avaliar uma coluna computada.|  
|**re_numtextcols**|**int**|Número de colunas de objeto binário grande na tabela replicada.|  
|**re_schema_lsn_begin**|**binary(8000)**|Número de sequência de log inicial (LSN) de logon da versão do esquema.|  
|**re_schema_lsn_end**|**binary(8000)**|LSN final de logon na versão do esquema.|  
|**re_numcols**|**int**|Número de colunas publicadas.|  
|**re_colid**|**int**|Identificador de coluna no Publicador.|  
|**re_awcName**|**nvarchar(510)**|Nome da coluna publicada.|  
|**re_ccName**|**smallint**|Número de caracteres no nome da coluna.|  
|**re_pk**|**tinyint**|Se a coluna publicada faz parte de uma chave primária ou não.|  
|**re_unique**|**tinyint**|Se a coluna publicada faz parte de um índice exclusivo ou não.|  
|**re_maxlen**|**smallint**|Comprimento máximo da coluna publicada.|  
|**re_prec**|**tinyint**|Precisão da coluna publicada.|  
|**re_scale**|**tinyint**|Escala da coluna publicada.|  
|**re_collatid**|**bigint**|ID de intercalação da coluna publicada.|  
|**re_xvtype**|**smallint**|Tipo da coluna publicada.|  
|**re_offset**|**smallint**|Deslocamento da coluna publicada.|  
|**re_bitpos**|**tinyint**|Posição de bit da coluna publicada, no vetor de byte.|  
|**re_fNullable**|**tinyint**|Especifica se a coluna publicada suporta valores NULL.|  
|**re_fAnsiTrim**|**tinyint**|Especifica se a exclusão ANSI é usada na coluna publicada.|  
|**re_computed**|**smallint**|Especifica se a coluna publicada é uma coluna computada.|  
|**se_rowsetid**|**bigint**|ID do conjunto de linhas.|  
|**se_schema_lsn_begin**|**binary(8000)**|LSN inicial de logon na versão do esquema.|  
|**se_schema_lsn_end**|**binary(8000)**|LSN final de logon na versão do esquema.|  
|**se_numcols**|**int**|Número de colunas.|  
|**se_colid**|**int**|ID da coluna no assinante.|  
|**se_maxlen**|**smallint**|Comprimento máximo da coluna.|  
|**se_prec**|**tinyint**|Precisão da coluna.|  
|**se_scale**|**tinyint**|Escala da coluna.|  
|**se_collatid**|**bigint**|ID de agrupamento da coluna.|  
|**se_xvtype**|**smallint**|Tipo da coluna.|  
|**se_offset**|**smallint**|Deslocamento da coluna.|  
|**se_bitpos**|**tinyint**|Posição de bit da coluna, no vetor de byte.|  
|**se_fNullable**|**tinyint**|Especifica se a coluna suporta valores NULL.|  
|**se_fAnsiTrim**|**tinyint**|Especifica se o fragmento ANSI é usado na coluna.|  
|**se_computed**|**smallint**|Especifica se a coluna é uma coluna computada.|  
|**se_nullBitInLeafRows**|**int**|Especifica se o valor da coluna é NULL.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão de VIEW DATABASE STATE no banco de dados de publicação para chamar **dm_repl_schemas**.  
  
## <a name="remarks"></a>Comentários  
 As informações só serão retornadas para objetos de banco de dados replicados atualmente armazenados no cache de artigo de replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à replicação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

