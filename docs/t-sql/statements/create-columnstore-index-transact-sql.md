---
title: "CRIAR um índice COLUMNSTORE (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 76
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 0fb8883678dad7a62cac9c2109b093ee79e27b27
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Converter uma tabela rowstore em um índice columnstore clusterizado ou criar um índice columnstore não clusterizado. Use um índice columnstore para executar análise operacional em tempo real com eficiência em uma carga de trabalho OLTP ou para melhorar o desempenho de consulta e compactação de dados de data warehouse cargas de trabalho.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar a tabela como um índice columnstore clusterizado.   Não é necessário criar primeiro uma tabela rowstore e convertê-lo para um índice columnstore clusterizado.  
  
Vá para exemplos:  
-   [Exemplos para converter uma tabela rowstore em columnstore](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [Exemplos de índices columnstore não clusterizados](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
Vá para cenários:  
-   [Índices ColumnStore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [Índices ColumnStore para data warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
Saiba Mais:  
-   [Guia de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [Resumo de recursos de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
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
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name   
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
CREATE CLUSTERED COLUMNSTORE INDEX  
Crie um índice columnstore clusterizado no qual todos os dados são compactados e armazenados por coluna. O índice inclui todas as colunas na tabela e armazena toda a tabela. Se a tabela existente for um heap ou índice clusterizado, a tabela é convertida em um índice columnstore clusterizado. Se a tabela já estiver armazenada como um índice columnstore clusterizado, o índice existente é descartado e recriado.  
  
*index_name*  
Especifica o nome para o novo índice.  
  
Se a tabela já tiver um índice columnstore clusterizado, você pode especificar o mesmo nome que o índice existente, ou você pode usar a opção DROP EXISTING para especificar um novo nome.  
  
ON [*database_name*. [*schema_name* ]. | *schema_name* . ] *table_name*  
   Especifica o nome de uma, duas ou três partes da tabela a ser armazenada como um índice columnstore clusterizado. Se a tabela for um heap ou índice clusterizado de tabela é convertido de rowstore em columnstore. Se a tabela já está columnstore, essa instrução recria o índice columnstore clusterizado.  
  
com  
DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON especifica para descartar o índice columnstore clusterizado existente e criar um novo índice columnstore.  

   O padrão, DROP_EXISTING = OFF espera que o nome do índice é o mesmo que o nome existente. Ocorre um erro é o nome do índice especificado já existe.  
  
MAXDOP = *max_degree_of_parallelism*  
   Substitui a configuração de servidor degrau máximo de paralelismo existente enquanto durar a operação do índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
   *max_degree_of_parallelism* valores podem ser:  
   - 1 - Suprima a geração de plano paralelo.  
   - \>1 - restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema. Por exemplo, quando MAXDOP = 4, o número de processadores usados será 4 ou menos.  
   - 0 (padrão) - Use o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
   Para obter mais informações, consulte [configurar o grau máximo de paralelismo opção de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md), e [configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
 
COMPRESSION_DELAY = **0** | *atraso* [minutos]  
   Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

   Para uma tabela baseada em disco, *atraso* Especifica o número mínimo de minutos que um rowgroup delta no estado CLOSED deve permanecer no rowgroup delta antes do SQL Server pode compactá-las no rowgroup compactado. Como as tabelas baseadas em disco não controlar inserir e atualizar horários em linhas individuais, o SQL Server aplica o atraso para rowgroups delta no estado fechado.  
   O padrão é 0 minutos.  
   Para obter recomendações sobre quando usar COMPRESSION_DELAY, consulte [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. As opções são as seguintes:   
COLUMNSTORE  
   COLUMNSTORE é o padrão e especifica para compactar com a maior compactação columnstore de alto desempenho. Essa é a opção típica.  
  
COLUMNSTORE_ARCHIVE  
   COLUMNSTORE_ARCHIVE mais compacta a tabela ou partição para um tamanho menor. Use esta opção para situações como arquivamento que exijam um tamanho menor de armazenamento e possam dispensar mais tempo para armazenamento e recuperação.  
  
   Para obter mais informações sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  

ON  
   Com as opções ON, você pode especificar opções de armazenamento de dados, como um esquema de partição, um grupo de arquivos específico ou o grupo de arquivos padrão. Se a opção ON não for especificada, o índice usa as configurações de partição ou grupo de arquivos de configurações da tabela existente.  
  
   *partition_scheme_name* **(** *column_name* **)**  
   Especifica o esquema de partição da tabela. O esquema de partição já deve existir no banco de dados. Para criar o esquema de partição, consulte [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md).  
 
   *nome da coluna* Especifica a coluna na qual um índice particionado será particionado. Esta coluna deve corresponder ao tipo de dados, comprimento e precisão do argumento da partição de função que *partition_scheme_name* está usando.  

   *filegroup_name*  
   Especifica o grupo de arquivos para armazenamento do índice columnstore clusterizado. Se nenhum local for especificado e a tabela não for particionada, o índice utilizará o mesmo grupo de arquivos da exibição ou tabela subjacente. O grupo de arquivos já deve existir.  

   **"**padrão**"**  
   Para criar o índice no grupo de arquivos padrão, use "padrão" ou [padrão].  
  
   Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. QUOTED_IDENTIFIER está ON por padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
CRIAR UM ÍNDICE COLUMNSTORE [CLUSTER]  
Criar um índice columnstore não clusterizado na memória em uma tabela rowstore armazenado como um heap ou índice clusterizado. O índice pode ter uma condição filtrada e não precisa incluir todas as colunas da tabela subjacente. O índice columnstore requer espaço suficiente para armazenar uma cópia dos dados. Ele pode ser atualizado e foi atualizado enquanto a tabela subjacente é alterada. O índice columnstore não clusterizado em um índice clusterizado habilita a análise em tempo real.  
  
*index_name*  
   Especifica o nome do índice. *index_name* devem ser exclusivos dentro da tabela, mas não precisa ser exclusivo no banco de dados. Os nomes de índice devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 **(** *coluna* [ **,**... *n* ] **)**  
    Especifica as colunas a serem armazenadas. Um índice não clusterizado columnstore é limitado a 1024 colunas.  
   Cada coluna deve ser de um tipo de dados com suporte para índices columnstore. Consulte [limitações e restrições](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest) para obter uma lista dos tipos de dados com suporte.  

ON [*database_name*. [*schema_name* ]. | *schema_name* . ] *table_name*  
   Especifica a uma, duas ou nome de três partes da tabela que contém o índice.  

COM DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON, o índice existente é removido e recriado. O nome de índice especificado deve ser igual ao índice existente atualmente; no entanto, a definição de índice pode ser modificada. Por exemplo, você pode especificar colunas ou opções de índice diferentes.
  
   DROP_EXISTING = OFF, um erro será exibido se o nome do índice especificado já existe. O tipo de índice não pode ser alterado com DROP_EXISTING. Na sintaxe compatível com versões anteriores, WITH DROP_EXISTING é equivalente a WITH DROP_EXISTING = ON.  

MAXDOP = *max_degree_of_parallelism*  
   Substitui o [configurar o grau máximo de paralelismo opção de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) opção de configuração para a duração da operação de índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
   *max_degree_of_parallelism* valores podem ser:  
   - 1 - Suprima a geração de plano paralelo.  
   - \>1 - restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema. Por exemplo, quando MAXDOP = 4, o número de processadores usados será 4 ou menos.  
   - 0 (padrão) - Use o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
   Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
ONLINE = [ON | OFF]   
   Aplica-se a: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], em apenas índices columnstore não clusterizado.
ON Especifica que o índice não clusterizado columnstore permaneça online e disponível enquanto a nova cópia do índice está sendo criado.

   Desativar Especifica que o índice não está disponível para uso, enquanto a nova cópia está sendo construída. Como esse é um índice não clusterizado, o permanece de tabela base disponível, que apenas o índice columnstore não clusterizado não é usado para atender consultas até que o novo índice seja concluído. 

COMPRESSION_DELAY = **0** | \<atraso > [minutos]  
   Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
   Especifica um limite inferior em quanto tempo uma linha deve permanecer no rowgroup delta antes que seja qualificado para migração para o grupo de linhas compactado. Por exemplo, um cliente pode dizer que se uma linha for alterada para 120 minutos, torná-la elegível para a compactação em formato de armazenamento Colunar. Para um índice columnstore em tabelas baseadas em disco, nós não rastrear o tempo quando uma linha foi inserida ou atualizada, usamos o delta rowgroup fechado tempo como um proxy para a linha em vez disso. A duração padrão é 0 minutos. Uma linha é migrada para o armazenamento Colunar depois que foram acumulado 1 milhão de linhas no rowgroup delta e ele foi marcado como fechado.  
  
DATA_COMPRESSION  
   Especifica a opção de compactação de dados para a tabela, o número de partição ou o intervalo de partições especificado. As opções são as seguintes:  
COLUMNSTORE  
   Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE é o padrão e especifica para compactar com a maior compactação columnstore de alto desempenho. Essa é a opção típica.  
  
COLUMNSTORE_ARCHIVE  
   Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Aplica-se somente a índices columnstore, incluindo índices columnstore não clusterizados e clusterizados. COLUMNSTORE_ARCHIVE mais compacta a tabela ou partição para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação.  
  
 Para obter mais informações sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
ONDE \<filter_expression > [AND \<filter_expression >] aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
   Chamado um predicado de filtro, especifica quais linhas devem ser incluídas no índice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]cria estatísticas filtradas nas linhas de dados no índice filtrado.  
  
   O predicado de filtro usa a lógica de comparação simples. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.  
  
   Estes são alguns exemplos de predicados de filtro da tabela `Production.BillOfMaterials`:  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   Para obter orientação sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).  
  
ON  
   Essas opções especificam os grupos de arquivos no qual o índice é criado.  
  
*partition_scheme_name* **(** *column_name* **)**  
   Especifica o esquema de partição que define os grupos de arquivos no qual as partições de um índice particionado é mapeado. O esquema de partição deve existir no banco de dados executando [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). 
   *nome da coluna* Especifica a coluna na qual um índice particionado será particionado. Esta coluna deve corresponder ao tipo de dados, comprimento e precisão do argumento da partição de função que *partition_scheme_name* está usando. *nome da coluna* não é restrito às colunas na definição do índice. Ao particionar um índice columnstore, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento como uma coluna do índice, se ela já não estiver especificada.  
   Se *partition_scheme_name* ou *arquivos* não for especificado e a tabela estiver particionada, o índice será colocado no mesmo esquema de partição, usando a mesma coluna de particionamento da tabela subjacente.  
   Um índice columnstore em uma tabela particionada deve ser alinhado por partição.  
   Para obter mais informações sobre particionamento de índices, consulte [tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  

*filegroup_name*  
   Especifica o nome do grupo de arquivos no qual criar o índice. Se *filegroup_name* não for especificado e a tabela não estiver particionada, o índice usa o mesmo grupo de arquivos da tabela subjacente. O grupo de arquivos já deve existir.  
 
**"**padrão**"**  
Cria o índice especificado no grupo de arquivos padrão.  
  
Nesse contexto, default não é uma palavra-chave. Ele é um identificador para o grupo de arquivos padrão e deve ser delimitado, como em ON **"**padrão**"** ou ON **[**padrão**]**. Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
##  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="GenRemarks"></a>Comentários gerais  
 Um índice columnstore pode ser criado em uma tabela temporária. Quando a tabela for removida ou a sessão encerrada, o índice também será removido.  
 
## <a name="filtered-indexes"></a>Índices filtrados  
Índice filtrado é um índice não clusterizado otimizado, adequado a consultas que selecionam uma pequena porcentagem de linhas de uma tabela. Ele usa um predicado de filtro para indexar uma parte dos dados na tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta, além de reduzir custos de armazenamento e de manutenção.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Opções SET necessárias para índices filtrados  
As opções SET na coluna Valor necessário são necessárias sempre que ocorrer alguma das seguintes condições:  
- Criar um índice filtrado.  
- A operação INSERT, UPDATE, DELETE ou MERGE modificar os dados de um índice filtrado.  
- O índice filtrado é usado pelo otimizador de consulta para produzir o plano de consulta.  
  
    |Opções Set|Valor Obrigatório|Valor do servidor padrão|Padrão<br /><br /> Valor OLE DB e ODBC|Padrão<br /><br /> Valor da DB-Library|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *A definição de ANSI_WARNINGS como ON definirá ARITHABORT implicitamente como ON quando o nível de compatibilidade do banco de dados for definido como 90 ou mais. Se o nível de compatibilidade do banco de dados estiver definido como 80 ou menos, a opção ARITHABORT deverá ser definida explicitamente como ON.  
  
 Se as opções SET estiverem incorretas, as seguintes condições poderão ocorrer:  
  
-   O índice filtrado não é criado.  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e reverte as instruções INSERT, UPDATE, DELETE ou MERGE que alteram os dados no índice.  
  
-   O otimizador de consulta não considera o índice no plano de execução para qualquer instrução Transact-SQL.  
  
 Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md). 
  
##  <a name="LimitRest"></a> Limitações e restrições  

**Cada coluna em um índice columnstore deve ser de um dos seguintes tipos de dados de negócios comuns:** 
-   DateTimeOffset [(  *n*  )]  
-   datetime2 [(  *n*  )]  
-   datetime  
-   smalldatetime  
-   date  
-   tempo [(  *n*  )]  
-   float [(  *n*  )]  
-   real [(  *n*  )]  
-   decimal [( *precisão* [ *, escala* ] **)** ]
-   numérico [( *precisão* [ *, escala* ] **)** ]    
-   money  
-   smallmoney  
-   bigint  
-   int  
-   smallint  
-   tinyint  
-   bit  
-   nvarchar [(  *n*  )] 
-   nvarchar (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o banco de dados SQL Azure no premium preço, em índices columnstore clusterizados apenas)   
-   nchar [(  *n*  )]  
-   varchar [(  *n*  )]  
-   varchar (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o banco de dados SQL Azure no premium preço, em índices columnstore clusterizados apenas)
-   char [(  *n*  )]  
-   varbinary [(  *n*  )] 
-   varbinary (max) (aplica-se a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o banco de dados SQL Azure no premium preço, em índices columnstore clusterizados apenas)
-   binário [(  *n*  )]  
-   Identificador exclusivo (aplica-se a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior)
  
Se a tabela subjacente tiver uma coluna de um tipo de dados que não há suporte para índices columnstore, você deve omitir a coluna do índice columnstore não clusterizado.  
  
**Colunas que usam qualquer um dos seguintes tipos de dados não podem ser incluídas em um índice columnstore:**
-   ntext, texto e imagem  
-   nvarchar (max), varchar (max) e varbinary (max) (aplica-se a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e as versões anteriores e índices columnstore não clusterizados) 
-   rowversion (e carimbo de data/hora)  
-   sql_variant  
-   Tipos CLR (hierarchyid e tipos espaciais)  
-   xml  
-   Identificador exclusivo (aplica-se a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**Índices columnstore não clusterizado:**
-   Não pode ter mais de 1024 colunas.  
-   Uma tabela com um índice columnstore não clusterizado pode ter restrições exclusivas, restrições de chave primária ou restrições de chave estrangeira, mas as restrições não podem ser incluídas no índice columnstore não clusterizado.  
-   Não pode ser criado em uma exibição ou exibição indexada.  
-   Não pode incluir uma coluna esparsa.  
-   Não pode ser alterado usando o **ALTER INDEX** instrução. Para alterar o índice não clusterizado, é preciso descartar e recriar o índice columnstore. Você pode usar **ALTER INDEX** para desabilitar e recriar um índice columnstore.  
-   Não pode ser criado usando o **incluir** palavra-chave.  
-   Não é possível incluir o **ASC** ou **DESC** palavras-chave para o índice de classificação. Os índices columnstore são ordenados de acordo com os algoritmos de compactação. A classificação eliminará muitos dos benefícios de desempenho.  
-   Não é possível incluir colunas de objeto grande (LOB) do tipo nvarchar (max), varchar (max) e varbinary (max) em índices de repositório de coluna não clusterizado. Somente índices columnstore clusterizados oferecem suporte a tipos de LOB, a partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] versão e o banco de dados do SQL Azure configurado no preço premium. Observe que as versões anteriores não dão suporte a tipos LOB em índices columnstore clusterizados e não clusterizados.


 **Índices ColumnStore não podem ser combinados com os seguintes recursos:**  
-   Colunas computadas. Começando com o SQL Server 2017, um índice columnstore clusterizado pode conter uma coluna computada não persistente. No entanto, no SQL Server de 2017, índices columnstore clusterizados não podem conter colunas computadas persistentes e não podem ser criados índices não clusterizados em colunas computadas. 
-   Compactação de página e de linha, e **vardecimal** o formato de armazenamento (um índice columnstore já é compactado em um formato diferente.)  
-   Replicação  
-   Fluxo de arquivos

Você não pode usar cursores ou gatilhos em uma tabela com um índice columnstore clusterizado. Essa restrição não se aplica a índices columnstore não clusterizado; Você pode usar cursores e gatilhos em uma tabela com um índice columnstore não clusterizado.

**Limitações específicas do SQL Server 2014**  
Essas limitações se aplicam somente ao SQL Server 2014. Nesta versão, apresentamos índices columnstore clusterizados atualizáveis. Índices columnstore não clusterizados foram ainda somente leitura.  

-   Controle de alterações. Você não pode usar o controle de alterações com índices columnstore não clusterizado (NCCI) porque eles são somente leitura. Ele funciona para índices columnstore clusterizados (CCI).  
-   O Change data capture. Você não pode usar o change data capture para índice columnstore não clusterizado (NCCI) porque eles são somente leitura. Ele funciona para índices columnstore clusterizados (CCI).  
-   Secundária legível. Você não pode acessar um índice clusterizado columnstore clusterizado (CCI) de um secundário legível de um grupo de disponibilidade sempre OnReadable.  Você pode acessar um índice columnstore não clusterizado (NCCI) de um secundário legível.  
-   Vários conjuntos de resultados ativos (MARS). SQL Server 2014 usa MARS para conexões somente leitura para tabelas com um índice columnstore.    No entanto, SQL Server 2014 não dá suporte a MARS para operações de DML (linguagem) de manipulação de dados simultâneas em uma tabela com um índice columnstore. Quando isso ocorrer, o SQL Server encerra as conexões e anula as transações.  
  
 Para obter informações sobre os benefícios de desempenho e as limitações de índices columnstore, consulte [visão geral de índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
##  <a name="Metadata"></a> Metadados  
 Todas as colunas em um índice columnstore são armazenadas nos metadados como colunas incluídas. O índice columnstore não tem colunas de chave. Essas exibições do sistema fornecem informações sobre índices columnstore.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>Exemplos para converter uma tabela rowstore em columnstore  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>A. Converter um índice columnstore clusterizado  
 Este exemplo cria uma tabela como um heap e, depois, converte-o em um índice columnstore clusterizado chamado o cci_Simple. Isso altera o armazenamento da tabela inteira, de rowstore a columnstore.  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. Converta um índice clusterizado em um índice columnstore clusterizado com o mesmo nome.  
 Este exemplo cria uma tabela com um índice clusterizado e, em seguida, demonstra a sintaxe de conversão do índice clusterizado em índice columnstore clusterizado. Isso altera o armazenamento da tabela inteira, de rowstore a columnstore.  
  
```  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. Ao converter uma tabela rowstore em um índice columnstore, lidar com índices não clusterizados.  
 Este exemplo mostra como tratar os índices não clusterizados ao converter uma tabela rowstore em um índice columnstore. Na verdade, começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nenhuma ação especial é necessária; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define automaticamente e recria os índices não clusterizados no novo índice columnstore clusterizado.  
  
 Se você deseja descartar os índices não clusterizados, use a instrução DROP INDEX antes de criar o índice columnstore. A opção DROP EXISTING remove somente o índice clusterizado que está sendo convertido. Ele não descarta os índices não clusterizados.  
  
 Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], você não pode criar um índice não clusterizado em um índice columnstore. Este exemplo mostra como nas versões anteriores é necessário descartar os índices não clusterizados antes de criar o índice columnstore.  
  
```  
  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
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
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  Remova todos os índices não clusterizados da tabela rowstore.  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  Descarte o índice clusterizado.  
  
    -   Faça isso somente se desejar especificar um novo nome para o índice quando ele for convertido em um índice columnstore clusterizado. Se você não remover o índice clusterizado, o novo índice columnstore clusterizado tem o mesmo nome.  
  
        > [!NOTE]  
        >  Pode ser mais fácil lembrar o nome do índice se você usar seu próprio nome. Todos os índices clusterizados do rowstore usam o nome padrão que é ' ClusteredIndex_\<GUID >'.  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  Converta a tabela rowstore em uma tabela columnstore com um índice columnstore clusterizado.  
  
    ```  
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
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. Converter uma tabela columnstore em um heap rowstore  
 Para converter uma tabela columnstore em um heap rowstore, basta remover o índice columnstore clusterizado.  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. Desfragmentar, recriando o índice columnstore clusterizado inteiro  
   Aplica-se a: SQL Server 2014  
  
 Há duas maneiras de recriar o índice columnstore clusterizado completo. Você pode usar CREATE CLUSTERED COLUMNSTORE INDEX, ou [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md) e a opção REBUILD. Ambos os métodos geram os mesmos resultados.  
  
> [!NOTE]  
>  Começando com o SQL Server 2016, use ALTER INDEX REORGANIZE em vez de reconstruir com os métodos descritos neste exemplo.  
  
```  
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
  
##  <a name="nonclustered"></a>Exemplos de índices columnstore não clusterizados  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>A. Criar um índice columnstore como um índice secundário em uma tabela rowstore  
 Este exemplo cria um índice não clusterizado columnstore em uma tabela rowstore. Somente um índice columnstore pode ser criado nesta situação. O índice columnstore exige armazenamento extra, pois ela contém uma cópia dos dados na tabela rowstore. Este exemplo cria uma tabela simples e um índice clusterizado e, em seguida, demonstra a sintaxe de criação de um índice não clusterizado columnstore.  
  
```  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
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
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 Para obter um exemplo mais complexo usando tabelas particionadas, consulte [visão geral de índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. Criar um índice não clusterizado columnstore com um predicado filtrado  
 O exemplo a seguir cria um índice columnstore não clusterizado filtrado na tabela Production. billofmaterials o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados. O predicado de filtro pode incluir colunas que não sejam de chave no índice filtrado. O predicado deste exemplo seleciona apenas as linhas em que EndDate é não NULL.  
  
```  
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
  
###  <a name="ncDML"></a> D. Alterar os dados em um índice não clusterizado columnstore  
   Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].
  
 Quando você cria um índice columnstore não clusterizado em uma tabela, não pode modificar diretamente os dados nessa tabela. Uma consulta com INSERT, UPDATE, DELETE ou MERGE falhará e retornará uma mensagem de erro. Para adicionar ou modificar os dados na tabela, siga um destes procedimentos:  
  
-   Desabilitar ou descartar o índice columnstore. Depois, você pode atualizar os dados na tabela. Se você desabilitar o índice columnstore, poderá recriar o índice columnstore quando concluir a atualização dos dados. Por exemplo,  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Carregar dados em uma tabela de preparação sem um índice columnstore. Criar um índice columnstore na tabela de preparo. Alternar a tabela de preparo para uma partição vazia da tabela principal.  
  
-   Alternar uma partição da tabela com o índice columnstore para uma tabela de preparo vazia. Se houver um índice columnstore na tabela de preparo, desabilite o índice columnstore. Executar quaisquer atualizações. Criar (ou recriar) o índice columnstore. Alternar a tabela de preparo para a partição anterior (não vazia) da tabela principal.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>A. Alterar um índice clusterizado para um índice columnstore clusterizado  
 Usando a instrução CREATE CLUSTERED COLUMNSTORE INDEX com DROP_EXISTING = ON, você pode:  
  
-   Altere um índice clusterizado em um índice columnstore clusterizado.  
  
-   Recompile um índice columnstore clusterizado.  
  
 Este exemplo cria a tabela de xDimProduct como uma tabela rowstore com um índice clusterizado e, em seguida, usa criar índice de COLUMNSTORE CLUSTERIZADO para alterar a tabela de uma tabela rowstore em uma tabela columnstore.  
  
```  
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
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. Recriar um índice columnstore clusterizado  
 Criar o exemplo anterior, este exemplo usa CREATE CLUSTERED COLUMNSTORE INDEX para recriar o índice columnstore clusterizado existente chamado cci_xDimProduct.  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. Alterar o nome de um índice columnstore clusterizado  
 Para alterar o nome de um índice columnstore clusterizado, remova o índice columnstore clusterizado existente e, em seguida, recrie o índice com um novo nome.  
  
 É recomendável somente fazer esta operação com uma pequena tabela ou uma tabela vazia. Demora muito tempo para descartar um índice columnstore clusterizado grandes e a recrie com um nome diferente.  
  
 Usando o índice de columnstore clusterizado cci_xDimProduct do exemplo anterior, este exemplo descarta o índice columnstore clusterizado cci_xDimProduct e, em seguida, recrie o índice columnstore clusterizado com o nome mycci_xDimProduct.  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. Converter uma tabela columnstore em uma tabela rowstore com um índice clusterizado  
 Pode haver uma situação para a qual você deseja remover um índice columnstore clusterizado e criar um índice clusterizado. Armazena a tabela no formato rowstore. Este exemplo converte uma tabela columnstore em uma tabela rowstore com um índice clusterizado com o mesmo nome. Nenhum dos dados é perdido. Todos os dados vai para a tabela rowstore e as colunas listadas torna-se as colunas de chave no índice clusterizado.  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. Converter uma tabela columnstore um heap rowstore  
 Use [DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32) para descartar o índice columnstore clusterizado e converter a tabela em um heap rowstore. Este exemplo converte a tabela de cci_xDimProduct em um heap rowstore. A tabela continua a ser distribuído, mas é armazenado como um heap.  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  


