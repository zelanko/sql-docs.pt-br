---
description: CREATE COLUMNSTORE INDEX (Transact-SQL)
title: CREATE COLUMNSTORE INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs:
- TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1421ba7d2f03ecdf6f8a687e4e6d662702fe464a
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300439"
---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Converta uma tabela rowstore em um índice columnstore clusterizado ou crie um índice columnstore não clusterizado. Use um índice columnstore para executar análise operacional em tempo real com eficiência em uma carga de trabalho OLTP ou para melhorar o desempenho da consulta e a compactação de dados em cargas de trabalho de data warehouse.  
  
> [!NOTE]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar a tabela como um índice columnstore clusterizado.   Não é mais necessário criar uma tabela rowstore primeiro e, em seguida, convertê-la em um índice columnstore clusterizado.  

> [!TIP]
> Para obter informações sobre as diretrizes de design de índice, confira o [Guia de design de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md).

Acesse diretamente os exemplos:  
-   [Exemplos para converter uma tabela rowstore em columnstore](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [Exemplos de índices columnstore não clusterizados](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
Acesse diretamente os cenários:  
-   [Índices columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [Índices columnstore para data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
Saiba mais:  
-   [Guia de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [Resumo de recursos dos índices columnstore](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ] 
[ ; ]  
  
--Create a nonclustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )
    | filegroup_name
    | "default"
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name } 
    [ORDER (column [,...n] ) ]  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  

```
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

Algumas das opções não estão disponíveis em todas as versões de mecanismo de banco de dados. A tabela a seguir mostra as versões quando as opções são introduzidas nos índices CLUSTERED COLUMNSTORE e NONCLUSTERED COLUMNSTORE:

|Opção| CLUSTERED | NONCLUSTERED |
|---|---|---|
| COMPRESSION_DELAY | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] |
| DATA_COMPRESSION | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | 
| ONLINE | [!INCLUDE[ssSQLv15_md](../../includes/sssqlv15-md.md)] | [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] |
| cláusula WHERE | N/D | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] |

Todas as opções estão disponíveis no Banco de Dados SQL do Azure.

### <a name="create-clustered-columnstore-index"></a>CREATE CLUSTERED COLUMNSTORE INDEX

Crie um índice columnstore clusterizado no qual todos os dados serão compactados e armazenados por coluna. O índice inclui todas as colunas na tabela e armazena toda a tabela. Se a tabela existente for um índice de heap ou clusterizado, a tabela será convertida em um índice columnstore clusterizado. Se a tabela já estiver armazenada como um índice columnstore clusterizado, o índice existente será descartado e recriado.  
  
*index_name*  
Especifica o nome do novo índice.  
  
Se a tabela já tiver um índice columnstore clusterizado, você poderá especificar o mesmo nome que o do índice existente ou usar a opção DROP EXISTING para especificar um novo nome.  
  
ON [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*

Especifica o nome de uma, duas ou três partes da tabela a ser armazenada como um índice columnstore clusterizado. Se a tabela for um índice de heap ou clusterizado, ela será convertida de rowstore para columnstore. Se a tabela já for um columnstore, essa instrução recompilará o índice columnstore clusterizado. Para converter em um índice de repositório de coluna clusterizado ordenado, o índice existente deve ser um índice columnstore clusterizado.
  
#### <a name="with-options"></a>Opções WITH

##### <a name="drop_existing--off--on"></a>DROP_EXISTING = [OFF] | ON

   `DROP_EXISTING = ON` especifica o descarte do índice existente e a criação de um novo índice columnstore.  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH (DROP_EXISTING = ON);
```
   O padrão, DROP_EXISTING = OFF, espera que o nome do índice seja o mesmo que o nome existente. Ocorrerá um erro se o nome do índice especificado já existir.  
  
##### <a name="maxdop--max_degree_of_parallelism"></a>MAXDOP = *max_degree_of_parallelism*  
   Substitui a configuração de servidor degrau máximo de paralelismo existente enquanto durar a operação do índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
   Os valores de *max_degree_of_parallelism* podem ser:  
   - 1 - Suprima a geração de plano paralelo.  
   - \>1 – restringe o número máximo de processadores usados em uma operação de índice paralela para o número especificado ou menos, com base na carga de trabalho atual do sistema. Por exemplo, quando MAXDOP = 4, o número de processadores usados é 4 ou menos.  
   - 0 (padrão) - Use o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH (MAXDOP = 2);
```

   Para obter mais informações, confira [Configurar a opção max degree of parallelism de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md), e [Configurar operações de índice paralelas](../../relational-databases/indexes/configure-parallel-index-operations.md).  
 
###### <a name="compression_delay--0--delay--minutes-"></a>COMPRESSION_DELAY = **0** | *delay* [ Minutes ]  
   Para uma tabela baseada em disco, *delay* especifica o número mínimo de minutos que um rowgroup delta no estado CLOSED precisa permanecer no rowgroup delta antes que o SQL Server possa compactá-lo no rowgroup compactado. Uma vez que tabelas baseadas em disco não controlam tempos de inserção e atualização em linhas individuais, o SQL Server aplica o atraso a rowgroups delta no estado CLOSED.  
   O padrão é 0 minuto.  
   
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( COMPRESSION_DELAY = 10 Minutes );
```

   Para obter recomendações de quando usar COMPRESSION_DELAY, confira [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
##### <a name="data_compression--columnstore--columnstore_archive"></a>DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. As opções são as descritas a seguir:   
- `COLUMNSTORE` é o padrão e especifica compactar com a compactação de columnstore de mais alto desempenho. Essa é a opção típica.  
- `COLUMNSTORE_ARCHIVE` compacta ainda mais a tabela ou a partição para um tamanho menor. Use esta opção para situações como arquivamento, que exigem um tamanho menor de armazenamento e podem dedicar mais tempo para armazenamento e recuperação.  
  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( DATA_COMPRESSION = COLUMNSTORE_ARCHIVE );
```
   Para obter mais informações sobre compactação, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  

###### <a name="online--on--off"></a>ONLINE = [ON | OFF]
- `ON` especifica que o índice columnstore não clusterizado permaneça online e disponível enquanto a nova cópia do índice está sendo criada.
- `OFF` especifica que o índice não está disponível para ser usado enquanto a nova cópia está sendo criada.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( ONLINE = ON );
```

#### <a name="on-options"></a>Opções ON 
   Com as opções ON, você pode especificar opções de armazenamento de dados, como um esquema de partição, um grupo de arquivos específico ou o grupo de arquivos padrão. Se a opção ON não for especificada, o índice usará as configurações da partição ou do grupo de arquivos da tabela existente.  
  
   *partition_scheme_name* **(** _column_name_ **)**  
   Especifica o esquema de partição da tabela. O esquema de partição já deve existir no banco de dados. Para criar o esquema de partição, confira [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md).  
 
   *column_name* especifica a coluna na qual um índice particionado será particionado. Essa coluna precisa corresponder ao tipo de dados, ao comprimento e à precisão do argumento da função de partição que *partition_scheme_name* está usando.  

   *filegroup_name*  
   Especifica o grupo de arquivos para armazenamento do índice columnstore clusterizado. Se nenhum local for especificado e a tabela não for particionada, o índice utilizará o mesmo grupo de arquivos da exibição ou tabela subjacente. O grupo de arquivos já deve existir.  

   **"** default **"**  
   Para criar o índice no grupo de arquivos padrão, use "default" ou [ default ].  
  
   Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. QUOTED_IDENTIFIER está ON por padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
### <a name="create-nonclustered-columnstore-index"></a>CREATE [NONCLUSTERED] COLUMNSTORE INDEX  
Criar um índice columnstore não clusterizado na memória em uma tabela rowstore armazenado como um heap ou índice clusterizado. O índice pode ter uma condição filtrada e não precisa incluir todas as colunas da tabela subjacente. O índice columnstore requer espaço suficiente para armazenar uma cópia dos dados. Ele pode ser atualizado e é atualizado enquanto a tabela subjacente é alterada. O índice columnstore não clusterizado em um índice clusterizado permite a análise em tempo real.  
  
*index_name*  
   Especifica o nome do índice. O *index_name* precisa ser exclusivo na tabela, mas não precisa ser exclusivo no banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 **(** _column_  [ **,** ... *n* ] **)**  
    Especifica as colunas a serem armazenadas. Um índice columnstore não clusterizado é limitado a 1024 colunas.  
   Cada coluna deve ser de um tipo de dados com suporte para índices columnstore. Confira [Limitações e restrições](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest) para obter uma lista dos tipos de dados compatíveis.  

ON [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*  
   Especifica o nome de uma, duas ou três partes da tabela que contém o índice.  

#### <a name="with-options"></a>Opções WITH
##### <a name="drop_existing--off--on"></a>DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON O índice existente é descartado e recriado. O nome de índice especificado deve ser igual ao índice existente atualmente; no entanto, a definição de índice pode ser modificada. Por exemplo, você pode especificar colunas ou opções de índice diferentes.
  
   DROP_EXISTING = OFF Um erro será exibido se o nome do índice especificado já existir. O tipo de índice não pode ser alterado com DROP_EXISTING. Na sintaxe compatível com versões anteriores, WITH DROP_EXISTING é equivalente a WITH DROP_EXISTING = ON.  

###### <a name="maxdop--max_degree_of_parallelism"></a>MAXDOP = *max_degree_of_parallelism*  
   Substitui a opção de configuração [Configurar a opção max degree of parallelism de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) durante a operação de índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
   Os valores de *max_degree_of_parallelism* podem ser:  
   - 1 - Suprima a geração de plano paralelo.  
   - \>1 – restringe o número máximo de processadores usados em uma operação de índice paralela para o número especificado ou menos, com base na carga de trabalho atual do sistema. Por exemplo, quando MAXDOP = 4, o número de processadores usados é 4 ou menos.  
   - 0 (padrão) - Use o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
   Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]
>  As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msC](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
###### <a name="online--on--off"></a>ONLINE = [ON | OFF]   
- `ON` especifica que o índice columnstore não clusterizado permaneça online e disponível enquanto a nova cópia do índice está sendo criada.
- `OFF` especifica que o índice não está disponível para ser usado enquanto a nova cópia está sendo criada. No índice não clusterizado, a tabela base permanece disponível, apenas o índice columnstore não clusterizado não é usado para atender às consultas até que o novo índice seja concluído. 

```sql
CREATE COLUMNSTORE INDEX ncci ON Sales.OrderLines (StockItemID, Quantity, UnitPrice, TaxRate) WITH ( ONLINE = ON );
```

##### <a name="compression_delay--0--delayminutes"></a>COMPRESSION_DELAY = **0** | \<delay>[Minutos]  
   Especifica um limite inferior para o tempo em que uma linha deve permanecer no rowgroup delta antes que ela seja qualificada para migrar para o rowgroup compactado. Por exemplo, um cliente pode dizer que se uma linha for alterada para 120 minutos, ele será elegível para a compactação em formato de armazenamento colunar. Para um índice columnstore em tabelas baseadas em disco, não acompanhamos o tempo em que uma linha é inserida ou atualizada, usamos o tempo de fechamento do rowgroup delta como um proxy para a linha. A duração padrão é 0 minutos. Uma linha é migrada para o armazenamento colunar depois que 1 milhão de linhas são acumuladas no rowgroup delta e ele é marcado como fechado.  
  
###### <a name="data_compression"></a>DATA_COMPRESSION  
   Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. As opções são as descritas a seguir:
   
- `COLUMNSTORE` – o padrão e especifica compactar com a compactação de columnstore de mais alto desempenho. Essa é a opção típica.  
- `COLUMNSTORE_ARCHIVE` – COLUMNSTORE_ARCHIVE compacta ainda mais a tabela ou a partição para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.  
  
 Para obter mais informações sobre compactação, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
##### <a name="where-filter_expression--and-filter_expression-"></a>WHERE \<filter_expression> [ AND \<filter_expression> ]
  
   Chamado de predicado de filtro, especifica quais linhas devem ser incluídas no índice. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria estatísticas filtradas nas linhas de dados no índice filtrado.  
  
   O predicado de filtro usa a lógica de comparação simples. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.  
  
   Estes são alguns exemplos de predicados de filtro da tabela `Production.BillOfMaterials`:  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   Para obter diretrizes sobre índices filtrados, confira [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).  
  
#### <a name="on-options"></a>Opções ON  
   Essas opções especificam os grupos de arquivos nos quais o índice é criado.  
  
*partition_scheme_name* **(** _column_name_ **)**  
   Especifica o esquema de partição que define os grupos de arquivos para os qual as partições de um índice particionado são mapeadas. O esquema de partição precisa existir no banco de dados por meio da execução de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). 
   *column_name* especifica a coluna na qual um índice particionado será particionado. Essa coluna precisa corresponder ao tipo de dados, ao comprimento e à precisão do argumento da função de partição que *partition_scheme_name* está usando. *column_name* não é restrito às colunas na definição de índice. Ao particionar um índice columnstore, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento como uma coluna do índice, se ela já não estiver especificada.  
   Se *partition_scheme_name* ou *filegroup* não for especificado e a tabela estiver particionada, o índice será colocado no mesmo esquema de partição, usando a mesma coluna de particionamento que a tabela subjacente.  
   Um índice columnstore em uma tabela particionada deve ser alinhado por partição.  
   Para obter mais informações sobre particionamento de índices, confira [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  

*filegroup_name*  
   Especifica o nome do grupo de arquivos no qual criar o índice. Se *filegroup_name* não for especificado e a tabela não estiver particionada, o índice usará o mesmo grupo de arquivos que a tabela subjacente. O grupo de arquivos já deve existir.  
 
**"** default **"**  
Cria o índice especificado no grupo de arquivos padrão.  
  
Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e precisa ser delimitado, como em ON **"** default **"** ou ON **[** default **]** . Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="general-remarks"></a><a name="GenRemarks"></a> Comentários gerais  
Um índice columnstore pode ser criado em uma tabela temporária. Quando a tabela for removida ou a sessão encerrada, o índice também será removido.  

Um índice columnstore clusterizado e ordenado poderá ser criado em colunas de todos os tipos de dados compatíveis com o [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)], exceto em colunas de cadeia de caracteres.  
 
## <a name="filtered-indexes"></a>Índices filtrados  
Índice filtrado é um índice não clusterizado otimizado, adequado a consultas que selecionam uma pequena porcentagem de linhas de uma tabela. Ele usa um predicado de filtro para indexar uma parte dos dados na tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta, além de reduzir custos de armazenamento e de manutenção.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Opções SET necessárias para índices filtrados  
As opções SET na coluna Valor necessário são necessárias sempre que ocorrer alguma das seguintes condições:  
- Criar um índice filtrado.  
- A operação INSERT, UPDATE, DELETE ou MERGE modificar os dados de um índice filtrado.  
- O índice filtrado é usado pelo otimizador de consulta para produzir o plano de consulta.  
  
    |Opções Set|Valor obrigatório|Valor do servidor padrão|Padrão<br /><br /> Valor OLE DB e ODBC|Padrão<br /><br /> Valor da DB-Library|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ATIVADO|ATIVADO|ATIVADO|OFF|  
    |ANSI_PADDING|ATIVADO|ATIVADO|ATIVADO|OFF|  
    |ANSI_WARNINGS*|ATIVADO|ATIVADO|ATIVADO|OFF|  
    |ARITHABORT|ATIVADO|ATIVADO|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ATIVADO|ATIVADO|ATIVADO|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ATIVADO|ATIVADO|ATIVADO|OFF|   
  
     *A definição de ANSI_WARNINGS como ON definirá ARITHABORT implicitamente como ON quando o nível de compatibilidade do banco de dados for definido como 90 ou mais. Se o nível de compatibilidade do banco de dados estiver definido como 80 ou menos, a opção ARITHABORT deverá ser definida explicitamente como ON.  
  
 Se as opções SET estiverem incorretas, as seguintes condições poderão ocorrer:  
  
-   O índice filtrado não é criado.  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e reverte as instruções INSERT, UPDATE, DELETE ou MERGE que alteram os dados no índice.  
  
-   O otimizador de consulta não considera o índice no plano de execução para qualquer instrução Transact-SQL.  
  
 Para obter mais informações sobre índices filtrados, consulte [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md). 
  
##  <a name="limitations-and-restrictions"></a><a name="LimitRest"></a> Limitações e restrições  

**Cada coluna em um índice columnstore precisa ser de um dos seguintes tipos de dados de negócios comuns:** 
-   datetimeoffset [ ( *n* ) ]  
-   datetime2 [ ( *n* ) ]  
-   DATETIME  
-   smalldatetime  
-   date  
-   time [ ( *n* ) ]  
-   float [ ( *n* ) ]  
-   real [ ( *n* ) ]  
-   decimal [ ( *precision* [ *, scale* ] **)** ]
-   numeric [ ( *precision* [ *, scale* ] **)** ]    
-   money  
-   SMALLMONEY  
-   BIGINT  
-   INT  
-   SMALLINT  
-   TINYINT  
-   bit  
-   nvarchar [ ( *n* ) ] 
-   nvarchar (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e à camada Premium, à camada Standard (S3 e posterior) e a todas as camadas de ofertas de vCore, apenas em índices columnstore clusterizados)   
-   nchar [ ( *n* ) ]  
-   varchar [ ( *n* ) ]  
-   varchar (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e à camada Premium, à camada Standard (S3 e posterior) e a todas as camadas de ofertas de vCore, apenas em índices columnstore clusterizados)
-   char [ ( *n* ) ]  
-   varbinary [ ( *n* ) ] 
-   varbinary (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e ao Banco de Dados SQL do Azure na camada Premium, na camada Standard (S3 e posterior) e a todas as camadas de ofertas de vCore, apenas em índices columnstore clusterizados)
-   binary [ ( *n* ) ]  
-   uniqueidentifier (aplica-se ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posteriores)
  
Se a tabela subjacente tiver uma coluna de um tipo de dados não compatível com índices columnstore, omita essa coluna do índice columnstore não clusterizado.  
  
**As colunas que usam um dos seguintes tipos de dados não podem ser incluídas em um índice columnstore:**
-   ntext, texto e imagem  
-   nvarchar(max), varchar(max) e varbinary(max) (aplica-se ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e às versões anteriores e a índices columnstore não clusterizados) 
-   rowversion (e carimbo de data/hora)  
-   sql_variant  
-   Tipos CLR (hierarchyid e tipos espaciais)  
-   Xml  
-   uniqueidentifier (aplica-se ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**Índices columnstore não clusterizados:**
-   Não pode ter mais de 1024 colunas.
-   Não pode ser criado como um índice baseado em restrição. É possível ter restrições exclusivas, restrições de chave primária e restrições de chave estrangeira em uma tabela com um índice columnstore. As restrições sempre são impostas com um índice de repositório de linha. As restrições não podem ser impostas com um índice columnstore (clusterizado ou não clusterizado).
-   Não pode incluir uma coluna esparsa.  
-   Não pode ser alterado usando a instrução **ALTER INDEX** . Para alterar o índice não clusterizado, é preciso descartar e recriar o índice columnstore. Você pode usar **ALTER INDEX** para desabilitar e recompilar um índice columnstore.  
-   Ele não pode ser criado usando a palavra-chave **INCLUDE** .  
-   Não é possível incluir as palavras-chave **ASC** ou **DESC** para classificar o índice. Os índices columnstore são ordenados de acordo com os algoritmos de compactação. A classificação eliminará muitos dos benefícios de desempenho.  
-   Não é possível incluir colunas de LOB (objeto grande) do tipo nvarchar(max), varchar(max) e varbinary(max) em índices de repositório de colunas não clusterizados. Somente índices columnstore clusterizados são compatíveis com tipos LOB, começando com a versão [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o Banco de Dados SQL do Azure configurado na camada Premium, na camada Standard (S3 e posterior) e em todas as camadas de ofertas de vCore. Observe que as versões anteriores não são compatíveis com os tipos LOB em índices columnstore clusterizados e não clusterizados.


> [!NOTE]  
> Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante, é possível criar um índice columnstore não clusterizado em uma exibição indexada.  


 **Os índices columnstore não podem ser combinados com os seguintes recursos:**  
-   Colunas computadas. Começando com o SQL Server 2017, um índice columnstore clusterizado pode conter uma coluna computada não persistente. No entanto, no SQL Server 2017, os índices columnstore clusterizados não podem conter colunas computadas persistentes e não é possível criar índices não clusterizados em colunas computadas. 
-   Compactação de página e de linha e o formato de armazenamento **vardecimal** (um índice columnstore já é compactado em um formato diferente.)  
-   Replicação  
-   Fluxo de arquivos

Não é possível usar cursores nem gatilhos em uma tabela com um índice columnstore clusterizado. Essa restrição não se aplica a índices columnstore não clusterizados. É possível usar cursores e gatilhos em uma tabela com um índice columnstore não clusterizado.

**Limitações específicas do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**  
Estas limitações se aplicam apenas ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Nesta versão, foram introduzidos os índices columnstore clusterizados atualizáveis. Os índices columnstore não clusterizados ainda eram somente leitura.  

-   Controle de alterações. Você não pode usar o controle de alterações com índices columnstore.  
-   Captura de dados de alterações. Não é possível usar a captura de dados de alterações em NCCI (índices columnstore não clusterizado) porque eles são somente leitura. Mas funciona para CCI (índices columnstore clusterizados).  
-   Secundário legível. Não é possível acessar um CCI (índice columnstore clusterizado) de um secundário legível de um grupo de disponibilidade Always On legível.  É possível acessar um NCCI (índice columnstore não clusterizado) de um secundário legível.  
-   MARS (conjunto de resultados ativos múltiplos). O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] usa o MARS para conexões somente leitura com tabelas que contenham um índice columnstore. No entanto, o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] não é compatível com o MARS para operações de DML (linguagem de manipulação de dados) simultâneas em uma tabela com um índice columnstore. Quando isso ocorre, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encerra as conexões e anula as transações.  
-  Os índices columnstore não clusterizados não podem ser criados em uma exibição ou exibição indexada.
  
 Para obter informações sobre os benefícios de desempenho e as limitações dos índices columnstore, confira [Visão geral de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
##  <a name="metadata"></a><a name="Metadata"></a> Metadados  
 Todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave. Essas exibições do sistema fornecem informações sobre índices columnstore.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="examples-for-converting-a-rowstore-table-to-columnstore"></a><a name="convert"></a> Exemplos para converter uma tabela rowstore em columnstore  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>a. Converter um índice columnstore clusterizado  
 Este exemplo cria uma tabela como um heap e, depois, converte-o em um índice columnstore clusterizado chamado o cci_Simple. Isso altera o armazenamento da tabela inteira, de rowstore a columnstore.  
  
```sql  
CREATE TABLE SimpleTable(  
    ProductKey [INT] NOT NULL,   
    OrderDateKey [INT] NOT NULL,   
    DueDateKey [INT] NOT NULL,   
    ShipDateKey [INT] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. Converta um índice clusterizado em um índice columnstore clusterizado com o mesmo nome.  
 Este exemplo cria uma tabela com um índice clusterizado e, em seguida, demonstra a sintaxe de conversão do índice clusterizado em índice columnstore clusterizado. Isso altera o armazenamento da tabela inteira, de rowstore a columnstore.  
  
```sql  
CREATE TABLE SimpleTable (  
    ProductKey [INT] NOT NULL,   
    OrderDateKey [INT] NOT NULL,   
    DueDateKey [INT] NOT NULL,   
    ShipDateKey [INT] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. Tratar índices não clusterizados ao converter uma tabela rowstore em um índice columnstore.  
 Este exemplo mostra como tratar os índices não clusterizados ao converter uma tabela rowstore em um índice columnstore. Na verdade, começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nenhuma ação especial é necessária, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define e recompila automaticamente os índices não clusterizados no novo índice columnstore clusterizado.  
  
 Se você desejar remover os índices não clusterizados, use a instrução DROP INDEX antes de criar o índice columnstore. A opção DROP EXISTING remove somente o índice clusterizado que está sendo convertido. Ela não descarta os índices não clusterizados.  
  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], não era possível criar um índice não clusterizado em um índice columnstore. Este exemplo mostra como nas versões anteriores era necessário remover os índices não clusterizados antes de criar o índice columnstore.  
  
```sql  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [INT] NOT NULL,   
    OrderDateKey [INT] NOT NULL,   
    DueDateKey [INT] NOT NULL,   
    ShipDateKey [INT] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. Converter uma tabela de fatos grande do rowstore em columnstore  
 Este exemplo explica como converter uma tabela de fatos grande de uma tabela rowstore em uma tabela columnstore.  
  
 Para converter uma tabela rowstore em uma tabela columnstore.  
  
1.  Primeiro, crie uma pequena tabela a ser usada neste exemplo.  
  
    ```sql  
    --Create a rowstore table with a clustered index and a nonclustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [INT] NOT NULL,  
        OrderDateKey [INT] NOT NULL,  
         DueDateKey [INT] NOT NULL,  
         ShipDateKey [INT] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a nonclustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  Remova todos os índices não clusterizados da tabela rowstore.  
  
    ```sql  
    --Drop all nonclustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  Descarte o índice clusterizado.  
  
    -   Faça isso somente se desejar especificar um novo nome para o índice quando ele for convertido em um índice columnstore clusterizado. Se você não remover o índice clusterizado, o novo índice columnstore clusterizado terá o mesmo nome.  
  
        > [!NOTE]  
        > Pode ser mais fácil lembrar o nome do índice se você usar seu próprio nome. Todos os índices clusterizados da rowstore usam o nome padrão que é "ClusteredIndex_\<GUID>".  
  
    ```sql  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name 'ClusteredIndex_<GUID>'.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  Converta a tabela rowstore em uma tabela columnstore com um índice columnstore clusterizado.  
  
    ```sql  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. Converter uma tabela columnstore em uma tabela rowstore com um índice clusterizado  
 Para converter uma tabela columnstore em uma tabela rowstore com um índice clusterizado, use a instrução CREATE INDEX com a opção DROP_EXISTING.  
  
```sql  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. Converter uma tabela columnstore em um heap rowstore  
 Para converter uma tabela columnstore em um heap rowstore, basta remover o índice columnstore clusterizado.  
  
```sql  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. Desfragmentar recompilando o índice columnstore clusterizado inteiro  
   Aplica-se a: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Há duas maneiras de recriar o índice columnstore clusterizado completo. Você pode usar CREATE CLUSTERED COLUMNSTORE INDEX ou [ALTER INDEX &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-index-transact-sql.md) e a opção REBUILD. Ambos os métodos geram os mesmos resultados.  
  
> [!NOTE]  
> A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], use `ALTER INDEX...REORGANIZE` em vez de reconstruir com os métodos descritos neste exemplo.  
  
```sql  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
```  
  
##  <a name="examples-for-nonclustered-columnstore-indexes"></a><a name="nonclustered"></a> Exemplos de índices columnstore não clusterizados  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>a. Criar um índice columnstore como um índice secundário em uma tabela rowstore  
 Este exemplo cria um índice columnstore não clusterizado em uma tabela rowstore. Somente um índice columnstore pode ser criado nesta situação. O índice columnstore exige armazenamento extra, pois contém uma cópia dos dados na tabela rowstore. Este exemplo cria uma tabela simples e um índice clusterizado e, em seguida, demonstra a sintaxe de criação de um índice columnstore não clusterizado.  
  
```sql  
CREATE TABLE SimpleTable  
(ProductKey [INT] NOT NULL,   
OrderDateKey [INT] NOT NULL,   
DueDateKey [INT] NOT NULL,   
ShipDateKey [INT] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>B. Criar um índice columnstore não clusterizado simples usando todas as opções  
 O exemplo a seguir demonstra a sintaxe de criação de um índice columnstore não clusterizado usando todas as opções.  
  
```sql  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 Para obter um exemplo mais complexo do uso de tabelas particionadas, confira [Visão geral de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. Criar um índice columnstore não clusterizado com um predicado filtrado  
 O exemplo a seguir cria um índice columnstore não clusterizado filtrado na tabela Production.BillOfMaterials no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O predicado de filtro pode incluir colunas que não sejam de chave no índice filtrado. O predicado deste exemplo seleciona apenas as linhas em que EndDate é não NULL.  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
###  <a name="d-change-the-data-in-a-nonclustered-columnstore-index"></a><a name="ncDML"></a> D. Alterar os dados em um índice columnstore não clusterizado  
   Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].
  
 Quando você cria um índice columnstore não clusterizado em uma tabela, não pode modificar diretamente os dados nessa tabela. Uma consulta com INSERT, UPDATE, DELETE ou MERGE falhará e retornará uma mensagem de erro. Para adicionar ou modificar os dados na tabela, siga um destes procedimentos:  
  
-   Desabilitar ou descartar o índice columnstore. Depois, você pode atualizar os dados na tabela. Se você desabilitar o índice columnstore, poderá recriar o índice columnstore quando concluir a atualização dos dados. Por exemplo,  
  
    ```sql  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Carregar dados em uma tabela de preparação sem um índice columnstore. Criar um índice columnstore na tabela de preparo. Alternar a tabela de preparo para uma partição vazia da tabela principal.  
  
-   Alternar uma partição da tabela com o índice columnstore para uma tabela de preparo vazia. Se houver um índice columnstore na tabela de preparo, desabilite o índice columnstore. Executar quaisquer atualizações. Criar (ou recriar) o índice columnstore. Alternar a tabela de preparo para a partição anterior (não vazia) da tabela principal.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>a. Alterar um índice clusterizado para um índice columnstore clusterizado  
 Usando a instrução CREATE CLUSTERED COLUMNSTORE INDEX com DROP_EXISTING = ON, você pode:  
  
-   Alterar um índice clusterizado para um índice columnstore clusterizado.  
  
-   Recompilar um índice columnstore clusterizado.  
  
 Este exemplo cria a tabela xDimProduct como uma tabela rowstore com um índice clusterizado e, em seguida, usa CREATE CLUSTERED COLUMNSTORE INDEX para alterar a tabela de uma tabela rowstore para uma tabela columnstore.  
  
```sql  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. Recompilar um índice columnstore clusterizado  
 Com base no exemplo anterior, este exemplo usa CREATE CLUSTERED COLUMNSTORE INDEX para recompilar o índice columnstore clusterizado existente chamado cci_xDimProduct.  
  
```sql  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. Alterar o nome de um índice columnstore clusterizado  
 Para alterar o nome de um índice columnstore clusterizado, remova o índice columnstore clusterizado existente e, em seguida, recrie o índice com um novo nome.  
  
 É recomendável fazer esta operação somente com uma tabela pequena ou uma tabela vazia. Demora muito para remover um índice columnstore clusterizado grande e a recompilá-lo com um nome diferente.  
  
 Usando o índice columnstore clusterizado cci_xDimProduct do exemplo anterior, este exemplo descarta o índice columnstore clusterizado cci_xDimProduct e, em seguida, recria o índice columnstore clusterizado com o nome mycci_xDimProduct.  
  
```sql  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. Converter uma tabela columnstore em uma tabela rowstore com um índice clusterizado  
 É possível que haja uma situação em você deseje remover um índice columnstore clusterizado e criar um índice clusterizado. Isso armazena a tabela no formato rowstore. Este exemplo converte uma tabela columnstore em uma tabela rowstore com um índice clusterizado com o mesmo nome. Nenhum dos dados é perdido. Todos os dados vão para a tabela rowstore e as colunas listadas tornam-se as colunas de chave no índice clusterizado.  
  
```sql  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. Converter uma tabela columnstore novamente em um heap rowstore  
 Use [DROP INDEX (SQL Server PDW)](drop-index-transact-sql.md) para remover o índice columnstore clusterizado e converter a tabela em um heap rowstore. Este exemplo converte a tabela cci_xDimProduct em um heap rowstore. A tabela continua a ser distribuída, mas é armazenada como um heap.  
  
```sql  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  

### <a name="f-create-an-ordered-clustered-columnstore-index-on-a-table-with-no-index"></a>F. Criar um índice columnstore clusterizado ordenado na tabela sem índice

```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE );
```

### <a name="g-convert-a-clustered-columnstore-index-to-an-ordered-clustered-columnstore-index"></a>G. Converter um índice columnstore clusterizado em um índice columnstore clusterizado com ordenado

```sql  
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE );
WITH (DROP_EXISTING = ON)
```

### <a name="h-add-a-column-to-the-ordering-of-an-ordered-clustered-columnstore-index"></a>H. Adicionar uma coluna à ordenação de um índice columnstore clusterizado ordenado

```sql
-- The original ordered clustered columnstore index was ordered on SHIPDATE column only.  Add PRODUCTKEY column to the ordering.
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE, PRODUCTKEY );
WITH (DROP_EXISTING = ON)
```
### <a name="i-change-the-ordinal-of-ordered-columns"></a>I. Alterar o ordinal de colunas ordenadas  
```sql
-- The original ordered clustered columnstore index was ordered on SHIPDATE, PRODUCTKEY.  Change the ordering to PRODUCTKEY, SHIPDATE.  
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( PRODUCTKEY,SHIPDATE );
WITH (DROP_EXISTING = ON)
```