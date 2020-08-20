---
description: sys.dm_db_page_info (Transact-SQL)
title: sys. dm_db_page_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 60df2ed8bf279bf7da8193282768124815aa6ab3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493689"
---
# <a name="sysdm_db_page_info-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Retorna informações sobre uma página em um banco de dados.  A função retorna uma linha que contém as informações de cabeçalho da página, incluindo `object_id` , `index_id` e `partition_id` .  Essa função substitui a necessidade de usar `DBCC PAGE` na maioria dos casos.

> [!NOTE]
> `sys.dm_db_page_info` no momento, há suporte apenas no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e posterior.


## <a name="syntax"></a>Sintaxe   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>Argumentos  
*DatabaseID* | NULL | OS     
É a ID do banco de dados. *DatabaseID* é **smallint**. A entrada válida é o número de identificação de um banco de dados. O padrão é NULL, mas o envio de um valor nulo para esse parâmetro resultará em um erro.
 
*FileID* | NULL | OS   
É a ID do arquivo. A *FileID* é **int**.  A entrada válida é o número de identificação de um arquivo no banco de dados especificado por *DatabaseID*. O padrão é NULL, mas o envio de um valor nulo para esse parâmetro resultará em um erro.

*PageId* | NULL | OS   
É a ID da página.  *PageId* é **int**.  A entrada válida é o número de identificação de uma página no arquivo especificado por *FileID*. O padrão é NULL, mas o envio de um valor nulo para esse parâmetro resultará em um erro.

*Modo* | NULL | OS   
Determina o nível de detalhes na saída da função. ' LIMITED ' retornará valores nulos para todas as colunas de descrição, ' DETAILED ' preencherá as colunas de descrição.  O padrão é ' LIMITED '.

## <a name="table-returned"></a>Tabela retornada  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id |INT |ID do banco de dados |
|file_id |INT |ID do Arquivo |
|page_id |INT |ID da página |
|page_header_version |INT |Versão do cabeçalho da página |
|page_type |INT |Tipo de página |
|page_type_desc |nvarchar (64) |Descrição do tipo de página |
|page_type_flag_bits |nvarchar (64) |Bits de sinalizador de tipo no cabeçalho da página |
|page_type_flag_bits_desc |nvarchar (64) |Descrição de bits do sinalizador de tipo no cabeçalho da página |
|page_flag_bits |nvarchar (64) |Sinalizar bits no cabeçalho da página |
|page_flag_bits_desc |nvarchar(256) |Sinalizar descrição de bits no cabeçalho da página |
|page_lsn |nvarchar (64) |Número de sequência de log/carimbo de data/hora |
|page_level |INT |Nível da página no índice (folha = 0) |
|object_id |INT |ID do objeto que possui a página |
|index_id |INT |ID do índice (0 para páginas de dados de heap) |
|partition_id |BIGINT |ID da partição |
|alloc_unit_id |BIGINT |ID da unidade de alocação |
|is_encrypted |bit |Bit para indicar se a página está criptografada ou não |
|has_checksum |bit |Bit para indicar se a página tem um valor de soma de verificação |
|soma de verificação |INT |Armazena o valor da soma de verificação usado para detectar dados corrompidos |
|is_iam_pg |bit |Bit para indicar se a página é uma página IAM  |
|is_mixed_ext |bit |Bit para indicar se alocado em uma extensão mista |
|has_ghost_records |bit |Bit para indicar se a página contém registros fantasmas <br> Um registro fantasma é aquele que foi marcado para exclusão, mas ainda precisa ser removido.|
|has_version_records |bit |Bit para indicar se a página contém registros de versão usados para [recuperação de banco de dados acelerada](../backup-restore/restore-and-recovery-overview-sql-server.md#adr) |
|pfs_page_id |INT |ID de página da página PFS correspondente |
|pfs_is_allocated |bit |Bit para indicar se a página está marcada como alocada na página PFS correspondente |
|pfs_alloc_percent |INT |Porcentagem de alocação conforme indicado pelo byte do PFS correspondente |
|pfs_status |nvarchar (64) |Byte PFS |
|pfs_status_desc |nvarchar (64) |Descrição do byte PFS |
|gam_page_id |INT |ID de página da página GAM correspondente |
|gam_status |bit |Bit para indicar se alocado em GAM |
|gam_status_desc |nvarchar (64) |Descrição do bit de status GAM |
|sgam_page_id |INT |ID de página da página SGAM correspondente |
|sgam_status |bit |Bit para indicar se alocado em SGAM |
|sgam_status_desc |nvarchar (64) |Descrição do bit de status SGAM |
|diff_map_page_id |INT |ID da página da página de bitmap diferencial correspondente |
|diff_status |bit |Bit para indicar se o status de comparação foi alterado |
|diff_status_desc |nvarchar (64) |Descrição do bit de status de comparação |
|ml_map_page_id |INT |ID da página da página de bitmap de log mínima correspondente |
|ml_status |bit |Bit para indicar se a página é minimamente registrada |
|ml_status_desc |nvarchar (64) |Descrição do bit de status de log mínimo |
|prev_page_file_id |SMALLINT |ID do arquivo de paginação anterior |
|prev_page_page_id |INT |ID da página da página anterior |
|next_page_file_id |SMALLINT |ID do arquivo da próxima página |
|next_page_page_id |INT |ID da página da próxima página |
|fixed_length |SMALLINT |Comprimento de linhas de tamanho fixo |
|slot_count |SMALLINT |Número total de slots (usados e não utilizados) <br> Para uma página de dados, esse número é equivalente ao número de linhas. |
|ghost_rec_count |SMALLINT |Número de registros marcados como fantasma na página <br> Um registro fantasma é aquele que foi marcado para exclusão, mas ainda precisa ser removido. |
|free_bytes |SMALLINT |Número de bytes livres na página |
|free_data_offset |INT |Deslocamento de espaço livre no final da área de dados |
|reserved_bytes |SMALLINT |Número de bytes livres reservados por todas as transações (se heap) <br> Número de linhas fantasmas (se folha de índice) |
|reserved_bytes_by_xdes_id |SMALLINT |Espaço contribuído pelo m_xdesID para m_reservedCnt <br> Somente para fins de depuração |
|xdes_id |nvarchar (64) |Última transação contribuída por m_reserved <br> Somente para fins de depuração |
||||

## <a name="remarks"></a>Comentários
A `sys.dm_db_page_info` função de gerenciamento dinâmico retorna informações de página como `page_id` , `file_id` , `index_id` , `object_id` etc. que estão presentes em um cabeçalho de página. Essas informações são úteis para solucionar problemas e depurar vários desempenhos (contenção de bloqueio e trava) e problemas de corrupção.

`sys.dm_db_page_info` pode ser usado no lugar da `DBCC PAGE` instrução em muitos casos, mas retorna apenas as informações de cabeçalho da página, não o corpo da página. `DBCC PAGE` ainda serão necessários para casos de uso em que todo o conteúdo da página for necessário.

## <a name="using-in-conjunction-with-other-dmvs"></a>Usando em conjunto com outras DMVs
Um dos casos de uso importantes do `sys.dm_db_page_info` é associá-lo a outras DMVs que expõem informações da página.  Para facilitar esse caso de uso, uma nova coluna chamada foi `page_resource` adicionada, o que expõe as informações da página em um formato hex de 8 bytes. Esta coluna foi adicionada a `sys.dm_exec_requests` e `sys.sysprocesses` e será adicionada a outras DMVs no futuro, conforme necessário.

Uma nova função, `sys.fn_PageResCracker` ,, usa o `page_resource` como entrada e gera uma única linha que contém `database_id` , `file_id` e `page_id` .  Essa função pode ser usada para facilitar junções entre `sys.dm_exec_requests` ou `sys.sysprocesses` e `sys.dm_db_page_info` .

## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` permissão no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>a. Exibindo todas as propriedades de uma página
A consulta a seguir retorna uma linha com todas as informações de página de uma determinada `database_id` `file_id` `page_id` combinação com o modo padrão (' Limited ')

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdm_db_page_info-with-other-dmvs"></a>B. Usando sys. dm_db_page_info com outros DMVs 

A consulta a seguir retorna uma linha por `wait_resource` exposição `sys.dm_exec_requests` quando a linha contém um não nulo `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>Consulte Também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


