---
title: ALTER INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- t-sql
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
- index rebuild [SQL Server]
- index reorganize [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6492f067d05a3606c5304e473162c8eabdcee5f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845704"
---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Modifica uma tabela ou índice de exibição existente (relacional ou XML) desabilitando, recriando ou reorganizando o índice, ou definindo opções no índice.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse 
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>Argumentos  
 *index_name*  
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela ou exibição, mas não precisam ser exclusivos no banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ALL  
 Especifica todos os índices associados à tabela ou exibição, independentemente do tipo de índice. Especificar ALL fará com que a instrução falhe se um ou mais índices estiverem em um grupo de arquivos offline ou somente leitura, ou se a operação especificada não for permitida em um ou mais tipos de índice. A tabela a seguir lista as operações de índice e os tipos de índice não permitidos.  
  
|Usando a palavra-chave ALL com esta operação|Falhará se a tabela tiver um ou mais|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice Columnstore: **aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|REBUILD PARTITION = *partition_number*|Índice não particionado, índice XML, índice espacial ou índice desabilitado|  
|REORGANIZE|Índices com ALLOW_PAGE_LOCKS definido como OFF|  
|REORGANIZE PARTITION = *partition_number*|Índice não particionado, índice XML, índice espacial ou índice desabilitado|  
|IGNORE_DUP_KEY = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice Columnstore: **aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice Columnstore: **aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
|RESUMABLE = ON  | Índices retomáveis não são compatíveis com a palavra-chave **All**. <br /><br /> **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] |   
  
> [!WARNING]
>  Para obter mais informações sobre operações de índice que podem ser executadas online, consulte [Diretrizes para operações de índice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

 Se ALL for especificado com PARTITION = *partition_number*, todos os índices deverão ser alinhados. Isso significa que eles serão particionados com base nas funções de partições equivalentes. Usar ALL com PARTITION faz com que todas as partições de índice com o mesmo *partition_number* sejam recriadas ou reorganizadas. Para obter mais informações sobre índices particionados, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or_view_name*  
 É o nome da tabela ou exibição associada ao índice. Para exibir um relatório dos índices em um objeto, use a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] é compatível ao formato de nome de três partes database_name.[schema_name].table_or_view_name quando database_name é o banco de dados atual ou database_name é tempdb e table_or_view_name começa com #.  
  
 REBUILD [ WITH **(**\<rebuild_index_option> [ **,**... *n*]**)** ]  
 Especifica que o índice será recriado usando as mesmas colunas, tipo de índice, atributo de exclusividade e ordem de classificação. Essa cláusula é equivalente a [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md). REBUILD habilita um índice desabilitado. A recriação de um índice clusterizado não recriará os índices não clusterizados associados, a menos que a palavra-chave ALL seja especificada. Se as opções de índice não forem especificadas, os valores de opção de índice existentes armazenados em [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) serão aplicados. Para qualquer opção de índice cujo valor não seja armazenado em **sys.indexes**, o padrão indicado na definição de argumento da opção será aplicado.  
  
 Se ALL for especificado e a tabela subjacente for um heap, a operação de recriação não terá efeito na tabela. Quaisquer índices não clusterizados associados à tabela serão recriados.  
  
 A operação de recriação poderá ser registrada minimamente se o modelo de recuperação de banco de dados for definido como bulk-logged ou simples.  
  
> [!NOTE]
>  Ao recriar um índice XML primário, a tabela de usuário subjacente não estará disponível durante a operação de índice.  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Para índices columnstore, a operação de recompilação:  
  
1.  não usa a ordem de classificação.  
  
2.  Obtenha um bloqueio exclusivo na tabela ou na partição durante a recompilação.  Os dados estão "offline" e indisponíveis durante a recompilação, mesmo se você usar NOLOCK, RCSI ou SI.  
  
3.  Compacta novamente todos os dados do columnstore. Há duas cópias do índice columnstore durante a recompilação. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui o índice columnstore original.  
  
 Para obter mais informações sobre como recompilar índices columnstore, consulte [Índices Columnstore – desfragmentação](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica que somente uma partição de um índice será recriada ou reorganizada. PARTITION não poderá ser especificado se *index_name* não for um índice particionado.  
  
 PARTITION = ALL recria todas as partições.  
  
> [!WARNING]
> É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações. É recomendável usar índices alinhados apenas quando o número de partições for maior que 1.000.  
  
 *partition_number*  
   
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 É o número de partição de um índice particionado que será reconstruído ou reorganizado. *partition_number* é uma expressão de constante que pode fazer referência a variáveis. Isso inclui variáveis de tipo definido pelo usuário ou funções e funções definidas pelo usuário, mas não é possível fazer referência a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. *partition_number* deve existir ou a instrução falhará.  
  
 WITH **(**\<single_partition_rebuild_index_option>**)**  
   
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 SORT_IN_TEMPDB, MAXDOP e DATA_COMPRESSION são as opções que podem ser especificadas ao recriar uma única partição (PARTITION = *n*). Índices XML não podem ser especificados em uma única operação de recriação de partição.  
  
 DISABLE  
 Marca o índice como desabilitado e indisponível para uso pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Qualquer índice pode ser desabilitado. A definição de um índice desabilitado permanece no catálogo do sistema sem nenhum dado de índice subjacente. Desabilitar um índice clusterizado evita que o usuário acesse os dados da tabela subjacente. Para habilitar um índice, use ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING. Para obter mais informações, consulte [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md) e [Habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
 REORGANIZE um índice rowstore  
 Para índices rowstore, REORGANIZE especifica reorganizar o nível folha do índice. A operação de REORGANIZE é:  
  
-   sempre executada online. Isso significa que os bloqueios de tabela de longo prazo não são mantidos e que as consultas ou atualizações da tabela subjacente podem continuar durante a transação ALTER INDEX REORGANIZE.  
-   Não é permitida para um índice desabilitado  
-   Não é permitida quando ALLOW_PAGE_LOCKS está definido como OFF  
-   Não é revertida quando é executada em uma transação e a transação é revertida.  
  
REORGANIZE WITH **(** LOB_COMPACTION = { **ON** | OFF } **)**  
 Aplica-se a índices rowstore.  
  
LOB_COMPACTION = ON  
  
-   Especifica compactar todas as páginas que contêm dados destes tipos de dados de objeto grande (LOB): image, text, ntext, varchar(max), nvarchar(max), varbinary(max) e xml. A compactação desses dados pode reduzir o tamanho dos dados no disco.  
  
-   Para um índice clusterizado, isso compacta todas as colunas LOB contidas na tabela.  
  
-   Reorganizar um índice não clusterizado, compacta todas as colunas LOB não chave (incluídas) no índice.  
  
-   REORGANIZE ALL executa LOB_COMPACTION em todos os índices. Para cada índice, isso compacta todas as colunas LOB no índice clusterizado, na tabela subjacente ou nas colunas incluídas em um índice não clusterizado.  
  
LOB_COMPACTION = OFF  
  
-   Páginas que contêm dados de objeto grande não são compactadas.  
  
-   OFF não tem nenhum efeito em um heap.  
  
 REORGANIZE um índice columnstore  
 Para índices columnstore, REORGANIZE compacta cada rowgroup delta CLOSED no columnstore como um rowgroup compactado. A operação REORGANIZE sempre é executada online. Isso significa que os bloqueios de tabela de longo prazo não são mantidos e que as consultas ou atualizações da tabela subjacente podem continuar durante a transação ALTER INDEX REORGANIZE. 
  
-   REORGANIZE não é necessário para mover rowgroups delta CLOSED para rowgroups compactados. O processo TM (motor de tupla) em segundo plano é ativado periodicamente para compactar rowgroups delta CLOSED. É recomendável usar REORGANIZE quando o motor de tupla está ficando para trás. REORGANIZE pode compactar rowgroups de maneira mais agressiva.  
  
-   Para compactar todos os rowgroups OPEN e CLOSED, veja a opção REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS) nesta seção.  
  
Para índices columnstore em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2016) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], REORGANIZE executa as seguintes otimizações adicionais desfragmentação online:  
  
-   Remove fisicamente linhas de um grupo de linhas quando 10% ou mais linhas foram excluídas logicamente. Os bytes excluídos são recuperados na mídia física. Por exemplo, se um grupo de linhas compactado de 1 milhão de linhas tiver 100 mil linhas excluídas, o SQL Server removerá as linhas excluídas e recompactará o rowgroup com 900 mil linhas. Ele salva no armazenamento removendo as linhas excluídas.  
  
-   Combina um ou mais rowgroups compactados para aumentar linhas por rowgroup até o máximo de 1.024.576 linhas. Por exemplo, se você importar em massa cinco lotes de 102.400 linhas, obterá cinco rowgroups compactados. Se você executar REORGANIZE, esses rowgroups serão mesclados em um grupo de linhas compactado de 512 mil linhas de tamanho. Isso pressupõe que não havia nenhuma limitação de tamanho ou memória de dicionário.  
  
-   Para rowgroups em que 10% ou mais linhas foram excluídas logicamente, o SQL Server tenta combinar esse grupo de linhas com um ou mais rowgroups. Por exemplo, o rowgroup 1 é compactado com 500 mil linhas e o rowgroup 21 é compactado com o máximo de 1.048.576 linhas.  O rowgroup 21 tem 60% das linhas excluídas, o que deixa 409.830 linhas. O SQL Server favorece combinar esses dois rowgroups para compactar um novo rowgroup com 909.830 linhas.  
  
REORGANIZE WITH ( COMPRESS_ALL_ROW_GROUPS = { ON | **OFF** } )  

 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

COMPRESS_ALL_ROW_GROUPS fornece uma maneira de forçar os rowgroups delta OPEN ou CLOSED para o columnstore. Com essa opção, não é necessário recompilar o índice columnstore para esvaziar os rowgroups delta.  Isso, combinado a outros recursos de desfragmentação de remover e mesclar, faz com que não seja mais necessário recompilar o índice na maioria das situações.    

-   ON força todos os rowgroups para a columnstore, não importa o tamanho e o estado (CLOSED ou OPEN).  
  
-   OFF força todos os rowgroups CLOSED para o columnstore.  
  
SET **(** \<set_index option> [ **,**... *n*] **)**  
 Especifica opções de índice sem recriar ou reorganizar o índice. SET não pode ser especificado para um índice desabilitado.  
  
PAD_INDEX = { ON | OFF }  
   
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 A porcentagem de espaço livre especificada por FILLFACTOR é aplicada às páginas de nível intermediário do índice. Se FILLFACTOR não for especificado ao mesmo tempo em que PAD_INDEX é definido como ON, o valor do fator de preenchimento armazenado em [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) será usado.  
  
 OFF ou *fillfactor* não está especificado  
 As páginas do nível intermediário são preenchidas até próximo à capacidade máxima. Isso deixa espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, com base no conjunto de chaves das páginas intermediárias.  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
FILLFACTOR = *fillfactor*  
 
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Especifica uma porcentagem que indica quanto [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0. Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.  
  
 Uma configuração FILLFACTOR explícita é usada somente quando o índice é criado pela primeira vez ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 Para exibir a configuração do fator de preenchimento, use **sys.indexes**.  
  
> [!IMPORTANT]
> A criação ou alteração de um índice clusterizado com um valor FILLFACTOR afeta a quantidade de espaço de armazenamento que os dados ocupam, pois o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.  
  
 SORT_IN_TEMPDB = { ON | **OFF** }  
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica se os resultados de classificação devem ser armazenados em **tempdb**. O padrão é OFF.  
  
 ON  
 Os resultados de classificação intermediários usados para criar o índice são armazenados no **tempdb**. Se **tempdb** estiver em um conjunto de discos diferente do banco de dados do usuário, isso poderá reduzir o tempo necessário para criar um índice. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 Se uma operação de classificação não for necessária, ou se a classificação puder ser executada na memória, a opção SORT_IN_TEMPDB será ignorada.  
  
 Para obter mais informações, consulte a [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY **=** { ON | OFF }  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. O padrão é OFF.  
  
 ON  
 Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.  
  
 OFF  
 Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.  
  
 IGNORE_DUP_KEY não pode ser definido como ON para índices criados em uma exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.  
  
 Para exibir IGNORE_DUP_KEY, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Na sintaxe compatível com versões anteriores, WITH IGNORE_DUP_KEY é equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE **=** { ON | OFF }  
 Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ON  
 As estatísticas desatualizadas não são recalculadas automaticamente.  
  
 OFF  
 A atualização automática de estatísticas está habilitada.  
  
 Para restaurar a atualização automática de estatísticas, defina STATISTICS_NORECOMPUTE como OFF ou execute UPDATE STATISTICS sem a cláusula NORECOMPUTE.  
  
> [!IMPORTANT]
> Desabilitar o recálculo automático de estatísticas de distribuição pode impedir que o otimizador de consulta selecione os planos de execução ideais para consultas que envolvem a tabela.  
  
 STATISTICS_INCREMENTAL = { ON | **OFF** }  
 Quando estiver **ON**, as estatísticas serão criadas conforme as estatísticas de partição. Quando estiver **OFF**, a árvore de estatísticas será removida e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] calculará as estatísticas novamente. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, a opção será ignorada e um aviso será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
-   Estatísticas criadas em bancos de dados somente leitura.  
-   Estatísticas criadas em índices filtrados.  
-   Estatísticas criadas em exibições.  
-   Estatísticas criadas em tabelas internas.  
-   Estatísticas criadas com índices espaciais ou índices XML.  
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ONLINE **=** { ON | **OFF** } \<conforme se aplica a rebuild_index_option>  
 Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF.  
  
 Para um índice XML ou índice espacial, só há suporte para ONLINE = OFF e, se ONLINE for definido como ON, um erro será gerado.  
  
> [!NOTE]
>  As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos compatíveis com as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos compatíveis com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) e [Edições e os recursos compatíveis com SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Isso permite que as consultas ou atualizações na tabela e nos índices subjacentes continuem. No início da operação, um bloqueio S (Compartilhado) é mantido brevemente no objeto de origem. Ao término da operação, por um breve momento, um bloqueio S será mantido na origem se um índice não clusterizado estiver sendo criado; ou um bloqueio SCH-M (Modificação de Esquema) será adquirido quando um índice clusterizado for criado ou descartado online, ou quando um índice clusterizado ou não clusterizado estiver sendo recriado. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local.  
  
 OFF  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Uma operação de índice offline que cria, recria ou descarta um índice clusterizado, espacial ou XML, ou que recria ou descarta um índice não clusterizado, adquire um bloqueio Sch-M na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT.  
  
 Para obter mais informações, consulte [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Índices, inclusive aqueles em tabelas temporárias globais, podem ser recriados online com as seguintes exceções:  
  
-   índices XML  
  
-   Índices em tabelas temporárias locais  
  
-   Um subconjunto de um índice particionado (é possível recriar online um índice particionado inteiro.)  

-  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] anterior à V12 e do SQL Server anterior à [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], não permita a opção `ONLINE` para compilação de índice clusterizado nem operações de recompilação quando a tabela base contiver colunas **varchar(max)** ou **varbinary(max)**.

RESUMABLE **=** { ON | **OFF**}

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 Especifica se uma operação de índice online é retomável.

 ON A operação do índice é retomável.

 OFF A operação do índice não é retomável.

MAX_DURATION **=** *time* [**MINUTES**] usado com **RESUMABLE = ON** (requer **ONLINE = ON**).
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Indica o tempo (um valor inteiro especificado em minutos) pelo qual um uma operação de índice online retomável é executada antes de ser colocada em pausa. 

ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
> [!NOTE]
>  Um índice não pode ser reorganizado quando ALLOW_PAGE_LOCKS está definido como OFF.  
  
 MAXDOP **=** max_degree_of_parallelism  
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Substitui a opção de configuração **max degree of parallelism** enquanto durar a operação do índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
> [!IMPORTANT]
>  Embora a opção MAXDOP tenha suporte sintaticamente em todos os índices XML, para um índice espacial ou um índice XML primário, no momento, ALTER INDEX usa apenas um único processador.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]
> As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos compatíveis com as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos compatíveis para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 COMPRESSION_DELAY **=** { **0** |*duration [Minutes]* }  
 Este recurso está disponível começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
 Para uma tabela baseada em disco, o atraso especifica o número mínimo de minutos que um rowgroup delta no estado CLOSED deve permanecer no rowgroup delta antes de o SQL Server poder compactá-lo no rowgroup compactado. Uma vez que tabelas baseadas em disco não controlam tempos de inserção e atualização em linhas individuais, o SQL Server aplica o atraso a rowgroups delta no estado CLOSED.  
O padrão é 0 minuto.  
  
 O padrão é 0 minuto.  
  
 Para obter recomendações sobre quando usar COMPRESSION_DELAY, consulte Índices columnstore para análise operacional em tempo real.  
  
 DATA_COMPRESSION  
 Especifica a opção de compactação de dados para o índice, número de partição ou intervalo de partições especificado. As opções são as seguintes:  
  
 Nenhuma  
 O índice ou as partições especificadas não são compactados. Não se aplica a índices columnstore.  
  
 ROW  
 O índice ou as partições especificadas são compactados com o uso da compactação de linha. Não se aplica a índices columnstore.  
  
 PAGE  
 O índice ou as partições especificadas são compactados com o uso da compactação de página. Não se aplica a índices columnstore.  
  
 COLUMNSTORE  
   
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE especifica a descompactação do índice ou partições especificadas compactadas com a opção COLUMNSTORE_ARCHIVE. Quando os dados forem restaurados, eles continuarão sendo compactados através da compactação columnstore usada em todos os índices columnstore.  
  
 COLUMNSTORE_ARCHIVE  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE_ARCHIVE compactará ainda mais a partição especificada para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.  
  
 Para obter mais informações sobre compactação, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [**,**...n] **)**  
    
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. 
  
 Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se o índice não for particionado, o argumento ON PARTITIONS irá gerar um erro. Se a cláusula ON PARTITIONS não for fornecida, a opção DATA_COMPRESSION será aplicada a todas as partições de um índice particionado.  
  
 \<partition_number_expression> pode ser especificado das seguintes maneiras:  
  
-   Forneça o número para uma partição, por exemplo: ON PARTITIONS (2).  
  
-   Forneça os números de várias partições individuais separados por vírgulas, por exemplo: ON PARTITIONS (1, 5).  
  
-   Forneça os intervalos e as partições individuais: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<range> pode ser especificado como números de partição separados pela palavra TO, por exemplo: ON PARTITIONS (6 TO 8).  
  
 Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção DATA_COMPRESSION mais de uma vez, por exemplo:  
  
```sql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 ONLINE **=** { ON | **OFF** } \<conforme se aplica a single_partition_rebuild_index_option>  
 Especifica se um índice ou partição do índice de uma tabela subjacente pode ser recriado online ou offline. Se **REBUILD** for executada online (**ON**), os dados nessa tabela estarão disponíveis para consultas e modificação de dados durante a operação de índice.  O padrão é **OFF**.  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Um bloqueio S na tabela é exigido no Início da recompilação de índice e um bloqueio Sch-M na tabela no final da recompilação de índice online. Embora ambos os bloqueios sejam bloqueios de metadados curtos, especialmente o bloqueio Sch-M deve esperar que todas as transações de bloqueio sejam concluídas. Durante o tempo de espera, o bloqueio Sch-M bloqueia todas as transações restantes que esperam atrás desse bloqueio ao acessar a mesma tabela.  
  
> [!NOTE]
>  A recompilação de índice online pode definir as opções *low_priority_lock_wait* descritas posteriormente nesta seção.  
  
 OFF  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação.  
  
 WAIT_AT_LOW_PRIORITY usado com **ONLINE=ON** apenas.  
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Uma recriação de índice online precisa aguardar as operações de bloqueio nesta tabela. **WAIT_AT_LOW_PRIORITY** indica que a operação de recompilação do índice online aguardará bloqueios de baixa prioridade, permitindo que outras operações continuem enquanto a operação de compilação de índice online estiver aguardando. Omitir a opção **WAIT AT LOW PRIORITY** é equivalente a WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutos, ABORT_AFTER_WAIT = NONE). Para obter mais informações, consulte [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 
  
 MAX_DURATION = *time* [**MINUTES**]  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 O tempo (um valor inteiro especificado em minutos) que a opção ou os bloqueios de recompilação de índice online deverão aguardar com baixa prioridade ao executar o comando DDL. Se a operação for bloqueada por **MAX_DURATION**, uma das ações de **ABORT_AFTER_WAIT** será executada. O tempo **MAX_DURATION** está sempre em minutos e a palavra **MINUTES** pode ser omitida.  
 
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
   
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Nenhuma  
 Continue aguardando o bloqueio com prioridade normal.  
  
 SELF  
 Saia da operação DDL de recompilação de índice online em execução no momento sem realizar a ação.  
  
 BLOCKERS  
 Elimine todas as transações de usuário que bloqueiam a operação DDL de recompilação de índice online para que a operação possa continuar. A opção **BLOCKERS** exige que o logon tenha a permissão **ALTER ANY CONNECTION**.  
 
 RESUME 
 
**Aplica-se a:** começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]  

Retome uma operação de índice que seja esteja em pausa manualmente ou devido a uma falha.

MAX_DURATION usado com **RESUMABLE=ON**

 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

O tempo (um valor de inteiro especificado em minutos) pelo qual a operação de índice online é executada após ser retomada. Quando o tempo expirar, a operação retomável será colocada em pausa se ainda estiver em execução.

WAIT_AT_LOW_PRIORITY usado com **RESUMABLE=ON** e **ONLINE = ON**.  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
 Retomar uma recompilação de índice online após uma pausa precisa esperar as operações de bloqueio nesta tabela. **WAIT_AT_LOW_PRIORITY** indica que a operação de recompilação do índice online aguardará bloqueios de baixa prioridade, permitindo que outras operações continuem enquanto a operação de compilação de índice online estiver aguardando. Omitir a opção **WAIT AT LOW PRIORITY** é equivalente a WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutos, ABORT_AFTER_WAIT = NONE). Para obter mais informações, consulte [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 


PAUSE
 
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
Pause uma operação de recompilação de índice online retomável.

ABORT

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

Anule uma operação de índice em execução ou em pausa declarada como retomável. Você precisa executar explicitamente uma operação **ABORT** para terminar uma operação de recompilação de índice retomável. Falha ou pausar uma operação de índice retomável não termina sua execução; em vez disso, deixa a operação em um estado de pausa indefinido.
  
## <a name="remarks"></a>Remarks  
ALTER INDEX não pode ser usado para reparticionar um índice ou movê-lo para um grupo de arquivos diferente. Essa instrução não pode ser usada para modificar a definição de índice, como adicionar ou excluir colunas ou alterar a ordem das colunas. Use CREATE INDEX com a cláusula DROP_EXISTING para executar essas operações.  
  
Quando uma opção não for especificada explicitamente, a configuração atual será aplicada. Por exemplo, se uma configuração FILLFACTOR não for especificada na cláusula REBUILD, o valor do fator de preenchimento armazenado no catálogo do sistema será usado durante o processo de recriação. Para exibir as configurações de opção de índice atuais, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
Os valores de ONLINE, MAXDOP e SORT_IN_TEMPDB não são armazenados no catálogo do sistema. A menos que especificado na instrução de índice, o valor padrão da opção será usado.
  
Em computadores com multiprocessadores, assim como ocorre com outras consultas, ALTER INDEX... REBUILD usa automaticamente mais processadores para executar as operações de verificação e classificação que estão associadas à modificação do índice. Quando você executa ALTER INDEX... REORGANIZE, com ou sem LOB_COMPACTION, o valor **grau máximo de paralelismo** é uma operação encadeada única. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!IMPORTANT]
> Um índice não poderá ser reorganizado ou recriado se o grupo de arquivos no qual ele está localizado estiver offline ou definido como somente leitura. Quando a palavra-chave ALL for especificada e um ou mais índices estiver em um grupo de arquivos offline ou somente leitura, a instrução falhará.  
  
## <a name="rebuilding-indexes"></a> Recompilando índices  
A recriação de um índice descarta e recria o índice. Isso remove a fragmentação, recupera espaço em disco ao compactar as páginas com base na configuração do fator de preenchimento especificada ou existente, e reclassifica as linhas do índice em páginas contíguas. Quando ALL é especificado, todos os índices da tabela são descartados e recriados em uma única transação. As restrições de chave estrangeira não precisam ser descartadas com antecedência. Quando índices com 128 extensões ou mais são recriados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.  
 
Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md). 
  
> [!NOTE]
> A recriação ou reorganização de índices pequenos geralmente não reduz a fragmentação. As páginas de índices pequenos às vezes são armazenadas em extensões mistas. Extensões mistas são compartilhadas por até oito objetos, portanto, a fragmentação em um índice pequeno pode não ser reduzida após a reorganização ou recriação.  
  
> [!IMPORTANT]
> Quando um índice for criado ou reconstruído no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as estatísticas serão criadas ou atualizadas por meio do exame de todas as linhas da tabela.
> 
> No entanto, começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar essas estatísticas. Para obter estatísticas em índices particionados por meio do exame de todas as linhas da tabela, use CREATE STATISTICS ou UPDATE STATISTICS com a cláusula FULLSCAN.  
  
Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], às vezes, era possível recriar um índice não clusterizado para corrigir as inconsistências causadas por falhas de hardware.    
No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posteriores, ainda é possível reparar essas inconsistências entre o índice e o índice clusterizado recriando um índice não clusterizado offline. Entretanto, não é possível reparar inconsistências de índice não clusterizado recriando o índice online, porque o mecanismo de recriação online usará o índice não clusterizado existente como base para a recriação e, portanto, a inconsistência persistirá. A recriação do índice offline poderá forçar, algumas vezes, um exame do índice clusterizado (ou heap) e, consequentemente, remover a inconsistência. Para garantir uma recompilação do índice clusterizado, remova e recrie o índice não clusterizado. Como nas versões anteriores, é recomendável que a recuperação de inconsistências seja feita com a restauração dos dados afetados de um backup; porém, talvez seja possível reparar as inconsistências do índice recriando o índice não clusterizado offline. Para obter mais informações, veja [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
Para recompilar um índice columnstore clusterizado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Obtenha um bloqueio exclusivo na tabela ou na partição durante a recompilação. Os dados estão “offline” e indisponíveis durante a recompilação.  
  
2.  Desfragmenta o columnstore excluindo fisicamente as linhas que foram excluídas logicamente da tabela; os bytes excluídos são recuperados na mídia física.  
  
3.  Lê todos os dados do índice columnstore original, incluindo o deltastore. Combina os dados em novos rowgroups e compacta os rowgroups em columnstore.  
  
4.  Requer espaço no meio físico para armazenar duas cópias do índice columnstore durante a recriação. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui o índice columnstore clusterizado original.  
  
## <a name="reorganizing-indexes"></a> Reorganizando índices  
A reorganização de um índice utiliza recursos mínimos do sistema. Ela desfragmenta o nível folha de índices clusterizados e não clusterizados em tabelas e exibições, reordenando fisicamente as páginas de nível folha para que correspondam à ordem lógica, da esquerda para a direita, dos nós folha. A reorganização também compacta as páginas de índice. A compactação baseia-se no valor do fator de preenchimento existente. Para exibir a configuração do fator de preenchimento, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
Quando ALL for especificado, os índices relacionais, clusterizados e não clusterizados e os índices XML da tabela serão reorganizados. Algumas restrições se aplicam quando ALL é especificado; veja a definição de ALL na seção Argumentos deste artigo.  
  
Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
 
> [!IMPORTANT]
> Quando um índice é reorganizado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as estatísticas não são atualizadas.
  
## <a name="disabling-indexes"></a> Desabilitando índices  
A desabilitação de um índice impede o acesso do usuário ao índice, e, para índices clusterizados, aos dados da tabela subjacente. A definição de índice permanece no catálogo do sistema. A desabilitação de um índice não clusterizado ou clusterizado em uma exibição exclui fisicamente os dados do índice. A desabilitação de um índice clusterizado impede o acesso aos dados, mas eles permanecem inalterados na árvore B até que o índice seja descartado ou recriado. Para exibir o status de um índice habilitado ou desabilitado, consulte a coluna **is_disabled** na exibição do catálogo **sys.indexes**.  
  
Se uma tabela estiver em uma publicação de replicação transacional, não será possível desabilitar nenhum índice associado a colunas de chave primária. Esses índices são necessários para a replicação. Para desabilitar um índice, você deve primeiramente descartar a tabela da publicação. Para obter mais informações, consulte [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
Use a instrução ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING para habilitar o índice. A recriação de um índice clusterizado desabilitado não pode ser executada com a opção ONLINE definida como ON. Para obter mais informações, consulte [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
## <a name="setting-options"></a>Opções de configuração  
É possível definir as opções ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY e STATISTICS_NORECOMPUTE para um índice especificado sem recriá-lo ou reorganizá-lo. Os valores modificados são aplicados imediatamente ao índice. Para exibir essas configurações, use **sys.indexes**. Para obter mais informações sobre opções de índice, consulte [Definir opções de índice](../../relational-databases/indexes/set-index-options.md).  
  
### <a name="row-and-page-locks-options"></a>Opções de bloqueios de linha e de página  
Quando ALLOW_ROW_LOCKS = ON e ALLOW_PAGE_LOCK = ON, os bloqueios em nível de linha, página e tabela são permitidos quando você acessa o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.  
  
Quando ALLOW_ROW_LOCKS = OFF e ALLOW_PAGE_LOCK = OFF, somente um bloqueio em nível de tabela é permitido ao acessar o índice.  
  
Se ALL for especificado quando as opções de bloqueio de linha ou de página forem definidas, as configurações serão aplicadas a todos os índices. Quando a tabela subjacente é um heap, as configurações são aplicadas das seguintes maneiras:  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON ou OFF|Ao heap e a quaisquer índices não clusterizados associados.|  
|ALLOW_PAGE_LOCKS = ON|Ao heap e a quaisquer índices não clusterizados associados.|  
|ALLOW_PAGE_LOCKS = OFF|Totalmente aos índices não clusterizados. Isso significa que todos os bloqueios de página não são permitidos nos índices não clusterizados. No heap, somente os bloqueios S (compartilhados), U (atualização) e X (exclusivos) da página não são permitidos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda pode adquirir um bloqueio de página intencional (IS, IU ou IX) para fins internos.|  
  
## <a name="online-index-operations"></a> Operações de índice online  
Ao recriar um índice, se a opção ONLINE estiver definida como ON, os objetos, as tabelas e os índices associados subjacentes estarão disponíveis para consultas e modificação de dados. Você também pode recriar online uma parte de um índice que reside em uma única partição. Os bloqueios de tabela exclusivos são mantidos por pouco tempo durante o processo de alteração.  
  
A reorganização de um índice sempre é executada online. O processo não mantém bloqueios de longo prazo e, portanto, não bloqueia consultas ou atualizações em execução.  
  
É possível executar operações de índice online simultâneas na mesma tabela ou partição de tabela somente ao fazer o seguinte:  
  
-   Criar vários índices não clusterizados.  
-   Reorganizar índices diferentes na mesma tabela.  
-   Reorganizar índices diferentes ao recriar índices não sobrepostos na mesma tabela.  
  
Todas as outras operações de índice online executadas ao mesmo tempo falham. Por exemplo, não é possível recriar dois ou mais índices na mesma tabela ao mesmo tempo, ou criar um novo índice ao recriar um índice existente na mesma tabela.  

### <a name="resumable-indexes"></a>Operações de índice retomáveis

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Online index rebuild é especificado como retomável usando a opção RESUMABLE=ON. 
-  A opção RESUMABLE não persiste nos metadados para um determinado índice e se aplica somente à duração de uma instrução DDL atual. Portanto, a cláusula RESUMABLE = ON deve ser especificada explicitamente para habilitar a capacidade de retomada.
-  A opção MAX_DURATION é compatível com a opção RESUMABLE=ON ou com a opção de argumento **low_priority_lock_wait**. 
   -  A opção MAX_DURATION para RESUMABLE especifica o intervalo para um índice que está sendo recompilado. Depois que esse tempo é consumido, a recompilação de índice é colocada em pausa ou conclui sua execução. O usuário decide quando uma recompilação de um índice em pausa pode ser retomada. O **time** em minutos para MAX_DURATION deve ser maior que 0 minutos e menor ou igual uma semana (7 * 24 * 60 = 10.080 minutos). Ter uma longa pausa para uma operação de índice pode afetar o desempenho de DML em uma tabela específica, bem como a capacidade de disco de banco de dados, já que tanto o original quanto o recém-criado exigem espaço em disco e precisam ser atualizados durante as operações DML. Se a opção MAX_DURATION for omitida, a operação de índice continuará até sua conclusão ou até que ocorra uma falha. 
   -  A opção de argumento \<low_priority_lock_wait > permite que você decida como a operação de índice pode continuar quando bloqueada no bloqueio SCH-M.
 
-  Executar novamente a instrução ALTER INDEX REBUILD original com os mesmos parâmetros retoma uma operação de recompilação de índice em pausa. Você também pode retomar uma operação de recompilação de índice em pausa executando a instrução ALTER INDEX RESUME.
-  A opção SORT_IN_TEMPDB=ON não é compatível com índice retomável 
-  O comando DDL com RESUMABLE=ON não pode ser executado em uma transação explícita (não pode fazer parte do bloco de confirmação begin tran…).
-  Apenas operações de índice em pausa estão retomáveis.
-  Ao retomar uma operação de índice em pausa, você pode alterar o valor MAXDOP para um novo valor.  Se MAXDOP não for especificado ao retomar uma operação de índice que está em pausa, o último valor MAXDOP será usado. Se a opção MAXDOP não for especificada para a operação de recompilação de índice, o valor padrão será usado.
- Para pausar imediatamente a operação de índice, você pode interromper o comando em andamento (Ctrl-C) ou executar o comando ALTER INDEX PAUSE ou o comando KILL *session_id*. Depois que o comando for colocado em pausa, ele poderá ser retomado usando a opção RESUME.
-  O comando ABORT elimina a sessão que hospedava a recompilação de índice original e elimina a operação de índice  
-  Não são necessários recursos extras para recompilação de índice retomáveis exceto para
   -    Espaço adicional necessário para manter o índice que está sendo criado, incluindo o tempo em que o índice está em pausa
   -    Um estado DDL que impede qualquer modificação de DDL
-  A limpeza duplicada será executada durante a fase de pausa do índice, mas ficará em pausa durante a execução de índice   
A seguinte funcionalidade está desabilitada para operações de recompilação do índice retomáveis
   -    Não é possível recompilar um índice desabilitado com RESUMABLE=ON
   -    Comando ALTER INDEX REBUILD ALL
   -    ALTER TABLE com recompilação de índice  
   -    O comando DDL com "RESUMEABLE = ON" não pode ser executado em uma transação explícita (não pode fazer parte do bloco de confirmação begin tran…)
   -    Recompile um índice que tenha colunas TIMESTAMP ou computadas como colunas chave.
-   Caso a tabela base contenha colunas LOB retomáveis clusterizadas, a recompilação do índice clusterizado exigirá um bloqueio Sch-M no início desta operação
   -    A opção SORT_IN_TEMPDB=ON não é compatível com índice retomável 

> [!NOTE]
> O comando DDL é executado até ser concluído, pausar ou falhar. Caso o comando pause, será emitido um erro indicando que a operação foi colocada em pausa e que a criação de índice não foi concluída. Para obter mais informações sobre o status atual do índice, veja [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). Como antes, no caso de uma falha, um erro será emitido também. 

 Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>WAIT_AT_LOW_PRIORITY com operações de índice online  
  
 Para executar a instrução DDL de uma recompilação de índice online, todas as transações de bloqueio ativas em execução em uma tabela específica devem ser concluídas. Quando a recompilação de índice online for executada, ela bloqueará todas as novas transações que estão prontas para iniciar a execução nessa tabela. Embora a duração do bloqueio da recompilação de índice online seja muito curta, é possível que a espera pela conclusão de todas as transações abertas em uma tabela específica e o bloqueio das novas transações a serem iniciadas afetem significativamente a taxa de transferência, diminuindo a velocidade da carga de trabalho ou ocasionando o tempo limite da mesma, e limite consideravelmente o acesso à tabela subjacente. A opção **WAIT_AT_LOW_PRIORITY** permite que os DBAs gerenciem o bloqueio S e os bloqueios Sch-M necessários para recompilações de índice online, e permite que selecionem uma das três opções. Nos três casos, se, durante o tempo de espera ( (MAX_DURATION = n [minutes]) ), não houver nenhuma atividade de bloqueio, a recompilação de índice online será executada imediatamente sem aguardar e a instrução DDL será concluída.  
  
## <a name="spatial-index-restrictions"></a>Restrições em índices espaciais  
 Quando você recria um índice espacial, a tabela de usuário subjacente não está disponível durante a operação do índice porque o índice espacial mantém um bloqueio de esquema.  
  
 Não é possível modificar a restrição PRIMARY KEY na tabela de usuário quando um índice espacial está definido em uma coluna dessa tabela. Para alterar a restrição PRIMARY KEY, primeiro descarte todos os índices espaciais da tabela. Depois de modificar a restrição PRIMARY KEY, é possível recriar cada um dos índices espaciais.  
  
 Em uma única operação de recriação de partição, não é possível especificar nenhum índice espacial. Entretanto, você pode especificar índices espaciais em uma recriação de partição completa.  
  
 Para alterar opções específicas a um índice espacial, como BOUNDING_BOX ou GRID, é possível usar uma instrução CREATE SPATIAL INDEX que especifique DROP_EXISTING = ON ou descartar o índice espacial e criar um novo. Para obter um exemplo, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
## <a name="data-compression"></a>Data Compression  
 Para obter mais informações sobre compactação de dados, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 Para avaliar como a alteração da compactação PAGE e ROW afetará uma tabela, um índice ou uma partição, use o procedimento armazenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md).  
  
As restrições a seguir se aplicam a índices particionados:  
  
-   Ao usar ALTER INDEX ALL ..., não será possível alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.  
-   O ALTER INDEX \<index>... REBUILD PARTITION ... recria a partição especificada do índice.  
-   O ALTER INDEX \<index>... REBUILD WITH... recria todas as partições do índice.  
  
## <a name="statistics"></a>Estatísticas  
 Quando você executar **ALTER INDEX ALL…** em uma tabela, somente as estatísticas associadas a índices serão atualizadas. As estatísticas automáticas ou manuais criadas na tabela (em vez de um índice) não são atualizadas.  
  
## <a name="permissions"></a>Permissões  
 Para executar ALTER INDEX, no mínimo, a permissão ALTER na tabela ou exibição é necessária.  
  
## <a name="version-notes"></a>Notas de versão  
  
-  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não usa opções filegroup nem filestream.  
-  Índices Columnstore não estão disponíveis antes de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. 
-  Operações de índice retomáveis estão disponíveis começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   
  
## <a name="basic-syntax-example"></a>Exemplo de sintaxe básica:   
  
```sql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>Exemplos: índices Columnstore  
 Estes exemplos se aplicam a índices columnstore.  
  
### <a name="a-reorganize-demo"></a>A. Demonstração de REORGANIZE  
 Este exemplo demonstra como funciona o comando ALTER INDEX REORGANIZE.  Ele cria uma tabela que tem vários rowgroups e, em seguida, demonstra como REORGANIZE mescla os rowgroups.  
  
```sql  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 Use a opção TABLOCK para inserir linhas em paralelo. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a operação INSERT INTO pode ser executada em paralelo quando TABLOCK for usado.  
  
```sql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 Execute este comando para ver os rowgroups delta OPEN. O número de rowgroups depende do grau de paralelismo.  
  
```sql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 Execute este comando para forçar todos os rowgroups CLOSED e OPEN para o columnstore.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 Execute este comando novamente e verá que os rowgroups menores são mesclados em um rowgroup compactado.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. Compactar rowgroups delta CLOSED para o columnstore  
 Este exemplo usa a opção REORGANIZE para compactar cada rowgroup delta CLOSED para o columnstore como um rowgroup compactado.   Isso não é necessário, mas é útil quando o motor de tupla não está compactando rowgroups CLOSED com rapidez suficiente.  
  
```sql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. Compactar todos os rowgroups delta OPEN AND CLOSED para o columnstore  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
 O comando REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON) compacta cada rowgroup delta OPEN e CLOSED para o columnstore como um rowgroup compactado. Isso esvazia o deltastore e força todas as linhas a serem compactadas no columnstore. Isso é útil principalmente depois de executar várias operações de inserção, já que essas operações armazenam as linhas em um ou mais rowgroups delta.  
  
 REORGANIZE combina rowgroups para preencher rowgroups até um número máximo de linhas \<= 1.024.576. Portanto, ao compactar todos os rowgroups OPEN e CLOSED, você não acabará com vários rowgroups compactados que tenham apenas algumas linhas neles. Você deseja que rowgroups sejam tão completos quanto possível para reduzir o tamanho compactado e melhorar o desempenho da consulta.  
  
```sql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. Desfragmentar um índice columnstore online  
 Não se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], REORGANIZE faz mais que compactar rowgroups delta para o columnstore. Ele também executa a desfragmentação online. Primeiro, reduz o tamanho do columnstore removendo fisicamente linhas excluídas quando 10% ou mais linhas em um grupo de linhas foram excluídos.  Em seguida, ele combina rowgroups para formar rowgroups maiores que tenham até o máximo de 1.024.576 linhas por rowgroup.  Todos os rowgroups que são alterados são recompactados.  
  
> [!NOTE]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], recompilar um índice columnstore não é mais necessário na maioria das situações, já que REORGANIZE remove fisicamente linhas excluídas e mescla rowgroups. A opção COMPRESS_ALL_ROW_GROUPS força todos os rowgroups delta OPEN ou CLOSED para o columnstore, o que antes só podia ser feito com uma recompilação. REORGANIZE está online e ocorre em segundo plano para que consultas possam continuar conforme a operação ocorre.  
  
```sql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. Recompilar um índice columnstore clusterizado offline  
Aplica-se a: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])   
  
> [!TIP]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], é recomendável usar ALTER INDEX REORGANIZE, em vez de ALTER INDEX REBUILD.  
  
> [!NOTE]
> Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], REORGANIZE só é usado para compactar rowgroups CLOSED para o columnstore. É a única maneira de realizar operações de desfragmentação e forçar todos os rowgroups delta para o columnstore é recompilar o índice.  
  
 Este exemplo mostra como recompilar um índice columnstore clusterizado e forçar todos os rowgroups delta para o columnstore. A primeira etapa prepara uma tabela FactInternetSales2 com um índice columnstore clusterizado e insere dados das quatro primeiras colunas.  
  
```sql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Os resultados mostram que há um rowgroup OPEN, o que significa que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aguardará mais linhas serem adicionadas antes de fechar o rowgroup e mover os dados para o columnstore. A próxima instrução recompila o índice columnstore clusterizado, o que força todas as linhas para o columnstore.  
  
```sql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Os resultados da instrução SELECT mostram que o rowgroup está COMPACTADO, o que significa que os segmentos de coluna do rowgroup agora estão compactados e armazenados no columnstore.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. Recompilar uma partição de um índice columnstore clusterizado offline  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  
 
 Para recompilar uma partição de um índice columnstore clusterizado grande, use ALTER INDEX REBUILD com a opção de partição. Este exemplo recompila a partição 12. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], é recomendável substituir a REBUILD por REORGANIZE.  
  
```sql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. Alterar um índice clusterizado columnstore para usar a compactação de arquivamento  
 Não se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 Você pode optar por reduzir o tamanho de um índice columnstore clusterizado ainda mais usando a opção de compactação de dados COLUMNSTORE_ARCHIVE. Isso é prático para dados mais antigos que você deseja manter em um armazenamento mais econômico. É recomendável usar isso apenas em dados que não são acessados com frequência, já que descompactar é mais lento do que a compactação COLUMNSTORE normal.  
  
 O exemplo a seguir recompila um índice columnstore clusterizado para usar a compactação de arquivamento e, em seguida, mostra como remover essa compactação. O resultado final usará apenas a compactação columnstore.  
  
```sql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>Exemplos: índices Rowstore  
  
### <a name="a-rebuilding-an-index"></a>A. Recriando um índice  
 O exemplo a seguir recompila um único índice na tabela `Employee` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. Recriando todos os índices de uma tabela e especificando opções  
 O exemplo a seguir especifica a palavra-chave ALL. Isso recompila todos os índices associados à tabela Production.Product no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Três opções são especificadas.  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
O exemplo a seguir adiciona a opção ONLINE que inclui a opção de bloqueio de baixa prioridade e adiciona a opção de compactação de linha.  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>C. Reorganizando um índice com a compactação LOB  
 O exemplo a seguir reorganiza um único índice clusterizado no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Como o índice contém um tipo de dados LOB no nível folha, a instrução também compacta todas as páginas que contêm dados de objeto grande. Observe que não é necessário especificar a opção WITH (LOB_COMPACTION) porque o valor padrão é ON.  
  
```sql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. Definindo opções em um índice  
 O exemplo a seguir define várias opções no índice `AK_SalesOrderHeader_SalesOrderNumber` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>E. Desabilitando um índice  
 O exemplo a seguir desabilita um índice não clusterizado na tabela `Employee` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. Desabilitando restrições  
 O exemplo a seguir desabilita uma restrição PRIMARY KEY desabilitando o índice PRIMARY KEY no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A restrição FOREIGN KEY na tabela subjacente é automaticamente desabilitada e a mensagem de aviso é exibida.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
O conjunto de resultados retorna esta mensagem de aviso.  
  
```  
Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
on table 'EmployeeDepartmentHistory' referencing table 'Department'  
was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
```  
  
### <a name="g-enabling-constraints"></a>G. Habilitando restrições  
 O exemplo a seguir habilita as restrições PRIMARY KEY e FOREIGN KEY que foram desabilitadas no exemplo F.  
  
A restrição PRIMARY KEY é habilitada com a recriação do índice PRIMARY KEY.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
Em seguida, a restrição FOREIGN KEY é habilitada.  
  
```sql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. Recriando um índice particionado  
 O exemplo a seguir recompila uma única partição, número de partição `5`, do índice particionado `IX_TransactionHistory_TransactionDate` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A partição 5 é recriada online e os 10 minutos do tempo de espera para o bloqueio de baixa prioridade se aplica separadamente a cada bloqueio pela operação de recriação de índice. Se durante esse tempo o bloqueio não puder ser obtido para recriação de índice completo, a instrução da operação de recriação será anulada.  
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>I. Alterando a configuração de compactação de um índice  
 O exemplo a seguir recompila um índice em uma tabela rowstore não particionada.  
  
```sql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
Para obter exemplos de compactação de dados adicionais, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
 
### <a name="j-online-resumable-index-rebuild"></a>J. Recompilação de índice online retomável

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 Os exemplos a seguir mostram como usar a recompilação de índice online de retomável. 

1. Executar uma recompilação de índice online como uma operação retomável com MAXDOP=1.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. Executar o mesmo comando novamente (veja acima) após uma operação de índice ter sido colocada em pausa retoma automaticamente a operação de recompilação de índice.

3. Execute uma recompilação de índice online como uma operação retomável com MAX_DURATION definido como 240 minutos.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. Pause uma recompilação de índice online retomável em execução.

   ```sql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. Retome uma recompilação de índice online para uma recompilação de índice executada como operação retomável especificando um novo valor de MAXDOP definido como 4.

   ```sql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. Retome uma operação de recompilação de índice online para uma recompilação de índice online executada como retomável. Defina MAXDOP como 2, defina o tempo de execução para o índice que está sendo executando como retomável para 240 minutos e, no caso de um índice que está sendo bloqueado no bloqueio, aguarde 10 minutos e depois encerre todos os bloqueadores. 

   ```sql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. Anule a operação de recompilação de índice retomável que está em execução ou em pausa.

   ```sql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>Consulte Também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)   
 [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
