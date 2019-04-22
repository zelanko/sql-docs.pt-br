---
title: sys.dm_db_page_info (Transact-SQL) | Microsoft Docs
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
author: ''
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2246abe2343622f2aece785a31e1e31f7166822b
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58899712"
---
# <a name="sysdmdbpageinfo-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Retorna informações sobre uma página em um banco de dados.  A função retorna uma linha que contém as informações de cabeçalho da página, incluindo o `object_id`, `index_id`, e `partition_id`.  Essa função substitui a necessidade de usar `DBCC PAGE` na maioria dos casos.

## <a name="syntax"></a>Sintaxe   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>Argumentos  
*DatabaseId* | NULL | DEFAULT     
É a ID do banco de dados. *DatabaseId* está **smallint**. Uma entrada válida é o número de identificação de um banco de dados. O padrão é NULL, no entanto, enviando que um valor NULL para esse parâmetro resultará em erro.
 
*FileId* | NULO | PADRÃO   
É a ID do arquivo. *FileId* está **int**.  Uma entrada válida é o número de identificação de um arquivo no banco de dados especificado por *DatabaseId*. O padrão é NULL, no entanto, enviando que um valor NULL para esse parâmetro resultará em erro.

*PageId* | NULL | DEFAULT   
É a ID da página.  *PageId* está **int**.  Uma entrada válida é o número de identificação de uma página no arquivo especificado por *FileId*. O padrão é NULL, no entanto, enviando que um valor NULL para esse parâmetro resultará em erro.

*modo* | NULO | PADRÃO   
Determina o nível de detalhes na saída da função. 'Limitado' retornará valores NULL para todas as colunas de descrição, 'Detalhada' preencherá as colunas de descrição.  O padrão é 'Limitado'.

## <a name="table-returned"></a>Tabela retornada  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id |INT |ID do banco de dados |
|file_id |INT |ID do Arquivo |
|page_id |INT |ID da página |
|page_type |INT |Tipo de página |
|page_type_desc |nvarchar(64) |Descrição do tipo de página |
|page_flag_bits |nvarchar(64) |Sinalizador de bits no cabeçalho da página |
|page_flag_bits_desc |nvarchar(256) |Descrição do sinalizador bits no cabeçalho da página |
|page_type_flag_bits |nvarchar(64) |Bits de sinalizador de tipo no cabeçalho da página |
|page_type_flag_bits_desc |nvarchar(64) |Descrição de bits de sinalizador de tipo no cabeçalho da página |
|object_id |INT |ID do objeto que possui a página |
|index_id |INT |ID do índice (0 para o heap de páginas de dados) |
|partition_id |BIGINT |ID da partição |
|alloc_unit_id |BIGINT |ID da unidade de alocação |
|page_level |INT |Nível da página no índice (folha = 0) |
|slot_count |SMALLINT |Número total de slots (utilizado e não utilizado) <br> Para uma página de dados, esse número é equivalente ao número de linhas. |
|ghost_rec_count |SMALLINT |Número de registros marcados como "Ghost" na página <br> Um registro fantasma é aquele que foi marcado para exclusão, mas ainda terá de ser removido. |
|torn_bits |INT |1 bit por setor para a detecção de gravações incorretas. Também usado para armazenar a soma de verificação <br> Esse valor é usado para detectar corrupção de dados |
|is_iam_pg |bit |Bit para indicar se a página é uma página IAM  |
|is_mixed_ext |bit |Bit indicar se alocados em uma extensão mista |
|pfs_file_id |SMALLINT |ID do arquivo da página correspondente de PFS |
|pfs_page_id |INT |ID de página correspondente de PFS |
|pfs_alloc_percent |INT |Percentual de alocação, conforme indicado pelo byte PFS |
|pfs_status |nvarchar(64) |PFS |
|pfs_status_desc |nvarchar(64) |Descrição do byte PFS |
|gam_file_id |SMALLINT |ID do arquivo da página GAM correspondente |
|gam_page_id |INT |ID da página da página GAM correspondente |
|gam_status |bit |Bit indicar se alocada em GAM |
|gam_status_desc |nvarchar(64) |Descrição do status bit GAM |
|sgam_file_id |SMALLINT |ID do arquivo da página SGAM correspondente |
|sgam_page_id |INT |ID da página da página SGAM correspondente |
|sgam_status |bit |Bit indicar se alocada no SGAM |
|sgam_status_desc |nvarchar(64) |Descrição do status bit SGAM |
|diff_map_file_id |SMALLINT |ID da página correspondente do bitmap diferencial do arquivo |
|diff_map_page_id |INT |ID da página da página correspondente do bitmap diferencial |
|diff_status |bit |Bit para indicar se o status de comparação é alterado |
|diff_status_desc |nvarchar(64) |Descrição do bit de status de comparação |
|ml_file_id |SMALLINT |ID do arquivo da página correspondente do bitmap de registro em log mínimo |
|ml_page_id |INT |ID da página da página correspondente do bitmap de registro em log mínimo |
|ml_status |bit |Bit para indicar se a página é minimamente registrada |
|ml_status_desc |nvarchar(64) |Descrição do status de registro em log mínimo de bits |
|free_bytes |SMALLINT |Número de bytes livres na página |
|free_data_offset |INT |Deslocamento de espaço livre no final da área de dados |
|reserved_bytes |SMALLINT |Número de bytes livres reservadas por todas as transações (se heap) <br> Número de linhas fantasmas (se o índice de folha) |
|reserved_xdes_id |SMALLINT |Espaço contribuído por m_xdesID para m_reservedCnt <br> Apenas para fins de depuração |
|xdes_id |nvarchar(64) |Transação mais recente da contribuição m_reserved <br> Apenas para fins de depuração |
|prev_page_file_id |SMALLINT |ID do arquivo de página anterior |
|prev_page_page_id |INT |ID de página anterior da página |
|next_page_file_id |SMALLINT |Próxima ID de arquivo de página |
|next_page_page_id |INT |ID da página próxima página |
|min_len |SMALLINT |Comprimento de linhas de tamanho fixo |
|lsn |nvarchar(64) |Número de sequência de log / carimbo de hora |
|header_version |INT |Versão de cabeçalho de página |

## <a name="remarks"></a>Comentários
O `sys.dm_db_page_info` função de gerenciamento dinâmico retorna informações de página semelhantes `page_id`, `file_id`, `index_id`, `object_id` etc. que estão presentes em um cabeçalho de página. Essas informações são úteis para solução de problemas e depuração de vários problemas de desempenho (contenção de bloqueio e trava) e corrupção.

`sys.dm_db_page_info` pode ser usado em vez do `DBCC PAGE` instrução em muitos casos, mas retorna apenas as página informações de cabeçalho, não o corpo da página. `DBCC PAGE` ainda serão necessários para casos de uso em que todo o conteúdo da página é necessário.

## <a name="using-in-conjunction-with-other-dmvs"></a>Usando em conjunto com outros DMVs
Um dos casos de uso importante `sys.dm_db_page_info` é colocá-lo com outros DMVs que expõem informações de página.  Para facilitar esse caso de uso, uma nova coluna chamada `page_resource` tiver sido adicionado, que expõe informações de página em um formato hexadecimal de 8 bytes. Esta coluna foi adicionada à `sys.dm_exec_requests` e `sys.sysprocesses` e será adicionado ao outros DMVs no futuro, conforme necessário.

Uma nova função, `sys.fn_PageResCracker`, leva a `page_resource` como entrada e gera uma única linha que contém `database_id`, `file_id` e `page_id`.  Essa função, em seguida, pode ser usada para facilitar as uniões entre `sys.dm_exec_requests` ou `sys.sysprocesses` e `sys.dm_db_page_info`.

## <a name="permissions"></a>Permissões  
Requer a `VIEW DATABASE STATE` permissão no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. Exibindo todas as propriedades de uma página
A consulta a seguir retorna uma linha com todas as informações de página para um determinado `database_id`, `file_id`, `page_id` combinação com o modo padrão ('limitado')

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdmdbpageinfo-with-other-dmvs"></a>B. Usando sys.dm_db_page_info com outros DMVs 

A consulta a seguir retorna uma linha por `wait_resource` expostos pelo `sys.dm_exec_requests` quando a linha contém um não-nulo `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>Consulte também  
[Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


