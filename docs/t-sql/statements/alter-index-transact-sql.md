---
title: "Instrução ALTER INDEX (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- TSQL
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
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: 222
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bfe0bfe90cfb8a168fd2c87d662ba978c12a898e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Modifica uma tabela ou índice de exibição existente (relacional ou XML) desabilitando, recriando ou reorganizando o índice, ou definindo opções no índice.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and SQL Database
  
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
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela ou exibição, mas não precisam ser exclusivos no banco de dados. Os nomes de índice devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ALL  
 Especifica todos os índices associados à tabela ou exibição, independentemente do tipo de índice. Especificar ALL fará com que a instrução falhe se um ou mais índices estiverem em um grupo de arquivos offline ou somente leitura, ou se a operação especificada não for permitida em um ou mais tipos de índice. A tabela a seguir lista as operações de índice e os tipos de índice não permitidos.  
  
|Usando a palavra-chave ALL com esta operação|Falhará se a tabela tiver um ou mais|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice ColumnStore: **aplica-se a:** (começando com o SQL Server 2012) do SQL Server e banco de dados do SQL Azure.|  
|REBUILD PARTITION = *número_da_partição*|Índice não particionado, índice XML, índice espacial ou índice desabilitado|  
|REORGANIZE|Índices com ALLOW_PAGE_LOCKS definido como OFF|  
|REORGANIZAR partição = *número_da_partição*|Índice não particionado, índice XML, índice espacial ou índice desabilitado|  
|IGNORE_DUP_KEY = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice ColumnStore: **aplica-se a:** (começando com o SQL Server 2012) do SQL Server e banco de dados do SQL Azure.|  
|ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice ColumnStore: **aplica-se a:** (começando com o SQL Server 2012) do SQL Server e banco de dados do SQL Azure.|
| RETOMÁVEIS = ON  | Índices retomáveis não tem suportados com **todos os** palavra-chave. <br /><br /> **Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública) |   
  
> [!WARNING]
>  Para obter mais informações sobre operações de índice que podem ser executadas online, consulte [diretrizes para operações de índice Online](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

 Se ALL for especificado com PARTITION = *número_da_partição*, todos os índices devem ser alinhados. Isso significa que eles serão particionados com base nas funções de partições equivalentes. Usar ALL com PARTITION faz com que todas as partições de índice com o mesmo *número_da_partição* ser recompilado ou reorganizado. Para obter mais informações sobre índices particionados, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or_view_name*  
 É o nome da tabela ou exibição associada ao índice. Para exibir um relatório dos índices em um objeto, use o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.  
  
 Banco de dados SQL oferece suporte a database_name de formato de nome de três partes. [schema_name]. de table_or_view_name quando database_name é o banco de dados atual ou database_name é tempdb e table_or_view_name começa com #.  
  
 RECRIAR [WITH **(**\<rebuild_index_option > [ **,**... *n*]**)** ]  
 Especifica que o índice será recriado usando as mesmas colunas, tipo de índice, atributo de exclusividade e ordem de classificação. Essa cláusula é equivalente a [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md). REBUILD habilita um índice desabilitado. A recriação de um índice clusterizado não recriará os índices não clusterizados associados, a menos que a palavra-chave ALL seja especificada. Se não forem especificadas opções de índice, o índice existente opção valores armazenados em [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) são aplicadas. Qualquer opção de índice cujo valor não é armazenado em **sys. Indexes**, o padrão indicado na definição do argumento da opção se aplica.  
  
 Se ALL for especificado e a tabela subjacente for um heap, a operação de recriação não terá efeito na tabela. Quaisquer índices não clusterizados associados à tabela serão recriados.  
  
 A operação de recriação poderá ser registrada minimamente se o modelo de recuperação de banco de dados for definido como bulk-logged ou simples.  
  
> [!NOTE]
>  Ao recriar um índice XML primário, a tabela de usuário subjacente não estará disponível durante a operação de índice.  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2012) e o banco de dados do SQL Azure.
  
 Para índices columnstore, a operação de recompilação:  
  
1.  Não use a ordem de classificação.  
  
2.  Obtenha um bloqueio exclusivo na tabela ou na partição durante a recompilação.  Os dados estão "offline" e indisponíveis durante a recompilação, mesmo se você usar NOLOCK, RCSI ou SI.  
  
3.  Compacta novamente todos os dados do columnstore. Há duas cópias do índice columnstore durante a recompilação. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui o índice columnstore original.  
  
 Para obter mais informações sobre como reconstruir índices columnstore, consulte [desfragmentação de índices Columnstore -](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 Especifica que somente uma partição de um índice será recriada ou reorganizada. PARTIÇÃO não pode ser especificada se *index_name* não é um índice particionado.  
  
 PARTITION = ALL recria todas as partições.  
  
> [!WARNING]
>  É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações. É recomendável usar índices alinhados apenas quando o número de partições for maior que 1.000.  
  
 *número_da_partição*  
   
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.
  
 É o número de partição de um índice particionado que será reconstruído ou reorganizado. *número_da_partição* é uma expressão constante que pode fazer referência a variáveis. Isso inclui variáveis de tipo definido pelo usuário ou funções e funções definidas pelo usuário, mas não é possível fazer referência a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. *número_da_partição* deve existir ou a instrução falhará.  
  
 COM **(**\<single_partition_rebuild_index_option >**)**  
   
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 SORT_IN_TEMPDB, MAXDOP e DATA_COMPRESSION são as opções que podem ser especificadas ao recriar uma única partição (PARTITION =  *n* ). Índices XML não podem ser especificados em uma única operação de recriação de partição.  
  
 DISABLE  
 Marca o índice como desabilitado e indisponível para uso pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Qualquer índice pode ser desabilitado. A definição de um índice desabilitado permanece no catálogo do sistema sem nenhum dado de índice subjacente. Desabilitar um índice clusterizado evita que o usuário acesse os dados da tabela subjacente. Para habilitar um índice, use ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING. Para obter mais informações, consulte [desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md) e [habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
 REORGANIZAR um índice rowstore  
 Para índices rowstore, REORGANIZE especifica para reorganizar o nível folha de índice.  A operação de REORGANIZAÇÃO é:  
  
-   Sempre executadas online. Isso significa que os bloqueios de tabela de longo prazo não são mantidos e que as consultas ou atualizações da tabela subjacente podem continuar durante a transação ALTER INDEX REORGANIZE.  
  
-   Não é permitido para um índice desabilitado  
  
-   Não é permitido quando ALLOW_PAGE_LOCKS está definido como OFF  
  
-   Não revertida quando ela é executada em uma transação e a transação será revertida.  
  
REORGANIZAR COM **(** LOB_COMPACTION = { **ON** | OFF} **)**  
 Aplica-se a índices rowstore.  
  
LOB_COMPACTION = ON  
  
-   Especifica para compactar todas as páginas que contêm dados desses tipos de dados de objeto grande (LOB): imagem, texto, ntext, varchar (max), nvarchar (max), varbinary (max) e xml. A compactação desses dados pode reduzir o tamanho dos dados no disco.  
  
-   Para um índice clusterizado, isso compacta todas as colunas LOB contidas na tabela.  
  
-   Para um índice não clusterizado, isso compacta todas as colunas LOB que são colunas (incluídas) no índice.  
  
-   REORGANIZAR todos executa LOB_COMPACTION em todos os índices. Para cada índice, isso compacta todas as colunas LOB no índice clusterizado, tabela subjacente ou colunas incluídas em um índice não clusterizado.  
  
LOB_COMPACTION = OFF  
  
-   Páginas que contêm dados de objeto grande não são compactadas.  
  
-   OFF não tem nenhum efeito em um heap.  
  
REORGANIZAR um índice columnstore  
REORGANIZAÇÃO é executada online.  
  
Para índices columnstore, REORGANIZE compacta cada delta FECHADOS para o columnstore como um rowgroup compactado.  
  
-   REORGANIZE não é necessária para mover rowgroups delta FECHADOS em rowgroups compactados. O processo de movimentação de tupla (TM) em segundo plano é ativado periodicamente para compactar rowgroups delta FECHADOS. É recomendável usar REORGANIZE quando o motor de tupla está atrasado. REORGANIZE pode compactar rowgroups de forma mais agressiva.  
  
-   Para compactar todos os rowgroups aberto e fechado, consulte a opção REORGANIZE com (COMPRESS_ALL_ROW_GROUPS) nesta seção.  
  
Para índices columnstore no SQL Server (começando com 2016) e o banco de dados SQL, REORGANIZE executa as seguintes otimizações adicionais desfragmentação online:  
  
-   Remove fisicamente linhas de um grupo de linhas quando 10% ou mais linhas foram excluídas logicamente. Os bytes excluídos são recuperados na mídia física. Por exemplo, se um grupo de linhas compactado de 1 milhão de linhas tem 100 mil linhas excluídas, o SQL Server remover as linhas excluídas e recompactar o rowgroup com a 900 mil linhas. Ele salva no armazenamento removendo linhas excluídas.  
  
-   Combina um ou mais rowgroups compactados para aumentar linhas por rowgroup até o máximo de 1,024,576 linhas. Por exemplo, se importar em massa 5 lotes de 102.400 linhas, você obterá 5 rowgroups compactados. Se você executar REORGANIZE, estes rowgroups serão mescladas em 1 grupo de linhas compactado de 512,000 linhas de tamanho. Isso pressupõe que não havia nenhum dicionário limitações de tamanho ou memória.  
  
-   Para rowgroups em que 10% ou mais linhas foram excluídas logicamente, SQL Server tenta combinar esse grupo de linhas com um ou mais rowgroups.    Por exemplo, 1 do rowgroup é compactado com 500.000 linhas e linhas 21 é compactada com o máximo de 1.048.576 linhas.  21 de grupo de linhas tem 60% das linhas excluídas que deixa 409,830 linhas. SQL Server favorece combinar essas duas rowgroups para compactar um grupo de linhas novas com 909,830 linhas.  
  
REORGANIZAR COM (COMPRESS_ALL_ROW_GROUPS = {ON | **OFF** })  
 No SQL Server (começando com 2016) e o banco de dados SQL, o COMPRESS_ALL_ROW_GROUPS fornece uma maneira para forçar os rowgroups delta aberto ou fechado para o columnstore. Com essa opção, não é necessário recriar o índice columnstore para esvaziar os rowgroups delta.  Isso, combinado com o outros remover e mesclagem desfragmentação recursos torna não é mais necessário reconstruir o índice na maioria das situações.    
-   ON força todos os rowgroups do ColumnStore, independentemente do tamanho e estado (FECHADAS ou ABERTAS).  
  
-   Desativar força todos os rowgroups CLOSED para o columnstore.  
  
DEFINIR **(** \<set_index opção > [ **,**... *n*] **)**  
 Especifica opções de índice sem recriar ou reorganizar o índice. SET não pode ser especificado para um índice desabilitado.  
  
PAD_INDEX = { ON | OFF }  
   
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 A porcentagem de espaço livre especificada por FILLFACTOR é aplicada às páginas de nível intermediário do índice. Se FILLFACTOR não for especificado ao mesmo tempo em que PAD_INDEX for definido como ON, o preenchimento fatores valor armazenado em [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) é usado.  
  
 DESATIVAR ou *fillfactor* não for especificado  
 As páginas do nível intermediário são preenchidas até próximo à capacidade máxima. Isso deixa espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, com base no conjunto de chaves das páginas intermediárias.  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
FILLFACTOR = *fator de preenchimento*  
 
 **Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.
  
 Especifica uma porcentagem que indica quanto [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. *fator de preenchimento* deve ser um valor inteiro de 1 a 100. O padrão é 0. Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.  
  
 Uma configuração FILLFACTOR explícita é usada somente quando o índice é criado pela primeira vez ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 Para exibir a configuração do fator de preenchimento, use **sys. Indexes**.  
  
> [!IMPORTANT]
>  A criação ou alteração de um índice clusterizado com um valor FILLFACTOR afeta a quantidade de espaço de armazenamento que os dados ocupam, pois o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 

**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 Especifica se deseja armazenar os resultados de classificação em **tempdb**. O padrão é OFF.  
  
 ON  
 Os resultados intermediários de classificação que são usados para criar o índice são armazenados em **tempdb**. Se **tempdb** está em um conjunto de discos diferente do banco de dados do usuário, isso pode reduzir o tempo necessário para criar um índice. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 Se uma operação de classificação não for necessária, ou se a classificação puder ser executada na memória, a opção SORT_IN_TEMPDB será ignorada.  
  
 Para obter mais informações, consulte [opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY  **=**  {ON | OFF}  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. O padrão é OFF.  
  
 ON  
 Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.  
  
 OFF  
 Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.  
  
 Ignore_dup_key não pode ser definida como ON para índices criados em um modo de exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.  
  
 Para exibir IGNORE_DUP_KEY, use [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Na sintaxe compatível com versões anteriores, WITH IGNORE_DUP_KEY é equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | OFF}  
 Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ON  
 As estatísticas desatualizadas não são recalculadas automaticamente.  
  
 OFF  
 A atualização automática de estatísticas está habilitada.  
  
 Para restaurar a atualização automática de estatísticas, defina STATISTICS_NORECOMPUTE como OFF ou execute UPDATE STATISTICS sem a cláusula NORECOMPUTE.  
  
> [!IMPORTANT]
>  Desabilitar o recálculo automático de estatísticas de distribuição pode impedir que o otimizador de consulta selecione os planos de execução ideais para consultas que envolvem a tabela.  
  
 STATISTICS_INCREMENTAL = {ON | **OFF** }  
 Quando **ON**, as estatísticas serão criadas por estatísticas de partição. Quando **OFF**, a árvore de estatísticas é descartada e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recomputará as estatísticas. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, a opção será ignorada e um aviso será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
  
-   Estatísticas criadas em bancos de dados somente leitura.  
  
-   Estatísticas criadas em índices filtrados.  
  
-   Estatísticas criadas em exibições.  
  
-   Estatísticas criadas em tabelas internas.  
  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
 
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.  
  
 On-line  **=**  {ON | **OFF** } \<como se aplica a rebuild_index_option >  
 Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF.  
  
 Para um índice XML ou índice espacial, só há suporte para ONLINE = OFF e, se ONLINE for definido como ON, um erro será gerado.  
  
> [!NOTE]
>  As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Isso permite que as consultas ou atualizações na tabela e nos índices subjacentes continuem. No início da operação, um bloqueio S (Compartilhado) é mantido brevemente no objeto de origem. Ao término da operação, por um breve momento, um bloqueio S será mantido na origem se um índice não clusterizado estiver sendo criado; ou um bloqueio SCH-M (Modificação de Esquema) será adquirido quando um índice clusterizado for criado ou descartado online, ou quando um índice clusterizado ou não clusterizado estiver sendo recriado. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local.  
  
 DESATIVADO  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Uma operação de índice offline que cria, recria ou descarta um índice clusterizado, espacial ou XML, ou que recria ou descarta um índice não clusterizado, adquire um bloqueio Sch-M na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT.  
  
 Para obter mais informações, consulte [como funcionam as operações de índice Online](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Índices, inclusive aqueles em tabelas temporárias globais, podem ser recriados online com as seguintes exceções:  
  
-   índices XML  
  
-   Índices em tabelas temporárias locais  
  
-   Um subconjunto de um índice particionado (é possível recriar online um índice particionado inteiro.)  

-  Antes de V12 no banco de dados SQL e SQL Server anterior ao SQL Server 2012, não é possível fazer o `ONLINE` opção para compilação de índice clusterizado ou recriar operações quando a tabela base contém **varchar (max)** ou **varbinary (max)**  colunas.

RETOMÁVEIS  **=**  {ON | **OFF**}

**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)  

 Especifica se uma operação de índice online é reiniciável.

 NO índice de operação é reiniciável.

 DESATIVAR o índice de operação não é reiniciável.

MAX_DURATION  **=**  *tempo* [**minutos**] usado com **RETOMÁVEL = ON** (requer **ONLINE = ON**).
 
**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)  

Indica o tempo (um valor inteiro especificado em minutos) que um retomáveis online operação de índice é executada antes de ser pausado. 

ALLOW_ROW_LOCKS  **=**  { **ON** | OFF}  
 
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** | OFF}  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.
  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
> [!NOTE]
>  Um índice não pode ser reorganizado quando ALLOW_PAGE_LOCKS está definido como OFF.  
  
 MAXDOP  **=**  max_degree_of_parallelism  
 
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
 Substitui o **grau máximo de paralelismo** opção de configuração para a duração da operação de índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
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
>  Operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 COMPRESSION_DELAY  **=**  { **0** |*duração [minutos]* }  
 Este recurso está disponível a partir do SQL Server 2016  
  
 Para uma tabela baseada em disco, o atraso Especifica o número mínimo de minutos que um rowgroup delta no estado CLOSED deve permanecer no rowgroup delta antes do SQL Server pode compactá-las no rowgroup compactado. Como as tabelas baseadas em disco não controlar inserir e atualizar horários em linhas individuais, o SQL Server aplica o atraso para rowgroups delta no estado fechado.  
O padrão é 0 minutos.  
  
 O padrão é 0 minutos.  
  
 Para obter recomendações sobre quando usar COMPRESSION_DELAY, consulte índices Columnstore para análise operacional em tempo real.  
  
 DATA_COMPRESSION  
 Especifica a opção de compactação de dados para o índice, número de partição ou intervalo de partições especificado. As opções são as seguintes:  
  
 Nenhuma  
 O índice ou as partições especificadas não são compactados. Não se aplica a índices columnstore.  
  
 ROW  
 O índice ou as partições especificadas são compactados com o uso da compactação de linha. Não se aplica a índices columnstore.  
  
 PAGE  
 O índice ou as partições especificadas são compactados com o uso da compactação de página. Não se aplica a índices columnstore.  
  
 COLUMNSTORE  
   
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.
  
 Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE especifica a descompactação do índice ou partições especificadas compactadas com a opção COLUMNSTORE_ARCHIVE. Quando os dados forem restaurados, eles continuarão sendo compactados através da compactação columnstore usada em todos os índices columnstore.  
  
 COLUMNSTORE_ARCHIVE  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.
  
 Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE_ARCHIVE compactará ainda mais a partição especificada para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.  
  
 Para obter mais informações sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 EM partições **(** { \<partition_number_expression > | \<intervalo >} [**,**... n] **)**  
    
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure. 
  
 Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se o índice não for particionado, o argumento ON PARTITIONS irá gerar um erro. Se a cláusula ON PARTITIONS não for fornecida, a opção DATA_COMPRESSION será aplicada a todas as partições de um índice particionado.  
  
 \<partition_number_expression > pode ser especificado das seguintes maneiras:  
  
-   Forneça o número de uma partição, por exemplo: ON PARTITIONS (2).  
  
-   Forneça os números de várias partições individuais separados por vírgulas, por exemplo: ON PARTITIONS (1, 5).  
  
-   Forneça os intervalos e as partições individuais: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<Range > pode ser especificado como números de partição separados pela palavra TO, por exemplo: ON PARTITIONS (6 TO 8).  
  
 Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção DATA_COMPRESSION mais de uma vez, por exemplo:  
  
```tsql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 On-line  **=**  {ON | **OFF** } \<como se aplica a single_partition_rebuild_index_option >  
 Especifica se um índice ou partição do índice de uma tabela subjacente pode ser reconstruída online ou offline. Se **RECRIAR** é executada online (**ON**) os dados nesta tabela estão disponíveis para consultas e modificação de dados durante a operação de índice.  O padrão é **OFF**.  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. É necessário um bloqueio S na tabela no início da recompilação de índice e um bloqueio Sch-M na tabela no final da recompilação de índice online. Embora ambos os bloqueios sejam bloqueios de metadados curtos, especialmente o bloqueio Sch-M deve esperar que todas as transações de bloqueio sejam concluídas. Durante o tempo de espera, o bloqueio Sch-M bloqueia todas as transações restantes que esperam atrás desse bloqueio ao acessar a mesma tabela.  
  
> [!NOTE]
>  Recompilação de índice online pode definir o *low_priority_lock_wait* opções descritas posteriormente nesta seção.  
  
 OFF  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação.  
  
 WAIT_AT_LOW_PRIORITY usado com **ONLINE = ON** somente.  
 
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.
  
 Uma recriação de índice online precisa aguardar as operações de bloqueio nesta tabela. **WAIT_AT_LOW_PRIORITY** indica que a operação de recriação de índice online aguardará bloqueios de baixa prioridade, permitindo que outras operações continuem enquanto a operação de compilação de índice online estiver aguardando. A omissão de **WAIT AT LOW PRIORITY** opção é equivalente a `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Para obter mais informações, consulte [WAIT_AT_LOW_PRIORITY](https://msdn.microsoft.com/library/ms188388.aspx). 
  
 MAX_DURATION = *tempo* [**minutos**]  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.
  
 O tempo (um valor inteiro especificado em minutos) que a opção ou os bloqueios de recompilação de índice online deverão aguardar com baixa prioridade ao executar o comando DDL. Se a operação está bloqueada para o **MAX_DURATION** de tempo, uma da **ABORT_AFTER_WAIT** ações serão executadas. **MAX_DURATION** hora é sempre em minutos e a palavra **minutos** pode ser omitido.  
 
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOQUEADORES** }]  
   
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.
  
 Nenhuma  
 Continue aguardando o bloqueio com prioridade normal.  
  
 SELF  
 Saia da operação DDL de recompilação de índice online em execução no momento sem realizar a ação.  
  
 BLOCKERS  
 Elimine todas as transações de usuário que bloqueiam a operação DDL de recompilação de índice online para que a operação possa continuar. O **BLOQUEADORES** opção requer o logon tenha **ALTER ANY CONNECTION** permissão.  
 
 RESUME 
 
**Aplica-se a**: começando com o SQL Server 2017 (recurso está em visualização pública)

Retome uma operação de índice é pausada manualmente ou devido a uma falha.

MAX_DURATION usado com **RETOMÁVEL = ON**

 
**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)

O tempo de operação de índice online retomáveis (um valor inteiro especificado em minutos) é executada após a retomada. Quando o tempo expira, a operação retomável está pausada se ele ainda está em execução.

WAIT_AT_LOW_PRIORITY usado com **RETOMÁVEL = ON** e **ONLINE = ON**.  
  
**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)
  
 Retomar uma recompilação de índice online após uma pausa de espera de bloqueio de operações nesta tabela. **WAIT_AT_LOW_PRIORITY** indica que a operação de recriação de índice online aguardará bloqueios de baixa prioridade, permitindo que outras operações continuem enquanto a operação de compilação de índice online estiver aguardando. A omissão de **WAIT AT LOW PRIORITY** opção é equivalente a `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Para obter mais informações, consulte [WAIT_AT_LOW_PRIORITY](https://msdn.microsoft.com/library/ms188388.aspx). 


PAUSAR
 
**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)
  
Pause uma operação de recompilação de índice online reiniciável.

ANULAR

**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)   

Anule uma operação de índice em execução ou em pausa que foi declarada como reiniciável. Você precisa executar explicitamente um **anular** operação de reconstrução de um índice retomável de finalização do comando. Falha ou pausar uma operação de índice retomáveis não encerra sua execução; em vez disso, ele deixa a operação em um estado de pausa indefinido.
  
## <a name="remarks"></a>Comentários  
 ALTER INDEX não pode ser usado para reparticionar um índice ou movê-lo para um grupo de arquivos diferente. Essa instrução não pode ser usada para modificar a definição de índice, como adicionar ou excluir colunas ou alterar a ordem das colunas. Use CREATE INDEX com a cláusula DROP_EXISTING para executar essas operações.  
  
 Quando uma opção não for especificada explicitamente, a configuração atual será aplicada. Por exemplo, se uma configuração FILLFACTOR não for especificada na cláusula REBUILD, o valor do fator de preenchimento armazenado no catálogo do sistema será usado durante o processo de recriação. Para exibir as configurações de opção de índice atual, use [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!NOTE]
>  Os valores de ONLINE, MAXDOP e SORT_IN_TEMPDB não são armazenados no catálogo do sistema. A menos que especificado na instrução de índice, o valor padrão da opção será usado.
  
 Em computadores multiprocessador, assim como acontece em outras consultas, ALTER INDEX REBUILD usa automaticamente mais processadores para executar operações de exame e classificação associadas à modificação do índice. Quando você executar ALTER INDEX REORGANIZE, com ou sem LOB_COMPACTION, o **grau máximo de paralelismo** valor é uma operação de thread único. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 Um índice não poderá ser reorganizado ou recriado se o grupo de arquivos no qual ele está localizado estiver offline ou definido como somente leitura. Quando a palavra-chave ALL for especificada e um ou mais índices estiver em um grupo de arquivos offline ou somente leitura, a instrução falhará.  
  
## <a name="rebuilding-indexes"></a>Recriando índices  
 A recriação de um índice descarta e recria o índice. Isso remove a fragmentação, recupera espaço em disco ao compactar as páginas com base na configuração do fator de preenchimento especificada ou existente, e reclassifica as linhas do índice em páginas contíguas. Quando ALL é especificado, todos os índices da tabela são descartados e recriados em uma única transação. As restrições FOREIGN KEY não precisam ser descartadas com antecedência. Quando índices com 128 extensões ou mais são recriados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.  
  
 A recriação ou reorganização de índices pequenos geralmente não reduz a fragmentação. As páginas de índices pequenos às vezes são armazenadas em extensões mistas. Extensões mistas são compartilhadas por até oito objetos, portanto, a fragmentação em um índice pequeno pode não ser reduzida após a reorganização ou recriação.  
  
 Começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Para obter estatísticas em índices particionados por meio do exame de todas as linhas da tabela, use CREATE STATISTICS ou UPDATE STATISTICS com a cláusula FULLSCAN.  
  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], às vezes, era possível recriar um índice não clusterizado para corrigir as inconsistências causadas por falhas de hardware. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posteriores, ainda é possível reparar essas inconsistências entre o índice e o índice clusterizado recriando um índice não clusterizado offline. Entretanto, não é possível reparar inconsistências de índice não clusterizado recriando o índice online, porque o mecanismo de recriação online usará o índice não clusterizado existente como base para a recriação e, portanto, a inconsistência persistirá. A recriação do índice offline poderá forçar, algumas vezes, um exame do índice clusterizado (ou heap) e, consequentemente, remover a inconsistência. Para garantir uma recompilação do índice clusterizado, remova e recrie o índice não clusterizado. Como nas versões anteriores, é recomendável que a recuperação de inconsistências seja feita com a restauração dos dados afetados de um backup; porém, talvez seja possível reparar as inconsistências do índice recriando o índice não clusterizado offline. Para obter mais informações, veja [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
 Para recompilar um índice columnstore clusterizado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Obtenha um bloqueio exclusivo na tabela ou na partição durante a recompilação. Os dados estão “offline” e indisponíveis durante a recompilação.  
  
2.  Desfragmenta o columnstore excluindo fisicamente as linhas que foram excluídas logicamente da tabela; os bytes excluídos são recuperados na mídia física.  
  
3.  Lê todos os dados do índice columnstore original, incluindo o deltastore. Combina os dados em novos rowgroups e compacta os rowgroups em columnstore.  
  
4.  Requer espaço no meio físico para armazenar duas cópias do índice columnstore durante a recriação. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui o índice columnstore clusterizado original.  
  
## <a name="reorganizing-indexes"></a>Reorganizando índices  
 A reorganização de um índice utiliza recursos mínimos do sistema. Ela desfragmenta o nível folha de índices clusterizados e não clusterizados em tabelas e exibições, reordenando fisicamente as páginas de nível folha para que correspondam à ordem lógica, da esquerda para a direita, dos nós folha. A reorganização também compacta as páginas de índice. A compactação baseia-se no valor do fator de preenchimento existente. Para exibir a configuração do fator de preenchimento, use [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Quando ALL for especificado, os índices relacionais, clusterizados e não clusterizados e os índices XML da tabela serão reorganizados. Algumas restrições se aplicam quando ALL é especificado; consulte a definição de ALL na seção Argumentos.  
  
 Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="disabling-indexes"></a>Desabilitando índices  
 A desabilitação de um índice impede o acesso do usuário ao índice, e, para índices clusterizados, aos dados da tabela subjacente. A definição de índice permanece no catálogo do sistema. A desabilitação de um índice não clusterizado ou clusterizado em uma exibição exclui fisicamente os dados do índice. A desabilitação de um índice clusterizado impede o acesso aos dados, mas eles permanecem inalterados na árvore B até que o índice seja descartado ou recriado. Para exibir o status de um índice habilitado ou desabilitado, consulte o **is_disabled** coluna o **sys. Indexes** exibição do catálogo.  
  
 Se uma tabela estiver em uma publicação de replicação transacional, não será possível desabilitar nenhum índice associado a colunas de chave primária. Esses índices são necessários para a replicação. Para desabilitar um índice, você deve primeiramente descartar a tabela da publicação. Para obter mais informações, consulte [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Use a instrução ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING para habilitar o índice. A recriação de um índice clusterizado desabilitado não pode ser executada com a opção ONLINE definida como ON. Para obter mais informações, consulte [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
## <a name="setting-options"></a>Opções de configuração  
 É possível definir as opções ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY e STATISTICS_NORECOMPUTE para um índice especificado sem recriá-lo ou reorganizá-lo. Os valores modificados são aplicados imediatamente ao índice. Para exibir essas configurações, use **sys. Indexes**. Para obter mais informações sobre opções de índice, consulte [Definir opções de índice](../../relational-databases/indexes/set-index-options.md).  
  
### <a name="row-and-page-locks-options"></a>Opções de bloqueios de linha e de página  
 Quando ALLOW_ROW_LOCKS = ON e ALLOW_PAGE_LOCK = ON, os bloqueios em nível de linha, página e tabela são permitidos quando você acessa o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.  
  
 Quando ALLOW_ROW_LOCKS = OFF e ALLOW_PAGE_LOCK = OFF, somente um bloqueio em nível de tabela é permitido ao acessar o índice.  
  
 Se ALL for especificado quando as opções de bloqueio de linha ou de página forem definidas, as configurações serão aplicadas a todos os índices. Quando a tabela subjacente é um heap, as configurações são aplicadas das seguintes maneiras:  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON ou OFF|Ao heap e a quaisquer índices não clusterizados associados.|  
|ALLOW_PAGE_LOCKS = ON|Ao heap e a quaisquer índices não clusterizados associados.|  
|ALLOW_PAGE_LOCKS = OFF|Totalmente aos índices não clusterizados. Isso significa que todos os bloqueios de página não são permitidos nos índices não clusterizados. No heap, somente os bloqueios S (compartilhados), U (atualização) e X (exclusivos) da página não são permitidos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda pode adquirir um bloqueio de página intencional (IS, IU ou IX) para fins internos.|  
  
## <a name="online-index-operations"></a>Operações de índice online  
 Ao recriar um índice, se a opção ONLINE estiver definida como ON, os objetos, as tabelas e os índices associados subjacentes estarão disponíveis para consultas e modificação de dados. Você também pode recriar online uma parte de um índice que reside em uma única partição. Os bloqueios de tabela exclusivos são mantidos por pouco tempo durante o processo de alteração.  
  
 A reorganização de um índice sempre é executada online. O processo não mantém bloqueios de longo prazo e, portanto, não bloqueia consultas ou atualizações em execução.  
  
 É possível executar operações de índice online simultâneas na mesma tabela ou partição de tabela somente ao fazer o seguinte:  
  
-   Criar vários índices não clusterizados.  
  
-   Reorganizar índices diferentes na mesma tabela.  
  
-   Reorganizar índices diferentes ao recriar índices não sobrepostos na mesma tabela.  
  
 Todas as outras operações de índice online executadas ao mesmo tempo falham. Por exemplo, não é possível recriar dois ou mais índices na mesma tabela ao mesmo tempo, ou criar um novo índice ao recriar um índice existente na mesma tabela.  

### <a name="resumable-index-operations"></a>Operações de índice retomáveis

**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)

RECONSTRUÇÃO de índice ONLINE é especificado como retomáveis usando o RETOMÁVEL = opção. 
-  A opção RETOMÁVEL não é persistente nos metadados para um determinado índice e se aplica somente a duração de uma instrução DDL atual. Portanto, o RETOMÁVEL = ON cláusula deve ser especificada explicitamente para habilitar a oferecer.

-  Observe que duas opções diferentes de MAX_DURATION. Um está relacionado à low_priority_lock_wait e o outro está relacionado ao RETOMÁVEL = opção.
   -  RETOMÁVEL oferecem suporte a opção MAX_DURATION = opção ou **low_priority_lock_wait** opção de argumento. 
   MAX_DURATION RETOMÁVEIS opção especifica o intervalo de tempo para um índice que está sendo recompilação. Depois que essa hora é usada a recompilação de índice é pausada ou concluir sua execução. Usuário decide quando uma recompilação de um índice de pausa pode ser retomada. O **tempo** em minutos para MAX_DURATION deve ser maior que 0 minutos e menor ou igual uma semana (7 x 24 x 60 = 10080 minutos). Ter uma longa pausa para uma operação de índice pode afetar o desempenho de DML em uma tabela específica, bem como a capacidade de disco de banco de dados como ambos os índices original e um recém-criado exigem espaço em disco e precisa ser atualizado durante as operações DML. Se a opção MAX_DURATION for omitida, a operação de índice continuará até sua conclusão ou até que ocorra uma falha. 
-   O \<low_priority_lock_wait > argumento opção permite que você decida como a operação de índice pode continuar quando bloqueado o bloqueio SCH-M.
 
-  Executar novamente a instrução ALTER INDEX REBUILD original com os mesmos parâmetros retoma uma operação de recompilação de índice em pausa. Você também pode retomar uma operação de recompilação de índice em pausa, executando a instrução ALTER INDEX RETOMAR.
-  O SORT_IN_TEMPDB = ON não há suporte para a opção de índice retomável 
-  O comando DDL com RETOMÁVEL = ON não pode ser executado em uma transação explícita (não pode ser parte de begin tran... bloco de confirmação).
-  Apenas operações de índice em pausa estão reiniciáveis.
-   Ao retomar uma operação de índice está pausada, você pode alterar o valor MAXDOP para um novo valor.  Se MAXDOP não for especificado ao retomar uma operação de índice que está em pausa, o último valor MAXDOP é obtido. Se a opção MAXDOP não é especificada para a operação de recriação de índice, o valor padrão é obtido.
- Para interromper imediatamente a operação de índice, você pode interromper o comando em andamento (Ctrl-C) ou você pode executar o comando ALTER INDEX pausar ou a instrução KILL *session_id* comando. Depois que o comando está em pausa pode ser retomado usando a opção de continuar.
-  O comando anular elimina a sessão que hospedado a recompilação de índice original e anula a operação de índice  
-  Não há recursos adicionais são necessários para recompilação de índice retomáveis exceto para
   -    Espaço adicional necessário para manter o índice que está sendo criado, incluindo o tempo quando o índice está em pausa
   -    Um estado DDL para evitar qualquer modificação de DDL
-  A limpeza fantasma será executado durante a fase de pausa do índice, mas ele será pausado durante a execução de índice   
A seguinte funcionalidade está desabilitada para operações de recriação de índice retomáveis
   -    Não há suporte para a recriação de um índice que está desabilitado com RETOMÁVEL = ON
   -    Comando ALTER INDEX REBUILD ALL
   -    ALTER TABLE com a recompilação de índice  
   -    O comando DDL com "RESUMEABLE = ON" não pode ser executado em uma transação explícita (não pode ser parte de begin tran... bloco de confirmação)
   -    Recrie um índice que tem computadas ou colunas de carimbo de hora como colunas de chave.
-   No caso da tabela base contém colunas LOB retomáveis clusterizadas recompilação de índice requer um bloqueio Sch-M no início desta operação
   -    O SORT_IN_TEMPDB = ON não há suporte para a opção de índice retomável 

> [!NOTE]
> O comando DDL é executado até que ela é concluída, faz uma pausa ou falha. No caso do comando pausa, será emitido um erro indicando que a operação foi pausada e que a criação de índice não foi concluída. Para obter mais informações sobre o status atual do índice podem ser obtidas [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). Como antes no caso de uma falha de um erro será emitido também. 

  
 Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>WAIT_AT_LOW_PRIORITY com operações de índice online  
  
 Para executar a instrução DDL de uma recompilação de índice online, todas as transações de bloqueio ativas em execução em uma tabela específica devem ser concluídas. Quando a recompilação de índice online for executada, ela bloqueará todas as novas transações que estão prontas para iniciar a execução nessa tabela. Embora a duração do bloqueio da recompilação de índice online seja muito curta, é possível que a espera pela conclusão de todas as transações abertas em uma tabela específica e o bloqueio das novas transações a serem iniciadas afetem significativamente a taxa de transferência, diminuindo a velocidade da carga de trabalho ou ocasionando o tempo limite da mesma, e limite consideravelmente o acesso à tabela subjacente. O **WAIT_AT_LOW_PRIORITY** opção permite que os DBAs gerenciem o bloqueio S e Sch-M bloqueios necessários para o índice online recria e permite selecionar uma das 3 opções. Em todos os casos de 3, se, durante o tempo de espera ( `(MAX_DURATION = n [minutes])` ), não há nenhuma atividade de bloqueio, a recompilação de índice online é executada imediatamente sem aguardar e a instrução DDL será concluída.  
  
## <a name="spatial-index-restrictions"></a>Restrições em índices espaciais  
 Quando você recria um índice espacial, a tabela de usuário subjacente não está disponível durante a operação do índice porque o índice espacial mantém um bloqueio de esquema.  
  
 Não é possível modificar a restrição PRIMARY KEY na tabela de usuário quando um índice espacial está definido em uma coluna dessa tabela. Para alterar a restrição PRIMARY KEY, primeiro descarte todos os índices espaciais da tabela. Depois de modificar a restrição PRIMARY KEY, é possível recriar cada um dos índices espaciais.  
  
 Em uma única operação de recriação de partição, não é possível especificar nenhum índice espacial. Entretanto, você pode especificar índices espaciais em uma recriação de partição completa.  
  
 Para alterar opções específicas a um índice espacial, como BOUNDING_BOX ou GRID, é possível usar uma instrução CREATE SPATIAL INDEX que especifique DROP_EXISTING = ON ou descartar o índice espacial e criar um novo. Para obter um exemplo, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
## <a name="data-compression"></a>Data Compression  
 Para obter mais informações sobre compactação de dados, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 Para avaliar como o alterando a compactação PAGE e ROW afetará uma tabela, um índice ou uma partição, use o [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) procedimento armazenado.  
  
 As restrições a seguir se aplicam a índices particionados:  
  
-   Quando você usa `ALTER INDEX ALL ...`, você não pode alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.  
  
-   A instrução ALTER INDEX \<índice >... REBUILD PARTITION ... recria a partição especificada do índice.  
  
-   A instrução ALTER INDEX \<índice >... REBUILD WITH... recria todas as partições do índice.  
  
## <a name="statistics"></a>Estatísticas  
 Quando você executa **ALTER INDEX ALL...** em uma tabela, somente as estatísticas associadas a índices são atualizadas. As estatísticas automáticas ou manuais criadas na tabela (em vez de um índice) não são atualizadas.  
  
## <a name="permissions"></a>Permissões  
 Para executar ALTER INDEX, no mínimo, a permissão ALTER na tabela ou exibição é necessária.  
  
## <a name="version-notes"></a>Notas de versão  
  
-   Banco de dados SQL não usa as opções de grupo de arquivos e filestream.  
  
-   Índices ColumnStore não estão disponíveis antes do SQL Server 2012. 

-  Operações de índice retomáveis estão disponível começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública) |   
  
## <a name="basic-syntax-example"></a>Exemplo de sintaxe básica:   
  
```tsql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>Exemplos: Índices de Columnstore  
 Estes exemplos se aplicam a índices columnstore.  
  
### <a name="a-reorganize-demo"></a>A. REORGANIZAR demonstração  
 Este exemplo demonstra como funciona o comando ALTER INDEX REORGANIZE.  Ele cria uma tabela que tem vários rowgroups e, em seguida, demonstra como REORGANIZAR mescla os rowgroups.  
  
```  
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
```tsql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 Use a opção TABLOCK para inserir linhas em paralelo. A operação INSERT INTO a partir do SQL Server 2016, pode executar em paralelo quando TABLOCK for usado.  
  
```tsql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 Execute este comando para ver os rowgroups delta aberto. O número de rowgroups depende do grau de paralelismo.  
  
```tsql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 Execute este comando para forçar todos os fechado e rowgroups abertos para o columnstore.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 Execute este comando novamente e você verá que os rowgroups menores são mesclados em um rowgroup compactado.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. Compactar rowgroups delta FECHADOS para o columnstore  
 Este exemplo usa o REORGANIZE opção para compacta cada rowgroup delta fechado para o columnstore como um rowgroup compactado.   Isso não é necessário, mas é útil quando o motor de tupla não compacta rowgroups CLOSED rápido o suficiente.  
  
```tsql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. Compactar todos os abertos e FECHADOS delta rowgroups do ColumnStore  
 Não é aplicável a: SQL Server 2012 e 2014  
  
 Iniciando com o SQL Server 2016, você pode executar REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON) para compactar cada rowgroup delta aberto e fechado para o columnstore como um rowgroup compactado.    Isso esvaziará o deltastore e força todas as linhas para obter compactados no columnstore. Isso é útil principalmente depois de executar várias operações de inserção, desde que essas operações armazenam as linhas de um ou mais deltastores.  
  
 REORGANIZE combina rowgroups para preencher rowgroups até um número máximo de linhas \<= 1,024,576. Portanto, ao compactar todos os rowgroups aberto e fechado você não acabará com muita rowgroups compactados que têm apenas algumas linhas neles. Você deseja que rowgroups seja tão completo quanto possível reduzir o tamanho compactado e melhorar o desempenho de consulta.  
  
```tsql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. Desfragmentar um índice columnstore online  
 Não é aplicável a: SQL Server 2012 e 2014.  
  
 Começando com o SQL Server 2016, REORGANIZE mais de compactar rowgroups delta para o columnstore. Ele também executa a desfragmentação online. Primeiro, ele reduz o tamanho do columnstore removendo fisicamente linhas excluídas quando 10% ou mais linhas em um grupo de linhas foram excluídos.  Em seguida, ele combina rowgroups para formar rowgroups maior do que ter até o máximo de 1,024,576 linhas por rowgroups.  Todos os rowgroups são alterados novamente compactados.  
  
> [!NOTE]
>  Começando com o SQL Server 2016, recriar um índice columnstore não é mais necessária na maioria das situações como REORGANIZAR fisicamente remove linhas excluídas e mescla os rowgroups. A opção COMPRESS_ALL_ROW_GROUPS força todos os rowgroups delta de aberto ou fechado para o columnstore que anteriormente só pode ser feito com uma recompilação.   REORGANIZE está online e ocorre em segundo plano para que consultas podem continuar, a operação ocorre.  
  
```tsql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. Recriar um índice columnstore clusterizado offline  
 Aplica-se a: SQL Server 2012, SQL Server 2014  
  
 Começando com o SQL Server 2016 e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], é recomendável usar ALTER INDEX REORGANIZE em vez de ALTER INDEX REBUILD.  
  
> [!NOTE]
>  No SQL Server 2012 e 2014, REORGANIZE só é usado para compactar rowgroups CLOSED para o columnstore. É a única maneira de realizar operações de desfragmentação e para forçar todos os rowgroups delta para o columnstore recriar o índice.  
  
 Este exemplo mostra como recriar um índice columnstore clusterizado e forçar todos os rowgroups delta para o columnstore. A primeira etapa prepara uma tabela FactInternetSales2 com um índice columnstore clusterizado e insere dados das quatro primeiras colunas.  
  
```tsql  
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
  
 Os resultados mostram um rowgroup aberto, o que significa que não há [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aguardará mais linhas a serem adicionadas antes de fechar o rowgroup e move os dados para o columnstore. A próxima instrução recompila o índice columnstore clusterizado, o que força todas as linhas do ColumnStore.  
  
```tsql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Os resultados da instrução SELECT mostram que o rowgroup está COMPACTADO, o que significa que os segmentos de coluna do rowgroup agora estão compactados e armazenados no columnstore.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. Recriar uma partição de um índice columnstore clusterizado offline  
 Use este formulário: SQL Server 2012, SQL Server 2014  
  
 Para recriar uma partição de um grande índice columnstore clusterizado, use ALTER INDEX REBUILD com a opção de partição. Este exemplo recria a partição 12. Começando com o SQL Server 2016, é recomendável substituir RECOMPILAÇÃO com REORGANIZE.  
  
```tsql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. Alterar um índice clusterizado columstore para usar a compactação de arquivamento  
 Não é aplicável a: SQL Server 2012  
  
 Você pode optar por reduzir o tamanho de um índice columnstore clusterizado ainda mais usando a opção de compactação de dados COLUMNSTORE_ARCHIVE. Isso é prático para dados mais antigos que você deseja manter em um armazenamento mais barato. É recomendável usar apenas isso em dados que não são acessados com frequência como descompactar é mais lenta do que a compactação COLUMNSTORE normal.  
  
 O exemplo a seguir recompila um índice columnstore clusterizado para usar a compactação de arquivamento e, em seguida, mostra como remover essa compactação. O resultado final usará apenas a compactação columnstore.  
  
```tsql  
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
  
## <a name="examples-rowstore-indexes"></a>Exemplos: Os índices Rowstore  
  
### <a name="a-rebuilding-an-index"></a>A. Recriando um índice  
 O exemplo a seguir recompila um único índice na tabela `Employee` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```tsql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. Recriando todos os índices de uma tabela e especificando opções  
 O exemplo a seguir especifica a palavra-chave `ALL`. Isso recompila todos os índices associados à tabela Production.Product no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Três opções são especificadas.  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
 O exemplo a seguir adiciona a opção ONLINE que inclui a opção de bloqueio de baixa prioridade e adiciona a opção de compactação de linha.  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.  
  
```tsql  
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
  
```tsql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. Definindo opções em um índice  
 O exemplo a seguir define várias opções no índice `AK_SalesOrderHeader_SalesOrderNumber` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2008) e o banco de dados do SQL Azure.  
  
```tsql  
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
  
```tsql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. Desabilitando restrições  
 O exemplo a seguir desabilita uma restrição PRIMARY KEY desabilitando o índice de chave primária no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados. A restrição FOREIGN KEY na tabela subjacente é automaticamente desabilitada e a mensagem de aviso é exibida.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
 O conjunto de resultados retorna esta mensagem de aviso.  
  
 ```tsql  
 Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
 on table 'EmployeeDepartmentHistory' referencing table 'Department'  
 was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
 ```  
  
### <a name="g-enabling-constraints"></a>G. Habilitando restrições  
 O exemplo a seguir habilita as restrições PRIMARY KEY e FOREIGN KEY que foram desabilitadas no exemplo F.  
  
 A restrição PRIMARY KEY é habilitada com a recriação do índice PRIMARY KEY.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
 Em seguida, a restrição FOREIGN KEY é habilitada.  
  
```tsql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. Recriando um índice particionado  
 O exemplo a seguir recompila uma única partição, número de partição `5`, do índice particionado `IX_TransactionHistory_TransactionDate` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A partição 5 é recriada online e os 10 minutos do tempo de espera para o bloqueio de baixa prioridade se aplica separadamente a cada bloqueio pela operação de recriação de índice. Se durante esse tempo o bloqueio não puder ser obtido para recriação de índice completo, a instrução da operação de recriação será anulada.  
  
**Aplica-se a**: SQL Server (começando com o SQL Server 2014) e o banco de dados do SQL Azure.  
  
```tsql  
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
  
```tsql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
 Para obter exemplos de compactação de dados adicionais, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
 
### <a name="j-online-resumable-index-rebuild"></a>J. Recompilação de índice online de retomáveis

**Aplica-se a**: começando com o SQL Server 2017 e o Azure SQL Database (recurso está em visualização pública)    

 Os exemplos a seguir mostram como usar a recompilação de índice online de reiniciável. 

1. Executar uma recriação de índice online como operação retomável com MAXDOP = 1.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. Executar o mesmo comando novamente (veja acima) após uma operação de índice foi pausada, retoma automaticamente a operação de recriação de índice.

3. Execute uma recriação de índice online como uma operação retomável com MAX_DURATION definido como 240 minutos.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. Pause uma recompilação de índice online em execução reiniciável.

   ```tsql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. Retome uma recompilação de índice online para uma recompilação de índice que foi executada como retomável operação especificando um novo valor de MAXDOP definido como 4.

   ```tsql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. Retome uma operação de recompilação de índice online para uma recompilação de índice online que foi executada como reiniciável. Definir MAXDOP para 2, o tempo de execução para o índice que está sendo executando como resmumable a 240 minutos e, no caso de um índice que está sendo bloqueado a espera de bloqueio 10 minutos e depois disso eliminar todos os bloqueadores. 

   ```tsql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. Anule a operação de recompilação de índice retomáveis que está em execução ou em pausa.

   ```tsql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Criar índice ESPACIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [Criar índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [Executar operações de índice Online](../../relational-databases/indexes/perform-index-operations-online.md)   
 [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  



