---
title: sp_spaceused (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
caps.latest.revision: 62
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6dc2878c9a913b5bb95ef32c9f00a6e7b1e94520
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43089379"
---
# <a name="spspaceused-transact-sql"></a>sp_spaceused (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Exibe o número de linhas, o espaço em disco reservado e o espaço em disco usado por uma tabela, exibição indexada ou fila [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados atual ou exibe o espaço em disco reservado e usado pelo banco de dados inteiro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>Argumentos  

Para [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)], `sp_spaceused` deve especificar os parâmetros nomeados (por exemplo `sp_spaceused (@objname= N'Table1');` em vez de depender da posição ordinal de parâmetros. 

 [  **@objname=**] **'***objname***'** 
   
 É o nome qualificado ou não qualificado da tabela, da exibição indexada ou da fila para a qual as informações de uso do espaço são solicitadas. As aspas são obrigatórias apenas se um nome de objeto qualificado for especificado. Se um nome de objeto totalmente qualificado (incluindo um nome de banco de dados) for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual.  
Se *objname* não for especificado, os resultados são retornados para o banco de dados inteiro.  
*objname* está **nvarchar(776)**, com um padrão NULL.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] só há suporte para objetos de banco de dados e tabela.
  
 [  **@updateusage=**] **'***updateusage***'**  
 Indica que DBCC UPDATEUSAGE deve ser executado para atualizar as informações de uso do espaço. Quando *objname* não é especificado, a instrução é executada no banco de dados inteiro; caso contrário, a instrução é executada no *objname*. Os valores podem ser **verdadeira** ou **falso**. *UPDATEUSAGE* está **varchar(5)**, com um padrão de **false**.  
  
 [  **@mode=**] **'***modo***'**  
 Indica o escopo dos resultados. Para uma tabela ampliada ou banco de dados, o *modo* parâmetro permite que você inclua ou exclua a parte remota do objeto. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 O *modo* argumento pode ter os seguintes valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|ALL|Retorna as estatísticas de armazenamento do objeto ou banco de dados incluindo a parte local e a parte remota.|  
|LOCAL_ONLY|Retorna as estatísticas de armazenamento somente a parte local do objeto ou banco de dados. Se o objeto ou o banco de dados não estiver habilitada para Stretch, retorna as mesmas estatísticas, como quando @mode = ALL.|  
|REMOTE_ONLY|Retorna as estatísticas de armazenamento do somente a parte remota do banco de dados ou objeto. Essa opção gera um erro quando uma das seguintes condições for verdadeira:<br /><br /> A tabela não está habilitada para ampliação.<br /><br /> A tabela está habilitada para ampliação, mas você nunca habilitou a migração de dados. Nesse caso, a tabela remota ainda não tem um esquema.<br /><br /> O usuário caiu manualmente a tabela remota.<br /><br /> O provisionamento de arquivo de dados remoto retornou um status de êxito, mas na verdade ele falhou.|  
  
 *modo* está **varchar(11)**, com um padrão de **n' '**.  
  
 [  **@oneresultset=**] *oneresultset*  
 Indica se deve retornar um único conjunto de resultados. O *oneresultset* argumento pode ter os seguintes valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|0|Quando *@objname* é nulo ou não é especificado, os dois conjuntos de resultados são retornados. Dois conjuntos de resultados é o comportamento padrão.|  
|1|Quando *@objname* = null ou não é especificado, um único conjunto de resultados será retornado.|  
  
 *oneresultset* está **bit**, com um padrão de **0**.  

[ **@include_total_xtp_storage**] **'***include_total_xtp_storage***'**  
**Aplica-se a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)].  
  
 Quando @oneresultset= 1, o parâmetro @include_total_xtp_storage determina se o conjunto de resultados único inclui colunas para o armazenamento MEMORY_OPTIMIZED_DATA. O valor padrão é 0, ou seja, por padrão (se o parâmetro é omitido) as colunas XTP não são incluídas no conjunto de resultados.  

## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *objname* for omitido e o valor de *oneresultset* for 0, os seguintes conjuntos de resultados são retornados para fornecer informações de tamanho de banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar(18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de log e de dados.|  
|**espaço não alocado**|**varchar(18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar(18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar(18)**|Total de espaço usado por índices.|  
|**não utilizado**|**varchar(18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|  
  
 Se *objname* for omitido e o valor de *oneresultset* é 1, o seguinte conjunto de resultados único é retornado para fornecer informações de tamanho de banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar(18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de log e de dados.|  
|**espaço não alocado**|**varchar(18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados.|  
|**reserved**|**varchar(18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar(18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar(18)**|Total de espaço usado por índices.|  
|**não utilizado**|**varchar(18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|  
  
 Se *objname* for especificado, o seguinte conjunto de resultados será retornado para o objeto especificado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Nome do objeto para o qual foram solicitadas informações de uso do espaço.<br /><br /> O nome de esquema do objeto não é retornado. Se o nome do esquema for necessário, use o [DM db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) ou [db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) exibições de gerenciamento dinâmico para obter informações sobre o tamanho equivalente.|  
|**rows**|**char(20)**|Número de linhas existentes na tabela. Se o objeto especificado for uma fila [!INCLUDE[ssSB](../../includes/sssb-md.md)], essa coluna indicará o número de mensagens na fila.|  
|**reserved**|**varchar(18)**|Quantidade total de espaço reservado para *objname*.|  
|**data**|**varchar(18)**|Quantidade total de espaço usado pelos dados no *objname*.|  
|**index_size**|**varchar(18)**|Quantidade total de espaço usado pelos índices *objname*.|  
|**não utilizado**|**varchar(18)**|Quantidade total de espaço reservado para *objname* , mas ainda não usado.|  
 
Isso é o modo padrão, quando nenhum parâmetro for especificado. Os seguintes conjuntos de resultados são retornados detalhando informações de tamanho do banco de dados em disco. 

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar(18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de log e de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso inclui o tamanho em disco total de todos os arquivos de ponto de verificação no grupo de arquivos.|  
|**espaço não alocado**|**varchar(18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso inclui o tamanho em disco total dos arquivos de ponto de verificação com o estado PRECREATED no grupo de arquivos.|  

Espaço usado por tabelas no banco de dados: (este conjunto de resultados não reflete a tabelas com otimização de memória, pois não há nenhuma estatística por tabela de uso do disco) 

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar(18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar(18)**|Total de espaço usado por índices.|  
|**não utilizado**|**varchar(18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|

O seguinte conjunto de resultados é retornado **só se** o banco de dados tem um grupo de arquivos MEMORY_OPTIMIZED_DATA pelo menos um contêiner: 

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com o estado PRECREATED, em KB. Contagens até o espaço não alocado no banco de dados como um todo. [Por exemplo, se houver 600.000 KB de arquivos de ponto de verificação pré-criados, esta coluna contém 600000 ' KB']|  
|**xtp_used**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com os estados de em construção, o ativo e o destino de mesclagem, em KB. Isso é o espaço em disco usado ativamente para dados em tabelas com otimização de memória.|  
|**xtp_pending_truncation**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com o estado WAITING_FOR_LOG_TRUNCATION, em KB. Isso é o espaço em disco usado para arquivos de ponto de verificação que aguardam limpeza, depois que o truncamento de log acontece.|

Se *objname* é omitido, o valor de oneresultset é 1, e *include_total_xtp_storage* é 1, o seguinte conjunto de resultados único é retornado para fornecer informações de tamanho de banco de dados atual. Se `include_total_xtp_storage` for 0 (o padrão), as três últimas colunas são omitidas. 

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome do banco de dados atual.|  
|**database_size**|**varchar(18)**|Tamanho do banco de dados atual em megabytes. **database_size** inclui arquivos de log e de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso inclui o tamanho em disco total de todos os arquivos de ponto de verificação no grupo de arquivos.|
|**espaço não alocado**|**varchar(18)**|Espaço no banco de dados que não foi reservado para objetos de banco de dados. Se o banco de dados tiver um grupo de arquivos MEMORY_OPTIMIZED_DATA, isso inclui o tamanho em disco total dos arquivos de ponto de verificação com o estado PRECREATED no grupo de arquivos.|  
|**reserved**|**varchar(18)**|Total de espaço alocado por objetos no banco de dados.|  
|**data**|**varchar(18)**|Total de espaço usado por dados.|  
|**index_size**|**varchar(18)**|Total de espaço usado por índices.|  
|**não utilizado**|**varchar(18)**|Total de espaço reservado para objetos no banco de dados, mas ainda não usado.|
|**xtp_precreated**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com o estado PRECREATED, em KB. Essa conta para o espaço não alocado no banco de dados como um todo. Retorna NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data pelo menos um contêiner. *Essa coluna só estará incluído se @include_total_xtp_storage= 1*.| 
|**xtp_used**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com os estados de em construção, o ativo e o destino de mesclagem, em KB. Isso é o espaço em disco usado ativamente para dados em tabelas com otimização de memória. Retorna NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data pelo menos um contêiner. *Essa coluna só estará incluído se @include_total_xtp_storage= 1*.| 
|**xtp_pending_truncation**|**varchar(18)**|Tamanho total dos arquivos de ponto de verificação com o estado WAITING_FOR_LOG_TRUNCATION, em KB. Isso é o espaço em disco usado para arquivos de ponto de verificação que aguardam limpeza, depois que o truncamento de log acontece. Retorna NULL se o banco de dados não tiver um grupo de arquivos memory_optimized_data pelo menos um contêiner. Essa coluna só estará incluído se `@include_total_xtp_storage=1`.|

## <a name="remarks"></a>Remarks  
 **database_size** sempre seja maior que a soma dos **reservada** + **espaço não alocado** porque ele inclui o tamanho dos arquivos de log, mas **reservado**e **unallocated_space** considere apenas as páginas de dados.  
  
 Páginas que são usadas por índices XML e índices de texto completo são incluídas no **index_size** para ambos os conjuntos de resultados. Quando *objname* for especificado, as páginas para os índices XML e índices de texto completo para o objeto também são contadas no total **reservado** e **index_size** resultados.  
  
 Se o uso do espaço é calculado para um banco de dados ou um objeto que tem um índice espacial, as colunas de tamanho de espaço, como **database_size**, **reservado**, e **index_size**, incluir o tamanho do índice espacial.  
  
 Quando *updateusage* for especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina os dados de páginas no banco de dados e fará as correções necessárias na **allocation_units** e **sys. Partitions** exibições em relação ao espaço de armazenamento usada por cada tabela do catálogo. Há algumas situações, por exemplo, depois de um índice ser descartado, em que as informações de espaço da tabela talvez não sejam atuais. *UPDATEUSAGE* pode levar algum tempo para ser executado em grandes tabelas ou bancos de dados. Use *updateusage* somente quando você suspeitar que valores incorretos estão sendo retornados e quando o processo não terá um efeito adverso em outros usuários ou processos no banco de dados. Se preferir, DBCC UPDATEUSAGE pode ser executado separadamente.  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Portanto, os valores retornados pelo **sp_spaceused** imediatamente depois de descartar ou truncar um objeto grande pode não refletir o espaço em disco real disponível.  
  
## <a name="permissions"></a>Permissões  
 A permissão para executar **sp_spaceused** é concedida à função **public** . Somente os membros da função de banco de dados fixa **db_owner** podem especificar o parâmetro **@updateusage** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>A. Exibindo informações de espaço em disco sobre uma tabela  
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
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. Exibir informações de uso de espaço sobre a tabela remota associado a uma tabela habilitada para Stretch  
 O exemplo a seguir resume o espaço usado pela tabela de remota associada a uma tabela habilitada para Stretch usando o **@mode** argumento para especificar o destino remoto. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. Exibindo informações de uso de espaço para um banco de dados em um único resultado definido  
 O exemplo a seguir resume o uso de espaço para o banco de dados atual em um único conjunto de resultados.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>E. Exibindo informações de uso de espaço para um banco de dados pelo menos um grupo de arquivos MEMORY_OPTIMIZED em um único conjunto de resultados 
 O exemplo a seguir resume o uso de espaço para o banco de dados atual com pelo menos um grupo de arquivos MEMORY_OPTIMIZED em um único conjunto de resultados.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>F. Exibindo informações de uso de espaço para um objeto de tabela MEMORY_OPTIMIZED em um banco de dados.
 O exemplo a seguir resume o uso de espaço para um objeto de tabela MEMORY_OPTIMIZED no banco de dados atual pelo menos um grupo de arquivos MEMORY_OPTIMIZED.
 
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

## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
