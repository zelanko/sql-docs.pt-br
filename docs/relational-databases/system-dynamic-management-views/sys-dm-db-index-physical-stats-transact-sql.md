---
title: sys.dm_db_index_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
caps.latest.revision: 95
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f1c0e78bb475630039b79cd27b8fb433ac8d03a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbindexphysicalstats-transact-sql"></a>sys.dm_db_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações de tamanho e fragmentação dos dados e índices da tabela ou exibição especificada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para um índice, uma linha é retornada para cada nível da árvore B em cada partição. Para um heap, uma linha é retornada para a unidade de alocação de IN_ROW_DATA de cada partição. Para dados LOB (objeto grande), uma linha é retornada para a unidade de alocação de LOB_DATA de cada partição. Se houver dados de estouro de linha na tabela, uma linha será retornada para a unidade de alocação de ROW_OVERFLOW_DATA em cada partição. Retorna informações sobre índices de columnstore otimizado de memória xVelocity.  
  
> [!IMPORTANT]
> Se você consultar **db_index_physical_stats** em uma instância de servidor que está hospedando um sempre no [réplica secundária legível](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), você pode encontrar um impedimento redo. Isso ocorre porque essa exibição de gerenciamento dinâmico adquire um bloqueio IS na exibição ou tabela de usuário especificada, que pode bloquear solicitações por um thread REDO para um bloqueio X na exibição ou tabela de usuário.  
  
 **sys.DM db_index_physical_stats** não retorna informações sobre índices com otimização de memória. Para obter informações sobre o uso de índice com otimização de memória, consulte [sys.DM db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_id* | NULO | 0 | PADRÃO  
 É a ID do banco de dados. *database_id* é **smallint**. As entradas válidas são o número da ID de um banco de dados, NULL, 0 ou DEFAULT. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto.  
  
 Especifique NULL para retornar informações de todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar NULL para *database_id*, você também deverá especificar NULL para *object_id*, *index_id*, e *número_da_partição*.  
  
 A função interna [DB_ID](../../t-sql/functions/db-id-transact-sql.md) pode ser especificado. Quando você usar DB_ID sem especificar um nome de banco de dados, o nível de compatibilidade do banco de dados atual deverá ser 90 ou mais.  
  
 *object_id* | NULO | 0 | PADRÃO  
 É a ID do objeto da tabela ou exibição em que o índice está ativado. *object_id* é **int**.  
  
 As entradas válidas são o número da ID de uma tabela e de uma exibição, NULL, 0 ou DEFAULT. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto. Como de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], as entradas válidas incluem também o nome de fila do agente de serviço ou o nome da tabela interna de fila. Quando os parâmetros padrão são aplicados (ou seja, todos os objetos, todos os índices, etc), informações de fragmentação de todas as filas são incluídos no conjunto de resultados.  
  
 Especifique NULL para retornar informações de todas as tabelas e exibições no banco de dados especificado. Se você especificar NULL para *object_id*, você também deverá especificar NULL para *index_id* e *número_da_partição*.  
  
 *index_id* | 0 | NULO | -1 | PADRÃO  
 É a ID do índice. *index_id* é **int**. As entradas válidas são o número de identificação de um índice, 0 se *object_id* for um heap, NULL, -1 ou DEFAULT. O padrão é -1. NULL, -1 e DEFAULT são valores equivalentes neste contexto.  
  
 Especifique NULL para retornar informações de todos os índices de uma tabela base ou exibição. Se você especificar NULL para *index_id*, você também deverá especificar NULL para *número_da_partição*.  
  
 *número_da_partição* | NULO | 0 | PADRÃO  
 É o número da partição no objeto. *número_da_partição* é **int**. As entradas válidas são o *partion_number* de um índice ou heap, NULL, 0 ou DEFAULT. O padrão é 0. NULL, 0 e DEFAULT são valores equivalentes neste contexto.  
  
 Especifique NULL para retornar informações de todas as partições do objeto proprietário.  
  
 *número_da_partição* tem base 1. Um heap ou índice não particionado tem *número_da_partição* definido como 1.  
  
 *modo* | NULO | PADRÃO  
 É o nome do modo. *modo* Especifica o nível de verificação que é usado para obter estatísticas. *modo* é **sysname**. Entradas válidas são DEFAULT, NULL, LIMITED, SAMPLED ou DETAILED. O padrão (NULL) é LIMITED.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Identificação do banco de dados da tabela ou exibição.|  
|object_id|**Int**|Identificação de objeto da tabela ou exibição na qual o índice se encontra.|  
|index_id|**Int**|Identificação de um índice.<br /><br /> 0 = Heap.|  
|partition_number|**Int**|Número de partição de base 1 no objeto proprietário; uma tabela, exibição ou índice.<br /><br /> 1 = Índice ou heap não particionado.|  
|index_type_desc|**nvarchar(60)**|Descrição do tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED INDEX<br /><br /> NONCLUSTERED INDEX<br /><br /> PRIMARY XML INDEX<br /><br /> SPATIAL INDEX<br /><br /> XML INDEX<br /><br /> ÍNDICE de mapeamento do COLUMNSTORE (interno)<br /><br /> ÍNDICE de DELETEBUFFER COLUMNSTORE (interno)<br /><br /> ÍNDICE de DELETEBITMAP COLUMNSTORE (interno)|  
|hobt_id|**bigint**|Heap ou árvore B a ID do índice ou partição.<br /><br /> Além de retornar o hobt_id de índices definidos pelo usuário, isso também retorna o hobt_id dos índices columnstore interno.|  
|alloc_unit_type_desc|**nvarchar(60)**|Descrição do tipo de unidade de alocação:<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> Unidade de alocação LOB_DATA contém os dados que são armazenados em colunas do tipo **texto**, **ntext**, **imagem**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e **xml**. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).<br /><br /> Unidade de alocação ROW_OVERFLOW_DATA contém os dados que são armazenados em colunas do tipo **varchar**, **nvarchar**, **varbinary**, e **SQL _ variante** que foram empurrados para fora da linha.|  
|index_depth|**tinyint**|Número de níveis de índice.<br /><br /> 1 = Heap ou unidade de alocação LOB_DATA ou ROW_OVERFLOW_DATA.|  
|index_level|**tinyint**|Nível atual do índice.<br /><br /> 0 para níveis folha de índice, heaps e unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA.<br /><br /> Maior que 0 para níveis de índice nonleaf. *index_level* será o mais alto no nível raiz de um índice.<br /><br /> Os níveis não folha dos índices só são processados quando *modo* = DETAILED.|  
|avg_fragmentation_in_percent|**float**|Fragmentação lógica para índices ou fragmentação de extensão para heaps na unidade de alocação IN_ROW_DATA.<br /><br /> O valor é medido como uma porcentagem e leva em consideração vários arquivos. Para definições de fragmentação lógica e de extensão, consulte Comentários.<br /><br /> 0 para unidades de alocação LOB_DATA e ROW_OVERFLOW_DATA.<br /><br /> NULL para heaps quando *modo* = SAMPLED.|  
|fragment_count|**bigint**|Número de fragmentos no nível folha de uma unidade de alocação IN_ROW_DATA. Para obter mais informações sobre fragmentos, consulte Comentários.<br /><br /> NULL para níveis não folha de um índice e unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA.<br /><br /> NULL para heaps quando *modo* = SAMPLED.|  
|avg_fragment_size_in_pages|**float**|Número médio de páginas em um fragmento no nível folha de uma unidade de alocação IN_ROW_DATA.<br /><br /> NULL para níveis não folha de um índice e unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA.<br /><br /> NULL para heaps quando *modo* = SAMPLED.|  
|page_count|**bigint**|Número total de páginas de índice ou dados.<br /><br /> Para um índice, o número total de páginas de índice no nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, o número total de páginas de dados na unidade de alocação IN_ROW_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA, o número total de páginas na unidade de alocação.|  
|avg_page_space_used_in_percent|**float**|Porcentagem média de espaço de armazenamento de dados disponível usada em todas as páginas.<br /><br /> Para um índice, a média se aplica ao nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, a média de todas as páginas de dados na unidade de alocação IN_ROW_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW DATA, a média de todas as páginas na unidade de alocação.<br /><br /> NULL quando *modo* = LIMITED.|  
|record_count|**bigint**|Número total de registros.<br /><br /> Para um índice, o número total de registros se aplica ao nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, o número total de registros na unidade de alocação IN_ROW_DATA.<br /><br /> **Observação:** para um heap, o número de registros retornados por essa função pode não corresponder o número de linhas que são retornados ao executar uma contagem de selecionar (\*) relacionada ao heap. Isso porque uma linha pode conter vários registros. Por exemplo, em algumas situações de atualização, uma única linha de heap pode ter um registro de encaminhamento e um registro encaminhado como resultado de uma operação de atualização. Da mesma forma, a maior parte das linhas de LOB grandes é dividida em vários registros no armazenamento LOB_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA, o número total de registros na unidade de alocação completa.<br /><br /> NULL quando *modo* = LIMITED.|  
|ghost_record_count|**bigint**|Número de registros fantasmas prontos para remoção pela tarefa de limpeza fantasma na unidade de alocação.<br /><br /> 0 para níveis não folha de um índice na unidade de alocação de IN_ROW_DATA.<br /><br /> NULL quando *modo* = LIMITED.|  
|version_ghost_record_count|**bigint**|Número de registros fantasmas retidos por uma transação de isolamento de instantâneo pendente em uma unidade de alocação.<br /><br /> 0 para níveis não folha de um índice na unidade de alocação de IN_ROW_DATA.<br /><br /> NULL quando *modo* = LIMITED.|  
|min_record_size_in_bytes|**Int**|Tamanho de registro mínimo em bytes.<br /><br /> Para um índice, o tamanho de registro mínimo aplica-se ao nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, o tamanho de registro mínimo na unidade de alocação IN_ROW_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA, o tamanho de registro mínimo na unidade de alocação completa.<br /><br /> NULL quando *modo* = LIMITED.|  
|max_record_size_in_bytes|**Int**|Tamanho de registro máximo em bytes.<br /><br /> Para um índice, o tamanho de registro máximo aplica-se ao nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, o tamanho de registro máximo na unidade de alocação IN_ROW_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA, o tamanho de registro máximo na unidade de alocação completa.<br /><br /> NULL quando *modo* = LIMITED.|  
|avg_record_size_in_bytes|**float**|Tamanho de registro médio em bytes.<br /><br /> Para um índice, o tamanho de registro médio aplica-se ao nível atual da árvore b na unidade de alocação IN_ROW_DATA.<br /><br /> Para um heap, o tamanho de registro médio na unidade de alocação IN_ROW_DATA.<br /><br /> Para as unidades de alocação LOB_DATA ou ROW_OVERFLOW_DATA, o tamanho de registro médio na unidade de alocação completa.<br /><br /> NULL quando *modo* = LIMITED.|  
|forwarded_record_count|**bigint**|Número de registros em um heap com ponteiros encaminhados a outro local de dados. (Esse estado ocorre durante uma atualização, quando não há espaço suficiente para armazenar a nova linha no local original.)<br /><br /> NULL para qualquer unidade de alocação diferente das unidades de alocação IN_ROW_DATA de um heap.<br /><br /> NULL para heaps quando *modo* = LIMITED.|  
|compressed_page_count|**bigint**|O número total de páginas compactadas.<br /><br /> Para heaps, as páginas alocadas recentemente não são compactadas com PAGE. Um heap é compactado com PAGE em duas condições especiais: quando os dados são importados em massa ou quando um heap é reconstruído. Operações DML típicas que causam alocações de página não terão compactação PAGE. Reconstrua um heap quando o valor compressed_page_count aumentar ultrapassando o limite desejado.<br /><br /> Para tabelas que têm um índice clusterizado, o valor compressed_page_count indica a eficiência da compactação PAGE.|  
|hobt_id|bigint|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Para apenas índices columnstore, esta é a ID para um conjunto de linhas que controla os dados de columnstore interno para uma partição. Os conjuntos de linhas são armazenadas como dados heaps ou binário árvores. Eles têm a mesma ID de índice que o índice de columnstore pai. Para obter mais informações, consulte [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md).<br /><br /> NULO se|  
|column_store_delete_buffer_state|tinyint|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = DRENAGEM<br /><br /> 3 = LIBERAÇÃO<br /><br /> 4 = DESATIVADO<br /><br /> 5 = PRONTO|  
|column_store_delete_buff_state_desc||**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> NOT_APPLICABLE – o índice pai não é um índice columnstore.<br /><br /> OPEN – Excluidores e scanners usam.<br /><br /> DESCARREGANDO – Excluidores são drenagem mas scanners ainda usarão-lo.<br /><br /> LIBERANDO – buffer é fechado e linhas no buffer estão sendo gravadas para o bitmap de exclusão.<br /><br /> DESATIVAR – linhas no buffer de exclusão fechado foram gravados para o bitmap de exclusão, mas o buffer não foi truncado porque os scanners ainda estão usando. Novo scanners não precisam usar o buffer retiring porque o buffer aberto é suficiente.<br /><br /> PRONTO, que esse buffer de exclusão está pronto para uso.|  
  
## <a name="remarks"></a>Remarks  
 A função de gerenciamento dinâmico sys.dm_db_index_physical_stats substitui a instrução DBCC SHOWCONTIG.  
  
## <a name="scanning-modes"></a>Modos de exame  
 O modo em que a função é executada determina o nível do exame executado para obter os dados estatísticos usados pela função. *modo* é especificado como LIMITED, SAMPLED ou DETAILED. A função atravessa as cadeias de páginas para as unidades de alocação que compõem as partições especificadas da tabela ou índice. sys.DM db_index_physical_stats requer apenas um bloqueio (IS) bloqueio de tabela, independentemente do modo que ele é executado.  
  
 O modo LIMITED é o mais rápido e examina o menor número de páginas. Para um índice, apenas as páginas de nível pai da árvore b (ou seja, aquelas acima do nível folha) são examinadas. Para um heap, as páginas PFS e IAM associadas são examinadas, e as páginas de dados de um heap são examinadas no modo LIMITED.  
  
 Com o modo LIMITED, compressed_page_count é NULL porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] só examina as páginas não folha da árvore B e as páginas IAM e PFS do heap. Use modo SAMPLED para obter um valor estimado de compressed_page_count e use modo DETAILED para obter o valor real de compressed_page_count. O modo SAMPLED retorna estatísticas com base em uma amostra de 1 por cento de todas as páginas no índice ou heap. Os resultados em modo SAMPLED devem ser considerados aproximados. Se o índice ou heap tiver menos que 10.000 páginas, o modo DETAILED será usado em vez do SAMPLED.  
  
 O modo DETAILED examina todas as páginas e retorna todas as estatísticas.  
  
 Os modos são progressivamente mais lentos de LIMITED para DETAILED, porque mais trabalho é executado em cada modo. Para medir rapidamente o tamanho ou o nível de fragmentação de uma tabela ou índice, use o modo LIMITED. Ele é o mais rápido e não retornará uma linha para cada nível não folha na unidade de alocação IN_ROW_DATA do índice.  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>Usando funções de sistema para especificar valores de parâmetro  
 Você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] funções [DB_ID](../../t-sql/functions/db-id-transact-sql.md) e [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) para especificar um valor para o *database_id* e *object_id* parâmetros. No entanto, passar valores que não sejam válidos a essas funções pode causar resultados não intencionais. Por exemplo, se o banco de dados ou nome de objeto não puder ser encontrado por não existir ou por estar escrito incorretamente, ambas as funções retornarão NULL. A função sys.dm_db_index_physical_stats interpreta o NULL como um valor curinga que especifica todos os bancos de dados ou todos os objetos.  
  
 Além disso, a função OBJECT_ID é processada antes da função Sys.DM db_index_physical_stats é chamada e, portanto, é avaliada no contexto do banco de dados atual, não o banco de dados especificado em *database_id*. Esse comportamento pode fazer com que a função OBJECT_ID retorne um valor NULL; ou, se o nome do objeto existir no contexto do banco de dados atual e no banco de dados especificado, uma mensagem de erro poderá ser exibida. Os exemplos seguintes demonstram esses resultados não intencionais.  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>Prática recomendada  
 Sempre verifique se uma ID válida é retornada ao usar DB_ID ou OBJECT_ID. Por exemplo, ao usar OBJECT_ID, especifique um nome de três partes, como `OBJECT_ID(N'AdventureWorks2012.Person.Address')`, ou teste o valor retornado pelas funções antes de usá-los na função Sys.DM db_index_physical_stats. Os exemplos A e B a seguir demonstram um modo seguro de especificar identificações de banco de dados e objeto.  
  
## <a name="detecting-fragmentation"></a>Detectando a fragmentação  
 A fragmentação ocorre por meio dos processos de modificações de dados (instruções INSERT, UPDATE e DELETE) feitas na tabela e, portanto, nos índices definidos na tabela. Como essas modificações não são distribuídas uniformemente entre as linhas da tabela e os índices, o preenchimento de cada página pode variar com o tempo. Para consultas que examinam parte dos índices de uma tabela ou todos eles, esse tipo de fragmentação pode causar leituras de página adicionais. Isso impede o exame paralelo de dados.  
  
 O nível de fragmentação de um índice ou heap é mostrado na coluna avg_fragmentation_in_percent. Para heaps, o valor representa a fragmentação de extensão do heap. Para índices, o valor representa a fragmentação lógica do índice. Ao contrário de DBCC SHOWCONTIG, os algoritmos de cálculo de fragmentação em ambos os casos consideram o armazenamento que se estende por vários arquivos e, por isso, são precisos.  
  
 **Fragmentação lógica**  
  
 É a porcentagem de páginas com problema nas páginas de folha de um índice. Uma página fora de ordem é aquela cuja próxima página física alocada ao índice não é a página apontada pelo ponteiro de próxima págin*a* na página de folha atual.  
  
 **Fragmentação de extensão**  
  
 É a porcentagem de extensões com problema nas páginas de folha de um heap. Uma extensão com problema é aquela para a qual a extensão que contém a página atual de um heap não é fisicamente a próxima extensão depois da extensão que contém a página anterior.  
  
 O valor de avg_fragmentation_in_percent deve ser o mais próximo possível de zero para um máximo desempenho. Porém, valores de 0% a 10% podem ser aceitáveis. Podem ser usados todos os métodos de redução de fragmentação, como reconstruir, reorganizar ou recriar, para reduzir esses valores. Para obter mais informações sobre como analisar o grau de fragmentação em um índice, consulte [reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="reducing-fragmentation-in-an-index"></a>Reduzindo a fragmentação em um índice  
 Quando um índice estiver fragmentado de forma que a fragmentação afete o desempenho da consulta, há três opções para reduzir a fragmentação:  
  
-   Descartar e recriar o índice clusterizado.  
  
     Recriar um índice clusterizado redistribui os dados e resulta em páginas de dados completas. O nível de preenchimento pode ser configurado usando a opção FILLFACTOR em CREATE INDEX. As desvantagens desse método são que o índice permanece offline durante o ciclo de descarte e recriação e que a operação é atômica. Se a criação de índice for suspensa, o índice não será recriado. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
-   Usar ALTER INDEX REORGANIZE, a substituição de DBCC INDEXDEFRAG, para reordenar as páginas de nível folha do índice em uma ordem lógica. Como essa operação é online, o índice permanecerá disponível enquanto a instrução estiver sendo executada. A operação também pode ser interrompida sem perda do trabalho já concluído. A desvantagem desse método é que ele não reorganiza muito bem os dados como uma operação de reconstrução de índice e não atualiza as estatísticas.  
  
-   Usar ALTER INDEX REBUILD, a substituição de DBCC DBREINDEX, para reconstruir o índice online ou offline. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
 A fragmentação sozinha não é uma razão suficiente para reorganizar ou reconstruir um índice. O efeito principal da fragmentação é que ela reduz a velocidade da taxa de transferência read-ahead da página durante os exames de índice. O resultado é tempos de resposta mais lentos. Se a carga de trabalho da consulta em uma tabela ou índice fragmentado não envolver exames porque a carga de trabalho é composta por pesquisas singleton, a remoção da fragmentação poderá não ter efeito algum. Para obter mais informações, consulte [site da Microsoft](http://go.microsoft.com/fwlink/?linkid=31012).  
  
> [!NOTE]  
>  Executar DBCC SHRINKFILE ou DBCC SHRINKDATABASE poderá apresentar fragmentação se um índice for movido parcial ou completamente durante a operação de redução. Assim, se for necessário executar uma operação de redução, você deverá fazer isso antes da remoção da fragmentação.  
  
## <a name="reducing-fragmentation-in-a-heap"></a>Reduzindo fragmentação em um heap  
 Para reduzir a extensão da fragmentação de um heap, crie um índice clusterizado na tabela e descarte o índice. Isso redistribui os dados enquanto o índice clusterizado é criado. E também otimiza o máximo possível esse processo, enquanto considera a distribuição de espaço livre disponível no banco de dados. Quando o índice clusterizado é descartado para a recriação de um heap, os dados não são movidos e permanecem no mesmo lugar. Para obter informações sobre como executar essas operações, consulte [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) e [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md).  
  
> [!CAUTION]  
>  Criar e descartar um índice clusterizado em uma tabela recria todos os índices não clusterizados nessa tabela duas vezes.  
  
## <a name="compacting-large-object-data"></a>Compactando dados de objetos grandes  
 Por padrão, a instrução ALTER INDEX REORGANIZE compacta páginas que contêm dados LOB (objetos grandes). Como as páginas LOB não são desalocadas quando vazias, a compactação desses dados poderá melhorar o espaço em disco se vários dados LOB tiverem sido excluídos ou se uma coluna LOB foi descartada.  
  
 Reorganizar um índice clusterizado especificado compacta todas as colunas LOB contidas no índice clusterizado. Reorganizar um índice não clusterizado compacta todas as colunas LOB não-chave (incluídas) no índice. Quando ALL é especificado na instrução, todos os índices associados à tabela ou exibição especificada são reorganizados. Além disso, todas as colunas LOB associadas ao índice clusterizado, tabela subjacente ou índice não clusterizado com colunas incluídas são compactadas.  
  
## <a name="evaluating-disk-space-use"></a>Avaliando o uso do espaço em disco  
 A coluna avg_page_space_used_in_percent indica que a página está cheia. Para se obter um ótimo uso do espaço em disco, esse valor deverá estar perto de 100% para um índice que não terá muitas inserções aleatórias. Entretanto, um índice que tem muitas inserções aleatórias e páginas muito cheias terá um número maior de divisões de página. Isso causa mais fragmentação. Por isso, para reduzir as divisões de página, o valor deve ser menor que 100%. A recriação de um índice com a opção FILLFACTOR especificada permite que o preenchimento da página seja alterado para atender ao padrão de consulta do índice. Para obter mais informações sobre o fator de preenchimento, consulte [especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md). Além disso, ALTER INDEX REORGANIZE compactará um índice tentando preencher páginas para o FILLFACTOR especificado pela última vez. Isso aumenta o valor em avg_space_used_in_percent. Observe que ALTER INDEX REORGANIZE não pode reduzir o preenchimento da página. Em vez disso, o índice deverá ser recriado.  
  
## <a name="evaluating-index-fragments"></a>Avaliando fragmentos de índice  
 Um fragmento é composto de páginas de folha fisicamente consecutivas no mesmo arquivo de uma unidade de alocação. Um índice tem pelo menos um fragmento. O máximo de fragmentos que um índice pode ter é igual ao número de páginas no nível folha do índice. Fragmentos maiores indicam que menos E/S de disco é necessária para ler o mesmo número de páginas. Por isso, quanto maior o valor avg_fragment_size_in_pages, melhor o desempenho de exame de intervalo. Os valores avg_fragment_size_in_pages e avg_fragmentation_in_percent são inversamente proporcionais entre si. Por isso, a reconstrução ou a reorganização de um índice deve reduzir a quantidade de fragmentação e aumentar o tamanho do fragmento.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não retorna dados para índices columnstore clusterizados.  
  
## <a name="permissions"></a>Permissões  
 Requer as seguintes permissões:  
  
-   Permissão CONTROL no objeto especificado no banco de dados.  
  
-   Permissão VIEW DATABASE STATE para retornar informações sobre todos os objetos de banco de dados especificado, usando o curinga de objeto @*object_id*= NULL.  
  
-   Permissão VIEW SERVER STATE para retornar informações sobre todos os bancos de dados, usando o curinga de banco de dados @*database_id* = NULL.  
  
 Conceder VIEW DATABASE STATE permite que todos os objetos no banco de dados sejam retornados, independentemente de qualquer permissão CONTROL negada a objetos específicos.  
  
 Negar VIEW DATABASE STATE impede que todos os objetos do banco de dados sejam retornados, independentemente de qualquer permissão CONTROL concedida a objetos específicos. Além disso, quando o curinga de banco de dados @*database_id*= NULL for especificado, o banco de dados é omitido.  
  
 Para obter mais informações, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. Retornando informações sobre uma tabela especificada  
 O exemplo a seguir retorna as estatísticas de tamanho e fragmentação de todos os índices e partições da tabela `Person.Address`. O modo de exame é definido como `'LIMITED'` para oferecer melhor desempenho e limitar as estatísticas retornadas. A execução dessa consulta requer, no mínimo, a permissão CONTROL na tabela `Person.Address`.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
  
IF @db_id IS NULL  
BEGIN;  
    PRINT N'Invalid database';  
END;  
ELSE IF @object_id IS NULL  
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. Retornando informações sobre um heap  
 O exemplo a seguir retorna todas as estatísticas do heap `dbo.DatabaseLog` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Como a tabela contém dados LOB, uma linha é retornada para a unidade de alocação `LOB_DATA`, além da linha retornada para `IN_ROW_ALLOCATION_UNIT` que está armazenando as páginas de dados do heap. A execução dessa consulta requer, no mínimo, a permissão CONTROL na tabela `dbo.DatabaseLog`.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. Retornando informações de todos os bancos de dados  
 O exemplo a seguir retorna todas as estatísticas de todas as tabelas e índices na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] através da especificação do curinga `NULL` para todos os parâmetros. A execução desta consulta requer a permissão VIEW SERVER STATE.  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdmdbindexphysicalstats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. Usando sys.dm_db_index_physical_stats em um script para reconstruir ou reorganizar índices  
 O exemplo a seguir reorganiza ou reconstrói automaticamente em um banco de dados todas as partições que têm uma fragmentação média de 10%. A execução desta consulta requer a permissão VIEW DATABASE STATE. Este exemplo especifica `DB_ID` como o primeiro parâmetro sem especificar um nome de banco de dados. Um erro será gerado se o banco de dados atual tiver um nível de compatibilidade de 80 ou menos. Para resolver o erro, substitua `DB_ID()` por um nome de banco de dados válido. Para obter mais informações sobre níveis de compatibilidade do banco de dados, consulte [nível de compatibilidade do banco de dados ALTER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdmdbindexphysicalstats-to-show-the-number-of-page-compressed-pages"></a>E. Usando sys.dm_db_index_physical_stats para mostrar o número de páginas compactadas por página  
 O exemplo seguinte mostra como exibir e comparar o número total de páginas em relação às páginas que são compactadas por linha e página. Estas informações podem ser usadas para determinar o benefício que a compactação está fornecendo para um índice ou tabela.  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdmdbindexphysicalstats-in-sampled-mode"></a>F. Usando sys.dm_db_index_physical_stats em modo SAMPLED  
 O exemplo a seguir mostra como o modo SAMPLED retorna um aproximado que é diferente dos resultados do modo DETAILED.  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. Consultando filas do service broker para a fragmentação de índice  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Os exemplos a seguir mostra como consultar filas de agente do servidor de fragmentação.  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

