---
title: "Criar índice (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
caps.latest.revision: "223"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 92e32f9a86265376a67466aa389f29ec9608a061
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2017
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria um índice relacional em uma tabela ou exibição. Também chamado de um índice rowstore porque ele é um índice de árvore b não clusterizado ou não clusterizado. Você pode criar um índice rowstore antes que haja dados na tabela. Use um índice rowstore para melhorar o desempenho de consulta, especialmente quando as consultas, selecionem colunas específicas ou exigem valores sejam classificados em uma determinada ordem.  
  
  
> [!NOTE]  
>  Azure SQL Data Warehouse e o Parallel Data Warehouse atualmente não dão suporte a restrições exclusivas. Exemplos de referência restrições exclusivas só são aplicáveis ao SQL Server e banco de dados do SQL Azure    
  
 **Exemplos simples:**  
  
```  
-- Create a nonclustered index on a table or view  
CREATE INDEX i1 ON t1 (col1);  
```  
  
```  
--Create a clustered index on a table and use a 3-part name for the table  
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);  
```  
  
```  
-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint 
-- on 3 columns and specify the sort order for each column  
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);  
```  
  
 **Principais cenários:**  
  
-   No SQL Server 2016 e banco de dados do SQL Azure, use um índice não clusterizado em um índice columnstore para melhorar o desempenho da consulta de armazenagem de dados. Consulte [índices Columnstore - Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
 **Você precisa criar um tipo diferente de índice?**  
  
-   [Criar índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)  
  
-   [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )   
    [ INCLUDE ( column_name [ ,...n ] ) ]  
    [ WHERE <filter_predicate> ]  
    [ WITH ( <relational_index_option> [ ,...n ] ) ]  
    [ ON { partition_scheme_name ( column_name )   
         | filegroup_name   
         | default   
         }  
    ]  
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<relational_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | STATISTICS_INCREMENTAL = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE | ROW | PAGE}   
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
     [ , ...n ] ) ]  
}  
  
<filter_predicate> ::=   
    <conjunct> [ AND <conjunct> ]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...n)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
Backward Compatible Relational Index  
Important   The backward compatible relational index syntax structure 
will be removed in a future version of SQL Server. Avoid using this 
syntax structure in new development work, and plan to modify 
applications that currently use the feature. Use the syntax structure 
specified in <relational_index_option> instead.  
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
  
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}  
```  

  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON [ database_name . [ schema ] . | schema . ] table_name   
        ( { column [ ASC | DESC ] } [ ,...n ] )  
    WITH ( DROP_EXISTING = { ON | OFF } )  
[;]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 UNIQUE  
 Cria um índice exclusivo em uma tabela ou exibição. Um índice exclusivo é aquele no qual duas linhas não podem ter o mesmo valor de chave de índice. Um índice clusterizado em uma exibição deve ser exclusivo.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não permite a criação de um índice exclusivo em colunas que já contêm valores duplicados, independentemente de IGNORE_DUP_KEY estar definido como ON. Se isso for tentado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibirá uma mensagem de erro. Valores duplicados devem ser removidos para que um índice exclusivo possa ser criado em uma ou mais colunas. As colunas usadas em um índice exclusivo devem ser definidas como NOT NULL, pois vários valores nulos serão considerados duplicatas quando um índice exclusivo for criado.  
  
 CLUSTERED  
 Cria um índice no qual a ordem lógica dos valores de chave determina a ordem física das linhas correspondentes em uma tabela. O nível inferior, ou folha, do índice clusterizado contém as linhas de dados reais da tabela. Uma tabela ou exibição pode ter um índice clusterizado por vez.  
  
 Uma exibição com um índice clusterizado exclusivo é chamada de exibição indexada. Criar um índice clusterizado exclusivo em uma exibição materializa fisicamente a exibição. Um índice clusterizado exclusivo deve ser criado em uma exibição para que qualquer outro índice possa ser definido na mesma exibição. Para obter mais informações, veja [Criar exibições indexadas](../../relational-databases/views/create-indexed-views.md).  
  
 Crie o índice clusterizado antes de criar quaisquer índices não clusterizados. Os índices não clusterizados existentes nas tabelas serão recriados quando um índice clusterizado for criado.  
  
 Se CLUSTERED não for especificado, um índice não clusterizado será criado.  
  
> [!NOTE]  
>  Como o nível de folha de um índice clusterizado e as páginas de dados são os mesmos por definição, criando um índice clusterizado e usando ON *partition_scheme_name* ou ON *filegroup_name* cláusula efetivamente Move uma tabela do grupo de arquivos no qual a tabela foi criada para o novo esquema de partição ou grupo de arquivos. Antes de criar tabelas ou índices em grupos de arquivos específicos, verifique quais grupos de arquivos estão disponíveis e se eles têm espaço vazio suficiente para o índice.  
  
 Em alguns casos, criar um novo índice clusterizado pode habilitar índices previamente desabilitados. Para obter mais informações, consulte [habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md) e [desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
 **NÃO CLUSTERIZADO**  
 Cria um índice que especifica a ordem lógica de uma tabela. Com um índice não clusterizado, a ordem física das linhas de dados é independente de sua ordem indexada.  
  
 Cada tabela pode ter até 999 índices não clusterizados, independentemente de como eles são criados: seja implicitamente com as restrições PRIMARY KEY e UNIQUE ou explicitamente com CREATE INDEX.  
  
 Para exibições indexadas, os índices não clusterizados podem ser criados somente em uma exibição que tenha um índice clusterizado exclusivo já definido.  
  
 O padrão é NONCLUSTERED.  
  
 *index_name*  
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela ou exibição, mas não precisam ser exclusivos no banco de dados. Os nomes de índice devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *column*  
 É a coluna, ou colunas, em que o índice se baseia. Especifique dois ou mais nomes de coluna para criar um índice composto com os valores combinados das colunas especificadas. Lista as colunas a serem incluídas no índice composto, em ordem de prioridade de classificação, dentro dos parênteses após *table_or_view_name*.  
  
 Até 32 colunas podem ser combinadas em uma chave de índice composto único. Todas as colunas de uma chave de índice composto devem estar na mesma tabela ou exibição. O tamanho máximo permitido de valores de índice combinados é de 900 bytes para um índice clusterizado ou 1.700 para um índice não clusterizado. Os limites são 16 colunas e 900 bytes para versões anteriores [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
 Colunas que são dos tipos de dados de objeto grande (LOB) **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**,  **varbinary (max)**, **xml**, ou **imagem** não pode ser especificado como colunas de chave para um índice. Além disso, uma definição de exibição não pode incluir **ntext**, **texto**, ou **imagem** colunas, mesmo se eles não são referenciados na instrução CREATE INDEX.  
  
 É possível criar índices em colunas do tipo CLR definido pelo usuário se o tipo der suporte à ordenação binária. Também é possível criar índices em colunas computadas definidas como invocações de método de uma coluna de tipo definido pelo usuário, desde que os métodos sejam marcados como determinísticos e não executem operações de acesso aos dados. Para obter mais informações sobre como indexar colunas do tipo definido pelo usuário CLR, consulte [tipos definidos pelo usuário CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 [ **ASC** | DESC]  
 Determina a direção de classificação crescente ou decrescente da coluna de índice específica. O padrão é ASC.  
  
 INCLUIR **(***coluna* [ **,**... *n* ] **)**  
 Especifica as colunas não chave a serem adicionadas ao nível folha do índice não clusterizado. O índice não clusterizado pode ser exclusivo ou não exclusivo.  
  
 Os nomes de coluna não podem ser repetidos na lista INCLUDE e não podem ser usados simultaneamente como colunas de chave e não chave. Índices não clusterizados sempre conterão as colunas de índice clusterizado se um índice clusterizado for definido na tabela. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 São permitidos todos os tipos de dados, exceto **text**, **ntext**e **image**. O índice deve ser criado ou recriado offline (ONLINE = OFF) se qualquer uma das colunas não chave especificadas são **varchar (max)**, **nvarchar (max)**, ou **varbinary (max)** dados tipos.  
  
 As colunas computadas que são determinísticas e precisas ou imprecisas podem ser colunas incluídas. Colunas computadas derivadas de **imagem**, **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e **xml** tipos de dados podem ser incluídos em colunas não chave, desde que os tipos de dados de coluna computada seja permitido como uma coluna incluída. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
 Para obter informações sobre como criar um índice XML, consulte [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md).  
  
 ONDE \<filter_predicate > cria um índice filtrado especificando quais linhas a serem incluídas no índice. O índice filtrado deve ser um índice não clusterizado em uma tabela. Cria estatísticas filtradas para as linhas de dados no índice filtrado.  
  
 O predicado de filtro usa a lógica de comparação simples e não pode fazer referência a uma coluna computada, a uma coluna UDT, a uma coluna de tipo de dados espacial ou a uma coluna de tipo de dados hierarchyID. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.  
  
 Estes são alguns exemplos de predicados de filtro da tabela `Production.BillOfMaterials`:  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Índices filtrados não se aplicam a índices XML e índices de texto completo. Para índices UNIQUE, somente as linhas selecionadas devem ter valores de índice exclusivo. Índices filtrados não permitem a opção IGNORE_DUP_KEY.  
  
 ON *partition_scheme_name***(***column_name***)**  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica o esquema de partição que define os grupos de arquivos nos quais as partições de um índice particionado serão mapeadas. O esquema de partição deve existir no banco de dados executando [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) ou [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *nome da coluna* Especifica a coluna na qual um índice particionado será particionado. Esta coluna deve corresponder ao tipo de dados, comprimento e precisão do argumento da partição de função que *partition_scheme_name* está usando. *nome da coluna* não é restrito às colunas na definição do índice. Qualquer coluna na tabela base pode ser especificada, exceto quando particionar um índice exclusivo, *column_name* deve ser escolhida entre aquelas usadas como a chave exclusiva. Essa restrição permite ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificar a exclusividade de valores de chave em uma única partição apenas.  
  
> [!NOTE]  
>  Ao particionar um índice clusterizado não exclusivo, por padrão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento à lista de chaves de índices clusterizados, se ela já não estiver especificada. Ao particionar um índice não clusterizado e não exclusivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona a coluna de particionamento como uma coluna não chave (incluída) do índice, se ela já não estiver especificada.  
  
 Se *partition_scheme_name* ou *arquivos* não for especificado e a tabela estiver particionada, o índice será colocado no mesmo esquema de partição, usando a mesma coluna de particionamento da tabela subjacente.  
  
> [!NOTE]  
>  Não é possível especificar um esquema de particionamento em um índice XML. Se a tabela base for particionada, o índice XML usará o mesmo esquema de partição que a tabela.  
  
 Para obter mais informações sobre o particionamento de índices, [tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 ON *filegroup_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Cria o índice especificado no grupo de arquivos especificado. Se nenhum local for especificado e a tabela ou exibição não for particionada, o índice usará o mesmo grupo de arquivos que a tabela ou exibição subjacente. O grupo de arquivos já deve existir.  
  
 ON **"**padrão**"**  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssCurrent](../../includes/sssdsfull-md.md)].  
  
 Cria o índice especificado no grupo de arquivos padrão.  
  
 Nesse contexto, default não é uma palavra-chave. Ele é um identificador para o grupo de arquivos padrão e deve ser delimitado, como em ON **"**padrão**"** ou ON **[**padrão**]**. Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL"}]  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica a colocação de dados FILESTREAM para a tabela quando um índice clusterizado é criado. A cláusula FILESTREAM_ON permite mover os dados FILESTREAM para outro grupo de arquivos ou esquema de partição FILESTREAM.  
  
 *filestream_filegroup_name* é o nome de um grupo de arquivos FILESTREAM. O grupo de arquivos deve ter um arquivo definido para o grupo de arquivos usando um [criar banco de dados](../../t-sql/statements/create-database-sql-server-transact-sql.md) ou [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrução; caso contrário, ocorrerá um erro.  
  
 Se a tabela for particionada, a cláusula FILESTREAM_ON deverá ser incluída e especificar um esquema de partição de grupo de arquivos FILESTREAM que use a mesma função de partição e colunas de partição que o esquema de partição da tabela. Caso contrário, será gerado um erro.  
  
 Se a tabela não estiver particionada, a coluna FILESTREAM não poderá ser particionada. Os dados FILESTREAM da tabela devem ser armazenados em um único grupo de arquivos que é especificado na cláusula FILESTREAM_ON.  
  
 FILESTREAM_ON NULL poderá ser especificado em uma instrução CREATE INDEX se um índice clusterizado estiver sendo criado e a tabela não contiver uma coluna FILESTREAM.  
  
 Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **\<objeto >:: =**  
  
 É o objeto totalmente qualificado ou não totalmente qualificado a ser indexado.  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or_view_name*  
 É o nome da tabela ou exibição que será indexada.  
  
 A exibição deve ser definida com SCHEMABINDING para criar um índice nela. Um índice clusterizado exclusivo deve ser criado em uma exibição antes que qualquer índice não clusterizado seja criado. Para obter mais informações sobre exibições indexadas, consulte a seção Comentários.  
  
 Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o objeto pode ser uma tabela armazenada com um índice columnstore clusterizado.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]suporta o formato de nome de três partes *database_name***.** [*schema_name*]**.** *object_name* quando o *database_name* é o banco de dados atual ou o *database_name* é tempdb e o *object_name*começa com #.  
  
 **\<relational_index_option >:: =**  
  
 Especifica as opções a serem usadas ao criar o índice.  
  
 PAD_INDEX = {ON | **OFF** }  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 A porcentagem de espaço livre especificada por *fillfactor* é aplicada às páginas de nível intermediário do índice.  
  
 DESATIVAR ou *fillfactor* não for especificado  
 As páginas de nível intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, considerando o conjunto de chaves em páginas intermediárias.  
  
 A opção PAD_INDEX só é útil quando FILLFACTOR é especificado, porque PAD_INDEX usa a porcentagem especificada por FILLFACTOR. Se a porcentagem especificada para FILLFACTOR não for grande o suficiente para permitir uma linha, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] substituirá a porcentagem internamente para permitir o valor mínimo. O número de linhas em uma página de índice intermediária nunca é menor que dois, independentemente de quão baixo o valor de *fillfactor*.  
  
 Na sintaxe compatível com versões anteriores, WITH PAD_INDEX é equivalente a WITH PAD_INDEX = ON.  
  
 Fator de preenchimento  **=**  *fator de preenchimento*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou recriação do índice. *fator de preenchimento* deve ser um valor inteiro de 1 a 100. Se *fillfactor* é 100, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria índices com páginas de folha preenchidas até a capacidade.  
  
 A configuração FILLFACTOR se aplica somente quando o índice é criado ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para exibir a configuração do fator de preenchimento, use o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.  
  
> [!IMPORTANT]  
>  A criação de um índice clusterizado com FILLFACTOR inferior a 100 afeta a quantidade de espaço de armazenamento ocupado pelos dados, porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.  
  
 Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica se deseja armazenar os resultados de classificação temporários no **tempdb**. O padrão é OFF.  
  
 ON  
 Os resultados intermediários de classificação que são usados para criar o índice são armazenados em **tempdb**. Isso pode reduzir o tempo necessário para criar um índice se **tempdb** está em um conjunto de discos diferente do banco de dados do usuário. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 Além do espaço necessário no banco de dados de usuário para criar o índice, **tempdb** deve ter aproximadamente a mesma quantidade de espaço adicional para armazenar os resultados intermediários de classificação. Para obter mais informações, consulte [opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 Na sintaxe compatível com versões anteriores, WITH SORT_IN_TEMPDB é equivalente a WITH SORT_IN_TEMPDB = ON.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. A opção não tem nenhum efeito ao executar [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), ou [atualização](../../t-sql/queries/update-transact-sql.md). O padrão é OFF.  
  
 ON  
 Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.  
  
 OFF  
 Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.  
  
 IGNORE_DUP_KEY não pode ser definido como ON para índices criados em uma exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.  
  
 Para exibir IGNORE_DUP_KEY, use [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Na sintaxe compatível com versões anteriores, WITH IGNORE_DUP_KEY é equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF**}  
 Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ON  
 As estatísticas desatualizadas não são recalculadas automaticamente.  
  
 OFF  
 A atualização automática de estatísticas está habilitada.  
  
 Para restaurar a atualização automática de estatísticas, defina STATISTICS_NORECOMPUTE como OFF ou execute UPDATE STATISTICS sem a cláusula NORECOMPUTE.  
  
> [!IMPORTANT]  
>  Se o recálculo automático de estatísticas de distribuição for desabilitado, o otimizador de consulta possivelmente ficará impedido de selecionar planos de execução ideais para consultas que envolvam a tabela.  
  
 Na sintaxe compatível com versões anteriores, WITH STATISTICS_NORECOMPUTE é equivalente a WITH STATISTICS_NORECOMPUTE = ON.  
  
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
  
 DROP_EXISTING = {ON | **OFF** }  
 É uma opção para descartar e recriar o índice clusterizado ou existente com as especificações da coluna modificada e manter o mesmo nome para o índice. O padrão é OFF.  
  
 ON  
 Especifica para descartar e recriar o índice existente, que deve ter o mesmo nome que o parâmetro *index_name*.  
  
 OFF  
 Especifica não para descartar e recriar o índice existente. SQL Server exibe um erro se o nome do índice especificado já existe.  
  
 Com DROP_EXISTING, você pode alterar:  
  
-   Um índice rowstore não clusterizados para um índice rowstore clusterizado.  
  
 Com DROP_EXISTING, você não pode alterar:  
  
-   Um índice clusterizado rowstore em um índice rowstore não clusterizados.  
  
-   Um índice columnstore clusterizado para qualquer tipo de índice de rowstore.  
  
 Na sintaxe compatível com versões anteriores, WITH DROP_EXISTING é equivalente a WITH DROP_EXISTING = ON.  
  
 ONLINE = {ON | **OFF** }  
 Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Ele permite o prosseguimento de consultas ou atualizações feitas na tabela e nos índices subjacentes. No início da operação, um bloqueio Compartilhado (S) é mantido no objeto de origem por um período muito curto. Ao término da operação, por um curto período de tempo, um bloqueio S (Compartilhado) será adquirido na origem se um índice não clusterizado estiver sendo criado; ou um bloqueio de modificação de esquema (SCH-M) será adquirido quando um índice clusterizado for criado ou descartado online e quando um índice clusterizado ou não clusterizado estiver sendo recriado. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local.  
  
 DESATIVADO  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Uma operação de índice offline que cria, recria ou cancela um índice clusterizado ou recria ou cancela um índice não clusterizado, adquire um bloqueio de esquema de modificação (Sch-M) na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT.  
  
 Para obter mais informações, consulte [como funcionam as operações de índice Online](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Índices, inclusive os índices em tabelas temporárias globais, podem ser criados online com as seguintes exceções:  
  
-   Índice XML  
-   Índice em uma tabela temporária local.  
-   Índice clusterizado exclusivo inicial em uma exibição.  
-   Índices clusterizados desabilitados.  
-   Índice clusterizado se a tabela subjacente contiver tipos de dados LOB: **imagem**, **ntext**, **texto**e tipos espaciais.  
-   **varchar (max)** e **varbinary (max)** colunas não podem ser parte de um índice. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e, em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], quando uma tabela contiver **varchar (max)** ou **varbinary (max)** colunas, um índice clusterizado contendo outras colunas podem ser criado ou recriado usando o **ONLINE** opção. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]não permite que o **ONLINE** opção quando a tabela base contém **varchar (max)** ou **varbinary (max)** colunas.  
  
 Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ALLOW_ROW_LOCKS = { **ON** | OFF}  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
 ALLOW_PAGE_LOCKS = { **ON** | OFF}  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
 MAXDOP = *max_degree_of_parallelism*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Substitui o **grau máximo de paralelismo** opção de configuração para a duração da operação de índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado, ou menos, com base na carga de trabalho atual do sistema.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION  
 Especifica a opção de compactação de dados para o índice, número de partição ou intervalo de partições especificado. As opções são as seguintes:  
  
 Nenhuma  
 O índice ou as partições especificadas não são compactados.  
  
 ROW  
 O índice ou as partições especificadas são compactados com o uso da compactação de linha.  
  
 PAGE  
 O índice ou as partições especificadas são compactados com o uso da compactação de página.  
  
 Para obter mais informações sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
 EM partições **(** { \<partition_number_expression > | \<intervalo >} [ **,**...  *n*  ] **)** **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se o índice não for particionado, o argumento ON PARTITIONS irá gerar um erro. Se a cláusula ON PARTITIONS não for fornecida, a opção DATA_COMPRESSION será aplicada a todas as partições de um índice particionado.  
  
 \<partition_number_expression > pode ser especificado das seguintes maneiras:  
  
-   Forneça o número de uma partição, por exemplo: ON PARTITIONS (2).  
  
-   Forneça os números de várias partições individuais separados por vírgulas, por exemplo: ON PARTITIONS (1, 5).  
  
-   Forneça os intervalos e as partições individuais, por exemplo: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<Range > pode ser especificado como números de partição separados pela palavra TO, por exemplo: ON PARTITIONS (6 TO 8).  
  
 Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção DATA_COMPRESSION mais de uma vez, por exemplo:  
  
```  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
## <a name="remarks"></a>Comentários  
 A instrução CREATE INDEX é otimizada como qualquer outra consulta. Para salvar as operações de E/S, o processador de consultas pode optar por examinar outro índice em vez de executar um exame de tabela. A operação de classificação pode ser eliminada em algumas situações. Em computadores com multiprocessadores, CREATE INDEX pode usar mais processadores para executar operações de exame e classificação associadas à criação do índice, exatamente como fazem outras consultas. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 A operação de criação de índice poderá ser registrada minimamente se o modelo de recuperação de banco de dados for definido como bulk-logged ou simples.  
  
 Os índices podem ser criados em uma tabela temporária. Quando a tabela for removida ou a sessão encerrada, os índices serão removidos.  
  
 Os índices dão suporte a propriedades estendidas.  
  
## <a name="clustered-indexes"></a>Índices clusterizados  
 Criar um índice clusterizado em uma tabela (heap) ou descartar e recriar um índice clusterizado existente requer espaço de trabalho adicional disponível no banco de dados, para acomodar a classificação de dados e uma cópia temporária da tabela original ou dos dados do índice clusterizado existente. Para obter mais informações sobre índices clusterizados, consulte [criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md).  
  
## <a name="nonclustered-indexes"></a>Índices não clusterizados  
 Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você pode criar um índice não clusterizado em uma tabela armazenada como um índice columnstore clusterizado. Se você primeiro crie um índice não clusterizado em uma tabela armazenada como um heap ou índice clusterizado, o índice será mantido se posteriormente você converter a tabela em um índice columnstore clusterizado. Também não é necessário descartar o índice não clusterizado quando você recria o índice columnstore clusterizado.  
  
 Limitações e restrições:  
  
-   A opção FILESTREAM_ON não é válida quando você cria um índice não clusterizado em uma tabela armazenada como um índice columnstore clusterizado.  
  
## <a name="unique-indexes"></a>Índices exclusivos  
 Quando existe um índice exclusivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se há valores duplicados sempre que dados são adicionados por operações de inserção. As operações de inserção que geram valores de chave duplicados são revertidas, e o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe uma mensagem de erro. Isso acontece mesmo que a operação de inserção altere muitas linhas, mas crie apenas uma duplicata. Se for feita uma tentativa de inserir dados para os quais há um índice exclusivo e a cláusula IGNORE_DUP_KEY for definida como ON, somente as linhas que violarem o índice UNIQUE falharão.  
  
## <a name="partitioned-indexes"></a>Índices particionados  
 Índices particionados são criados e mantidos de uma maneira semelhante às tabelas particionadas, mas, como índices comuns, são tratados como objetos de banco de dados separados. É possível haver um índice particionado em uma tabela não particionada, bem como é possível ter um índice não particionado em uma tabela particionada.  
  
 Se você estiver criando um índice em uma tabela particionada e não especificar um grupo de arquivos para colocar o índice, ele será particionado da mesma maneira que a tabela subjacente. Isso ocorre porque, por padrão, os índices são colocados nos mesmos grupos de arquivos que suas tabelas subjacentes e, para uma tabela particionada, no mesmo esquema de partição que usa as mesmas colunas de particionamento. Quando o índice utilizará o mesmo esquema de partição e a coluna de particionamento da tabela, o índice é *alinhado* com a tabela.  
  
> [!WARNING]  
>  É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações. É recomendável usar índices alinhados apenas quando o número de partições for maior que 1.000.  
  
 Ao particionar um índice clusterizado não exclusivo, por padrão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adiciona quaisquer colunas de particionamento à lista de chaves de índice clusterizado, se já não estiverem especificadas.  
  
 As exibições indexadas podem ser criadas em tabelas particionadas da mesma maneira que os índices em tabelas. Para obter mais informações sobre índices particionados, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as estatísticas não são criadas por meio do exame todas as linhas na tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Para obter estatísticas em índices particionados por meio do exame de todas as linhas da tabela, use CREATE STATISTICS ou UPDATE STATISTICS com a cláusula FULLSCAN.  
  
## <a name="filtered-indexes"></a>Índices filtrados  
 Índice filtrado é um índice não clusterizado otimizado, adequado a consultas que selecionam uma pequena porcentagem de linhas de uma tabela. Ele usa um predicado de filtro para indexar uma parte dos dados na tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta, além de reduzir custos de armazenamento e de manutenção.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Opções SET necessárias para índices filtrados  
 As opções SET na coluna Valor necessário são necessárias sempre que ocorrer alguma das seguintes condições:  
  
-   Criar um índice filtrado.  
  
-   A operação INSERT, UPDATE, DELETE ou MERGE modificar os dados de um índice filtrado.  
  
-   O índice filtrado é usado pelo otimizador de consulta para produzir o plano de consulta.  
  
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
  
## <a name="spatial-indexes"></a>Índices espaciais  
 Para obter informações sobre índices espaciais, consulte [CREATE SPATIAL INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-spatial-index-transact-sql.md) e [visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="xml-indexes"></a>Índices XML  
 Para informações sobre índices XML, consulte [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md) e [XML índices &#40; SQL Server &#41; ](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="index-key-size"></a>Tamanho de chave de índice  
 O tamanho máximo para uma chave de índice é de 900 bytes para um índice clusterizado e 1.700 bytes para um índice não clusterizado. (Antes de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] o limite foi sempre 900 bytes.) Índices em **varchar** colunas que excedem o limite de bytes que podem ser criadas se os dados existentes nas colunas não exceder o limite no momento em que o índice é criado; Entretanto, subsequentes de inserção ou atualização ações nas colunas que fazem com que o tamanho total seja maior que o limite falhará. A chave de um índice clusterizado não pode conter colunas **varchar** que tenham dados existentes na unidade de alocação ROW_OVERFLOW_DATA. Se um índice clusterizado for criado em uma coluna **varchar** e os dados existentes estiverem na unidade de alocação IN_ROW_DATA, as ações subsequentes de inserção ou atualização na coluna que faria o push dos dados da linha apresentarão falha.  
  
 Índices não clusterizados podem incluir colunas não chave no nível folha do índice. Essas colunas não são consideradas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao calcular o tamanho da chave de índice. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
> [!NOTE]  
>  Quando as tabelas são particionadas, se as colunas de chave de particionamento ainda não estiverem presentes em um índice clusterizado não exclusivo, elas poderão ser adicionadas ao índice pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O tamanho combinado das colunas indexadas (sem contar as colunas incluídas) mais qualquer coluna de particionamento adicionada não pode exceder 1.800 bytes em um índice clusterizado não exclusivo.  
  
## <a name="computed-columns"></a>Colunas computadas  
 Os índices podem ser criados em colunas computadas. Além disso, as colunas computadas podem ter a propriedade PERSISTED. Isso significa que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena os valores computados na tabela e os atualiza quando as outras colunas das quais a coluna computada depende são atualizadas. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa esses valores persistentes ao criar um índice na coluna e quando o índice é referenciado em uma consulta.  
  
 Uma coluna computada deve ser determinística e precisa para ser indexada. Entretanto, o uso da propriedade PERSISTED expande o tipo das colunas computadas indexáveis para incluir:  
  
-   Colunas computadas baseadas nas funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e CLR, e métodos de tipo CLR definidos pelo usuário que são marcados como determinísticos pelo usuário.  
  
-   Colunas computadas baseadas em expressões que são determinísticas, conforme definidas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], mas imprecisas.  
  
 As colunas computadas persistentes requerem que as seguintes opções SET sejam definidas como mostrado na seção anterior "Opções SET necessárias para exibições indexadas".  
  
 A restrição UNIQUE ou PRIMARY KEY pode conter uma coluna computada contanto que satisfaça todas as condições para indexação. Especificamente, a coluna computada deve ser determinística e precisa ou determinística e persistente. Para obter mais informações sobre determinismo, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
 Colunas computadas derivadas de **imagem**, **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e **xml** dados tipos podem ser indexadas como uma coluna de chave não chave ou incluída como o tipo de dados de coluna computada seja permitido como uma coluna de chave de índice ou coluna não chave. Por exemplo, você não pode criar um índice XML primário em um computada **xml** coluna. Se o tamanho da chave de índice exceder 900 bytes, uma mensagem de aviso será exibida.  
  
 Criar um índice em uma coluna computada pode causar a falha de uma operação de inserção ou atualização que tenha funcionado anteriormente. Essa falha pode ocorrer quando a coluna computada resultar em erro aritmético. Por exemplo, na tabela a seguir, embora a coluna computada `c` resulte em um erro aritmético, a instrução `INSERT` funciona.  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 Se, em vez disso, depois de criar a tabela, você criar um índice em uma coluna computada `c`, a mesma instrução `INSERT` agora falhará.  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
## <a name="included-columns-in-indexes"></a>Colunas incluídas em índices  
 As colunas não chave, chamadas de colunas incluídas, podem ser adicionadas ao nível folha de um índice não clusterizado para melhorar o desempenho da consulta ao abrangê-la. Isso quer dizer que todas as colunas referenciadas na consulta são incluídas no índice como colunas de chave ou não chave. Isso permite que o otimizador de consulta localize todas as informações necessárias de um exame de índice; os dados de tabela ou de índice clusterizado não são acessados. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
## <a name="specifying-index-options"></a>Especificando opções de índice  
 O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu novas opções de índice e também modifica o modo como as opções são especificadas. Na sintaxe compatível com versões anteriores, WITH *option_name* é equivalente a WITH **(** \<option_name >  **=**  ON **)**. Ao definir as opções de índice, aplicam-se as seguintes regras: 
  
-   Novas opções de índice só podem ser especificadas usando WITH **(***option_name*  **=**  ON | DESATIVAR**)**.  
  
-   As opções não podem ser especificadas com o uso de sintaxe compatível com versões anteriores e nova sintaxe na mesma instrução. Por exemplo, especificando WITH **(**DROP_EXISTING**,** ONLINE  **=**  ON**)** faz com que a instrução falhar.  
  
-   Quando você cria um índice XML, as opções devem ser especificadas usando WITH **(***option_name*  **=**  ON | DESATIVAR**)**.  
  
## <a name="dropexisting-clause"></a>Cláusula DROP_EXISTING  
 É possível usar a cláusula DROP_EXISTING para recriar o índice, adicionar ou descartar colunas, modificar opções, modificar a ordem de classificação de colunas, ou alterar o esquema de partição ou o grupo de arquivos.  
  
 Se o índice impuser uma restrição PRIMARY KEY ou UNIQUE e a definição de índice não for alterada de alguma maneira, o índice será descartado e recriado preservando a restrição existente. Entretanto, se a definição de índice for alterada, a instrução falhará. Para alterar a definição de uma restrição PRIMARY KEY ou UNIQUE, descarte a restrição e adicione uma restrição com a nova definição.  
  
 DROP_EXISTING melhora o desempenho quando você recria um índice clusterizado, com o mesmo conjunto de chaves ou um conjunto diferente, em uma tabela que também tenha índices não clusterizados. DROP_EXISTING substitui a execução de uma instrução DROP_INDEX no índice clusterizado antigo, seguida da execução de uma instrução CREATE_INDEX para o novo índice clusterizado. Os índices não clusterizados são recriados uma vez e, depois disso, somente se a definição de índice for alterada. A cláusula DROP_EXISTING não recria os índices não clusterizados quando a definição de índice tem o mesmo nome de índice, chave e colunas de partição, atributo de exclusividade e ordem de classificação que o índice original.  
  
 Os índices não clusterizados podem ser recriados ou não, mas sempre permanecem em seus grupos de arquivos ou esquemas de partição originais e usam as funções de partição originais. Se um índice clusterizado for recriado para um grupo de arquivos ou esquema de partição diferente, os índices não clusterizados não serão movidos para coincidir com o novo local do índice clusterizado. Portanto, mesmo os índices não clusterizados previamente alinhados ao índice clusterizado, podem não estar mais alinhados a ele. Para obter mais informações sobre o alinhamento de índices particionados, consulte.  
  
 A cláusula DROP_EXISTING não classificará os dados novamente se as mesmas colunas de chave de índice forem usadas na mesma ordem e com a mesma ordem crescente ou decrescente, a menos que a instrução de índice especifique um índice não clusterizado e a opção ONLINE seja definida como OFF. Se o índice clusterizado for desabilitado, a operação CREATE INDEX WITH DROP_EXISTING deverá ser executada com ONLINE definido como OFF. Se um índice não clusterizado for desabilitado e não for associado a um índice clusterizado desabilitado, a operação CREATE INDEX WITH DROP_EXISTING poderá ser executada com ONLINE definido como OFF ou ON.  
  
 Quando índices com 128 extensões ou mais são descartados ou recriados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.  
  
## <a name="online-option"></a>Opção ONLINE  
 As diretrizes a seguir são aplicáveis ao executar operações de índice online:  
  
-   A tabela subjacente não pode ser alterada, truncada ou descartada quando uma operação de índice online estiver em andamento.  
  
-   É necessário espaço em disco temporário adicional durante a operação de índice.  
  
-   As operações online podem ser executadas em índices particionados e índices que contenham colunas computadas ou colunas incluídas persistentes.  
  
 Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
## <a name="row-and-page-locks-options"></a>Opções de bloqueios de linha e de página  
 Quando ALLOW_ROW_LOCKS = ON e ALLOW_PAGE_LOCK = ON, os bloqueios em nível de linha, página e tabela são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.  
  
 Quando ALLOW_ROW_LOCKS = OFF e ALLOW_PAGE_LOCK = OFF, somente um bloqueio em nível de tabela é permitido ao acessar o índice.  
  
## <a name="viewing-index-information"></a>Exibindo informações de índice  
 Para retornar informações sobre índices, é possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema.  
  
## <a name="data-compression"></a>Data Compression  
 Compactação de dados é descrita no tópico [compactação de dados](../../relational-databases/data-compression/data-compression.md). A seguir estão os pontos-chave a serem considerados:  
  
-   A compactação pode permitir que mais linhas sejam armazenadas em uma página, mas não altera o tamanho máximo da linha.  
  
-   Páginas não folha de um índice não são compactadas por página, mas podem ser compactadas por linha.  
  
-   Cada índice não clusterizado tem uma configuração de compactação individual e não herda a configuração de compactação da tabela subjacente.  
  
-   Quando um índice clusterizado é criado em um heap, ele herda o estado de compactação do heap, a menos que um estado de compactação alternativo seja especificado.  
  
 As restrições a seguir se aplicam a índices particionados:  
  
-   Não será possível alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.  
  
-   A instrução ALTER INDEX \<índice >... REBUILD PARTITION ... recria a partição especificada do índice.  
  
-   A instrução ALTER INDEX \<índice >... REBUILD WITH... recria todas as partições do índice.  
  
 Para avaliar como a alteração do estado de compactação afetará uma tabela, um índice ou uma partição, use o procedimento armazenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], você não pode criar:  
  
-   Um índice rowstore clusterizado ou em uma tabela de data warehouse quando já existe um índice. Esse comportamento é diferente do SMP SQL Server que permite que os índices rowstore e columnstore coexistir na mesma tabela.  
  
-   Você não pode criar um índice em uma exibição.  
  
## <a name="metadata"></a>Metadados  
 Para exibir informações sobre índices existentes, você pode consultar o [sys. Indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.  
  
## <a name="version-notes"></a>Notas de versão  
 Banco de dados SQL não oferece suporte a opções de grupo de arquivos e filestream.  
  
## <a name="examples-all-versions-uses-the-adventureworks-database"></a>Exemplos: Todas as versões. Usa o banco de dados AdventureWorks.  
  
### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. Criar um índice rowstore não clusterizado simples  
 Os exemplos a seguir criam um índice não clusterizado no `VendorID` coluna o `Purchasing.ProductVendor` tabela.  
  
```  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. Criar um índice composto rowstore não clusterizado simples  
 O exemplo a seguir cria um índice composto não clusterizado no `SalesQuota` e `SalesYTD` colunas do `Sales.SalesPerson` tabela.  
  
```  
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  
```  
  
### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. Criar um índice em uma tabela em outro banco de dados  
 O exemplo a seguir cria um índice não clusterizado no `VendorID` coluna o `ProductVendor` tabela o `Purchasing` banco de dados.  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);   
```  
  
### <a name="d-add-a-column-to-an-index"></a>D. Adicionar uma coluna a um índice  
 O exemplo a seguir cria o índice IX_FF com duas colunas de dbo. Tabela FactFinance.  A próxima instrução recompila o índice com uma coluna e mantém o nome existente.  
  
```  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey ASC, DateKey ASC );  
  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)  
WITH ( DROP_EXISTING = ON );  
 ```  
  
## <a name="examples-sql-server-azure-sql-database"></a>Exemplos: SQL Server, o banco de dados SQL do Azure  
  
### <a name="e-create-a-unique-nonclustered-index"></a>E. Criar um índice não clusterizado exclusivo  
 O exemplo a seguir cria um índice não clusterizado exclusivo na coluna `Name` da tabela `Production.UnitMeasure` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O índice imporá a exclusividade dos dados inseridos na coluna `Name`.  
  
```  
CREATE UNIQUE INDEX AK_UnitMeasure_Name   
    ON Production.UnitMeasure(Name);  
```  
  
 A consulta a seguir testa a restrição de exclusividade tentando inserir uma linha com o mesmo valor que o de uma linha existente.  
  
```  
--Verify the existing value.  
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';  
GO  
INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)  
    VALUES ('OC', 'Ounces', GetDate());  
```  
  
 A mensagem de erro resultante é:  
  
```  
Server: Msg 2601, Level 14, State 1, Line 1  
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.  
```  
  
### <a name="f-use-the-ignoredupkey-option"></a>F. Use a opção IGNORE_DUP_KEY  
 O exemplo a seguir demonstra o efeito da opção `IGNORE_DUP_KEY` inserindo várias linhas em uma tabela temporária primeiro com a opção definida como `ON` e, em seguida, com a opção definida como `OFF`. Uma única linha é inserida na tabela `#Test`, causando intencionalmente um valor duplicado quando a segunda instrução de várias linhas `INSERT` for executada. Uma contagem de linhas na tabela retorna o número de linhas inseridas.  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = ON);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 A seguir são apresentados os resultados da segunda instrução `INSERT`.  
  
```  
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.  
  
Number of rows   
--------------   
38  
```  
  
 Observe que as linhas inseridas da tabela `Production.UnitMeasure` que não violaram a restrição de exclusividade foram inseridas com êxito. Um aviso foi emitido e a linha duplicada ignorada, mas a transação inteira não foi revertida.  
  
 As mesmas instruções são executadas novamente, mas com `IGNORE_DUP_KEY` definido como `OFF`.  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = OFF);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 A seguir são apresentados os resultados da segunda instrução `INSERT`.  
  
```  
Server: Msg 2601, Level 14, State 1, Line 5  
Cannot insert duplicate key row in object '#Test' with unique index  
'AK_Index'. The statement has been terminated.  
  
Number of rows   
--------------   
1  
```  
  
 Observe que nenhuma linha da tabela `Production.UnitMeasure` foi inserida na tabela, embora somente uma linha violasse a restrição de índice `UNIQUE`.  
  
### <a name="g-using-dropexisting-to-drop-and-re-create-an-index"></a>G. Usando DROP_EXISTING para descartar e recriar um índice  
 O exemplo a seguir remove e recria um índice existente na coluna `ProductID` da tabela `Production.WorkOrder` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] usando a opção `DROP_EXISTING`. As opções `FILLFACTOR` e `PAD_INDEX` também são definidas.  
  
```  
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID  
    ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80,  
        PAD_INDEX = ON,  
        DROP_EXISTING = ON);  
GO  
  
```  
  
### <a name="h-create-an-index-on-a-view"></a>H. Criar um índice em um modo de exibição  
 O exemplo a seguir cria uma exibição e um índice nessa exibição. Duas consultas que usam a exibição indexada são incluídas.  
  
```  
--Set the options to support indexed views.  
SET NUMERIC_ROUNDABORT OFF;  
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
    QUOTED_IDENTIFIER, ANSI_NULLS ON;  
GO  
--Create view with schemabinding.  
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
DROP VIEW Sales.vOrders ;  
GO  
CREATE VIEW Sales.vOrders  
WITH SCHEMABINDING  
AS  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
        OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
    FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
    WHERE od.SalesOrderID = o.SalesOrderID  
    GROUP BY OrderDate, ProductID;  
GO  
--Create an index on the view.  
CREATE UNIQUE CLUSTERED INDEX IDX_V1   
    ON Sales.vOrders (OrderDate, ProductID);  
GO  
--This query can use the indexed view even though the view is   
--not specified in the FROM clause.  
SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
    OrderDate, ProductID  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND ProductID BETWEEN 700 and 800  
        AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
GROUP BY OrderDate, ProductID  
ORDER BY Rev DESC;  
GO  
--This query can use the above indexed view.  
SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND DATEPART(mm,OrderDate)= 3  
        AND DATEPART(yy,OrderDate) = 2002  
GROUP BY OrderDate  
ORDER BY OrderDate ASC;  
GO  
  
```  
  
### <a name="i-create-an-index-with-included-non-key-columns"></a>I. Criar um índice com colunas incluídas (não chave)  
 O exemplo a seguir cria um índice não clusterizado com uma coluna de chave (`PostalCode`) e quatro colunas não chave (`AddressLine1`, `AddressLine2`, `City`, `StateProvinceID`). Uma consulta incluída pelo índice vem em seguida. Para exibir o índice selecionado pelo otimizador de consulta, no **consulta** menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione **Exibir plano de execução real** antes de executar a consulta.  
  
```  
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
GO  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
GO  
```  
  
### <a name="j-create-a-partitioned-index"></a>J. Criar um índice particionado  
 O exemplo a seguir cria um índice particionado não clusterizado em `TransactionsPS1`, um esquema de partição existente no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Este exemplo pressupõe que o exemplo de índice particionado tenha sido instalado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
GO  
```  
  
### <a name="k-creating-a-filtered-index"></a>K. Criando um índice filtrado  
 O exemplo a seguir cria um índice filtrado na tabela Production.BillOfMaterials do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O predicado de filtro pode incluir colunas que não sejam de chave no índice filtrado. O predicado deste exemplo seleciona apenas as linhas em que EndDate é não NULL.  
  
```  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
### <a name="l-create-a-compressed-index"></a>L. Criar um índice compactado  
 O exemplo a seguir cria um índice em uma tabela não particionada usando a compactação de linha.  
  
```  
CREATE NONCLUSTERED INDEX IX_INDEX_1   
    ON T1 (C2)  
WITH ( DATA_COMPRESSION = ROW ) ;   
GO  
```  
  
 O exemplo a seguir cria um índice em uma tabela particionada usando a compactação de linha em todas as partições do índice.  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH ( DATA_COMPRESSION = ROW ) ;  
GO  
```  
  
 O exemplo a seguir cria um índice em uma tabela particionada usando a compactação de página na partição `1` do índice e a compactação de linha nas partições `2` a `4` do índice.  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),  
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="m-basic-syntax"></a>M. Sintaxe básica  
  
```  
CREATE INDEX IX_VendorID   
    ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID   
    ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID   
    ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="n-create-a-non-clustered-index-on-a-table-in-the-current-database"></a>N. Criar um índice não clusterizado em uma tabela no banco de dados atual  
 O exemplo a seguir cria um índice não clusterizado no `VendorID` coluna o `ProductVendor` tabela.  
  
```  
CREATE INDEX IX_ProductVendor_VendorID   
    ON ProductVendor (VendorID);   
```  
  
### <a name="o-create-a-clustered-index-on-a-table-in-another-database"></a>O. Criar um índice clusterizado em uma tabela em outro banco de dados  
 O exemplo a seguir cria um índice não clusterizado no `VendorID` coluna o `ProductVendor` tabela o `Purchasing` banco de dados.  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID   
    ON Purchasing..ProductVendor (VendorID);   
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [Criar índice ESPACIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Criar índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys. xml_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 

