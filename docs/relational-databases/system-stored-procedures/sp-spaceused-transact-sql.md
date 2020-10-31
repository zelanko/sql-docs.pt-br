---
description: sp_spaceused (Transact-SQL)
title: sp_spaceused (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f2e03e32842a9187761c0f4471d871277682005
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067508"
---
# <a name="sp_spaceused-transact-sql"></a>sp_spaceused (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Exibe o número de linhas, o espaço em disco reservado e o espaço em disco usado por uma tabela, exibição indexada ou fila [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados atual ou exibe o espaço em disco reservado e usado pelo banco de dados inteiro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>Argumentos  

Para [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] , `sp_spaceused` deve especificar parâmetros nomeados (por exemplo `sp_spaceused (@objname= N'Table1');` , em vez de depender da posição ordinal dos parâmetros. 

`[ @objname = ] 'objname'`
   
 É o nome qualificado ou não qualificado da tabela, da exibição indexada ou da fila para a qual as informações de uso do espaço são solicitadas. As aspas são obrigatórias apenas se um nome de objeto qualificado for especificado. Se um nome de objeto totalmente qualificado (incluindo um nome de banco de dados) for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual.  
Se *objname* não for especificado, os resultados serão retornados para todo o banco de dados.  
*objname* é **nvarchar (776)** , com um padrão de NULL.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] oferecem suporte apenas a objetos de banco de dados e de tabela.
  
`[ @updateusage = ] 'updateusage'` Indica que o DBCC UPDATEUSAGE deve ser executado para atualizar as informações de uso do espaço. Quando *objname* não for especificado, a instrução será executada no banco de dados inteiro; caso contrário, a instrução será executada em *objname* . Os valores podem ser **true** ou **false** . o *UPDATEUSAGE* é **varchar (5)** , com um padrão de **false** .  
  
`[ @mode = ] 'mode'` Indica o escopo dos resultados. Para uma tabela ou banco de dados ampliado, o parâmetro *Mode* permite que você inclua ou exclua a parte remota do objeto. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 O argumento de *modo* pode ter os seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ALL|Retorna as estatísticas de armazenamento do objeto ou banco de dados, incluindo a parte local e a parte remota.|  
|LOCAL_ONLY|Retorna as estatísticas de armazenamento apenas da parte local do objeto ou do banco de dados. Se o objeto ou banco de dados não estiver habilitado para Stretch, o retornará as mesmas estatísticas de quando @mode = All.|  
|REMOTE_ONLY|Retorna as estatísticas de armazenamento apenas da parte remota do objeto ou banco de dados. Essa opção gera um erro quando uma das seguintes condições é verdadeira:<br /><br /> A tabela não está habilitada para ampliação.<br /><br /> A tabela está habilitada para ampliação, mas você nunca habilitou a migração de dados. Nesse caso, a tabela remota ainda não tem um esquema.<br /><br /> O usuário removeu manualmente a tabela remota.<br /><br /> O provisionamento do arquivo de dados remotos retornou um status de êxito, mas, na verdade, falhou.|  
  
 o *modo* é **varchar (11)** , com um padrão de **n' all' '** .  
  
`[ @oneresultset = ] oneresultset` Indica se um único conjunto de resultados deve ser retornado. O argumento *oneresultset* pode ter os seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Quando *\@ objname* é nulo ou não é especificado, dois conjuntos de resultados são retornados. Dois conjuntos de resultados são o comportamento padrão.|  
|1|Quando *\@ objname* = NULL ou não for especificado, um único conjunto de resultados será retornado.|  
  
 *oneresultset* é **bit** , com um padrão de **0** .  

`[ @include_total_xtp_storage] 'include_total_xtp_storage'`
**Aplica-se a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] , [!INCLUDE[sssds-md](../../includes/sssds-md.md)] .  
  
 Quando @oneresultset = 1, o parâmetro @include_total_xtp_storage determina se o único ResultSet inclui colunas para MEMORY_OPTIMIZED_DATA armazenamento. O valor padrão é 0, ou seja, por padrão (se o parâmetro for omitido), as colunas XTP não serão incluídas no ResultSet.  

## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *objname* for omitido e o valor de *oneresultset* for 0, os seguintes conjuntos de resultados serão retornados para fornecer informações de tamanho do banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar (18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de dados e de log.|  
|**espaço não alocado**|**varchar (18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**reservado**|**varchar (18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar (18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar (18)**|Total de espaço usado por índices.|  
|**Não utilizado**|**varchar (18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|  
  
 Se *objname* for omitido e o valor de *oneresultset* for 1, o único conjunto de resultados a seguir será retornado para fornecer informações de tamanho do banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar (18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de dados e de log.|  
|**espaço não alocado**|**varchar (18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados.|  
|**reservado**|**varchar (18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar (18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar (18)**|Total de espaço usado por índices.|  
|**Não utilizado**|**varchar (18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|  
  
 Se *objname* for especificado, o seguinte conjunto de resultados será retornado para o objeto especificado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Nome do objeto para o qual foram solicitadas informações de uso do espaço.<br /><br /> O nome de esquema do objeto não é retornado. Se o nome do esquema for necessário, use as exibições de gerenciamento dinâmico [Sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) ou [Sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) para obter informações de tamanho equivalentes.|  
|**rows**|**Char (20)**|Número de linhas existentes na tabela. Se o objeto especificado for uma fila [!INCLUDE[ssSB](../../includes/sssb-md.md)], essa coluna indicará o número de mensagens na fila.|  
|**reservado**|**varchar (18)**|Quantidade total de espaço reservado para *objname* .|  
|**data**|**varchar (18)**|Quantidade total de espaço usada pelos dados em *objname* .|  
|**index_size**|**varchar (18)**|Quantidade total de espaço usada pelos índices em *objname* .|  
|**Não utilizado**|**varchar (18)**|Quantidade total de espaço reservado para *objname* , mas que ainda não foi usado.|  
 
Esse é o modo padrão, quando nenhum parâmetro é especificado. Os seguintes conjuntos de resultados são retornados detalhando as informações de tamanho do banco de dados em disco. 

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar (18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de dados e de log. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso incluirá o tamanho total em disco de todos os arquivos de ponto de verificação no grupo de arquivos.|  
|**espaço não alocado**|**varchar (18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso incluirá o tamanho total em disco dos arquivos de ponto de verificação com o estado precriado no grupo de arquivos.|  

Espaço usado pelas tabelas no banco de dados: (este ResultSet não reflete as tabelas com otimização de memória, pois não há nenhuma contabilidade por tabela de uso do disco) 

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**reservado**|**varchar (18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar (18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar (18)**|Total de espaço usado por índices.|  
|**Não utilizado**|**varchar (18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|

O seguinte conjunto de resultados será retornado **somente se** o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA com pelo menos um contêiner: 

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com o estado precriado, em KB. Conta em direção ao espaço não alocado no banco de dados como um todo. [Por exemplo, se houver 600.000 KB de arquivos de ponto de verificação criados, essa coluna conterá ' 600000 KB ']|  
|**xtp_used**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com Estados em construção, ativo e destino de MESCLAgem, em KB. Esse é o espaço em disco usado ativamente para dados em tabelas com otimização de memória.|  
|**xtp_pending_truncation**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com estado WAITING_FOR_LOG_TRUNCATION, em KB. Esse é o espaço em disco usado para arquivos de ponto de verificação que estão aguardando limpeza, quando ocorre um truncamento de log.|

Se *objname* for omitido, o valor de oneresultset será 1 e *include_total_xtp_storage* será 1, o único conjunto de resultados a seguir será retornado para fornecer informações de tamanho do banco de dados atual. Se `include_total_xtp_storage` for 0 (o padrão), as três últimas colunas serão omitidas. 

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar (18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de dados e de log. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso incluirá o tamanho total em disco de todos os arquivos de ponto de verificação no grupo de arquivos.|
|**espaço não alocado**|**varchar (18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso incluirá o tamanho total em disco dos arquivos de ponto de verificação com o estado precriado no grupo de arquivos.|  
|**reservado**|**varchar (18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar (18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar (18)**|Total de espaço usado por índices.|  
|**Não utilizado**|**varchar (18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|
|**xtp_precreated**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com o estado precriado, em KB. Isso conta em direção ao espaço não alocado no banco de dados como um todo. Retornará NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data com pelo menos um contêiner. *Esta coluna só será incluída se @include_total_xtp_storage = 1* .| 
|**xtp_used**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com Estados em construção, ativo e destino de MESCLAgem, em KB. Esse é o espaço em disco usado ativamente para dados em tabelas com otimização de memória. Retornará NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data com pelo menos um contêiner. *Esta coluna só será incluída se @include_total_xtp_storage = 1* .| 
|**xtp_pending_truncation**|**varchar (18)**|Tamanho total dos arquivos de ponto de verificação com estado WAITING_FOR_LOG_TRUNCATION, em KB. Esse é o espaço em disco usado para arquivos de ponto de verificação que estão aguardando limpeza, quando ocorre um truncamento de log. Retornará NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data com pelo menos um contêiner. Esta coluna só será incluída se `@include_total_xtp_storage=1` .|

## <a name="remarks"></a>Comentários  
 **database_size** geralmente é maior do que a soma do espaço **reservado** não  +  **alocado** porque inclui o tamanho dos arquivos de log, mas **reservado** e **unallocated_space** considerar apenas as páginas de dados. Em alguns casos com o Azure Synapse Analytics, essa instrução pode não ser verdadeira. 
  
 As páginas usadas por índices XML e índices de texto completo são incluídas em **index_size** para ambos os conjuntos de resultados. Quando *objname* é especificado, as páginas dos índices XML e dos índices de texto completo do objeto também são contadas nos resultados totais **reservados** e **index_size** .  
  
 Se o uso de espaço for calculado para um banco de dados ou um objeto que tenha um índice espacial, as colunas de tamanho de espaço, como **database_size** , **reservadas** e **index_size** , incluem o tamanho do índice espacial.  
  
 Quando o *UPDATEUSAGE* é especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina as páginas de dados no banco de dado e faz as correções necessárias nas exibições do catálogo **Sys.allocation_units** e **Sys. partitions** sobre o espaço de armazenamento usado por cada tabela. Há algumas situações, por exemplo, depois de um índice ser descartado, em que as informações de espaço da tabela talvez não sejam atuais. o *UPDATEUSAGE* pode levar algum tempo para ser executado em grandes tabelas ou bancos de dados. Use o *UPDATEUSAGE* somente quando você suspeitar de que valores incorretos estão sendo retornados e quando o processo não terá um efeito adverso em outros usuários ou processos no banco de dados. Se preferir, DBCC UPDATEUSAGE pode ser executado separadamente.  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Portanto, os valores retornados por **sp_spaceused** imediatamente após descartar ou truncar um objeto grande podem não refletir o espaço em disco real disponível.  
  
## <a name="permissions"></a>Permissões  
 A permissão para executar **sp_spaceused** é concedida à função **public** . Somente os membros da função de banco de dados fixa **db_owner** podem especificar o parâmetro **\@updateusage** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>a. Exibindo informações de espaço em disco sobre uma tabela  
 O exemplo a seguir relata informações de espaço em disco para a tabela `Vendor` e seus índices.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>B. Exibindo informações atualizadas de espaço sobre um banco de dados  
 O exemplo a seguir resume o espaço usado no banco de dados atual e usa o parâmetro `@updateusage` opcional para assegurar que os valores corretos sejam retornados.  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. Exibindo informações de uso de espaço sobre a tabela remota associada a uma tabela habilitada para Stretch  
 O exemplo a seguir resume o espaço usado pela tabela remota associada a uma tabela habilitada para Stretch usando o argumento **\@ Mode** para especificar o destino remoto. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. Exibindo informações de uso de espaço para um banco de dados em um único conjunto de resultados  
 O exemplo a seguir resume o uso de espaço para o banco de dados atual em um único conjunto de resultados.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memory_optimized-file-group-in-a-single-result-set"></a>E. Exibindo informações de uso de espaço para um banco de dados com pelo menos um MEMORY_OPTIMIZED grupo de arquivos em um único conjunto de resultados 
 O exemplo a seguir resume o uso de espaço para o banco de dados atual com pelo menos um MEMORY_OPTIMIZED grupo de arquivos em um único conjunto de resultados.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memory_optimized-table-object-in-a-database"></a>F. Exibindo informações de uso de espaço para um objeto de tabela MEMORY_OPTIMIZED em um banco de dados.
 O exemplo a seguir resume o uso de espaço para um objeto de tabela MEMORY_OPTIMIZED no banco de dados atual com pelo menos um grupo de arquivos MEMORY_OPTIMIZED.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused
@objname = N'VehicleTemparatures',
@updateusage = 'FALSE',
@mode = 'ALL',
@oneresultset = '0',
@include_total_xtp_storage = '1';
GO
```  

## <a name="see-also"></a>Consulte Também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [&#41;DBCC UPDATEUSAGE &#40;Transact-SQL ](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
