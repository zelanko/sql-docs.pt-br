---
title: CREATE TABLE (SQL Data Warehouse do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 965a4196c9da552fda93c320bd7f9abea9bd9570
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716691"
---
# <a name="create-table-azure-sql-data-warehouse"></a>CREATE TABLE (SQL Data Warehouse do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Cria uma nova tabela no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  

Para entender as tabelas e como usá-las, confira [Tabelas no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/).

> [!NOTE]
>  as discussões sobre o SQL Data Warehouse neste artigo aplicam-se ao SQL Data Warehouse e ao Parallel Data Warehouse, a menos que haja alguma indicação contrária.

 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>

## <a name="syntax"></a>Sintaxe
  
```
-- Create a new table.
CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]
    )  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[;]  

<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::=
    {
        <cci_option> --default for Azure SQL Data Warehouse
      | HEAP --default for Parallel Data Warehouse
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC
    }  
    {
        DISTRIBUTION = HASH ( distribution_column_name )
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )

<cci_option> ::= [CLUSTERED COLUMNSTORE INDEX] [ORDER (column [,…n])]
  
<data type> ::=
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>
## <a name="arguments"></a>Argumentos

 *database_name*  
 O nome do banco de dados que conterá a nova tabela. O padrão é o banco de dados atual.  
  
 *schema_name*  
 O esquema da tabela. A especificação de *esquema* é opcional. Se ele estiver vazio, o esquema padrão será usado.  
  
 *table_name*  
 O nome da nova tabela. Para criar uma tabela temporária local, preceda o nome da tabela com #.  Para obter explicações e diretrizes sobre tabelas temporárias, confira [Tabelas temporárias no SQL Data Warehouse do Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/). 

 *column_name*  
 O nome de uma coluna da tabela.

### <a name="ColumnOptions"></a> Opções de coluna

 `COLLATE` *Windows_collation_name*  
 Especifica a ordenação da expressão. A ordenação precisa ser uma das ordenações do Windows compatíveis com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de ordenações do Windows compatíveis com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Nome de ordenação do Windows (Transact-SQL)](windows-collation-name-transact-sql.md)/).  
  
 `NULL` | `NOT NULL`  
 Especifica se os valores `NULL` são permitidos na coluna. O padrão é `NULL`.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 Especifica o valor padrão da coluna.  
  
 | Argumento | Explicação |
 | -------- | ----------- |
 | *constraint_name* | O nome opcional da restrição. O nome da restrição é exclusivo no banco de dados. O nome pode ser reutilizado em outros bancos de dados. |
 | *constant_expression* | O valor padrão da coluna. A expressão precisa ser um valor literal ou uma constante. Por exemplo, estas expressões de constante são permitidas: `'CA'`, `4`. Essas expressões constantes não são permitidas: `2+3`, `CURRENT_TIMESTAMP`. |
  
### <a name="TableOptions"></a> Opções de estrutura da tabela

Para obter diretrizes de como escolher o tipo de tabela, confira [Indexando tabelas no SQL Data Warehouse do Azure](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/).
  
 `CLUSTERED COLUMNSTORE INDEX` 
 
Armazena a tabela como um índice columnstore clusterizado. O índice columnstore clusterizado aplica-se a todos os dados da tabela. Esse comportamento é o padrão para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].
 
 `HEAP` Armazena a tabela como um heap. Esse comportamento é o padrão para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 `CLUSTERED INDEX` ( *index_column_name* [ ,...*n* ] )  
 Armazena a tabela como um índice clusterizado com uma ou mais colunas de chave. Esse comportamento armazena os dados por linha. Use *index_column_name* para especificar o nome de uma ou mais colunas de chave no índice.  Para obter mais informações, confira Tabelas rowstore nos Comentários gerais.
 
 `LOCATION = USER_DB` Essa opção foi preterida. Ela é aceita sintaticamente, mas não é mais necessária e não afeta mais o comportamento.   
  
### <a name="TableDistributionOptions"></a> Opções de distribuição da tabela

Para entender como escolher o melhor método de distribuição e use tabelas distribuídas, confira [Distribuindo tabelas no SQL Data Warehouse do Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/).

`DISTRIBUTION = HASH` ( *distribution_column_name* ) Atribui cada linha a uma distribuição, efetuando hash no valor armazenado em *distribution_column_name*. O algoritmo é determinístico, ou seja, ele sempre efetua hash no mesmo valor para a mesma distribuição.  A coluna de distribuição deve ser definida como NOT NULL porque todas as linhas que tiverem NULL são atribuídas à mesma distribuição.

`DISTRIBUTION = ROUND_ROBIN` Distribui as linhas uniformemente entre todas as distribuições de modo round robin. Esse comportamento é o padrão para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].

`DISTRIBUTION = REPLICATE` Armazena uma cópia da tabela em cada nó de computação. Para o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], a tabela é armazenada em um banco de dados de distribuição em cada nó de computação. Para o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], a tabela é armazenada em um grupo de arquivos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que abrange o nó de computação. Esse comportamento é o padrão para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
### <a name="TablePartitionOptions"></a> Opções de partição da tabela
Para obter diretrizes sobre o uso de partições de tabela, confira [Particionando tabelas no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/).

 `PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
Cria uma ou mais partições da tabela. Essas partições são fatias horizontais da tabela que permitem aplicar operações em subconjuntos de linhas, independentemente se a tabela está armazenada como um heap, um índice clusterizado ou um índice columnstore clusterizado. Ao contrário da coluna de distribuição, as partições da tabela não determinam a distribuição em que cada linha é armazenada. As partições da tabela determinam como as linhas são agrupadas e armazenadas em cada distribuição.  

| Argumento | Explicação |
| -------- | ----------- |
|*partition_column_name*| Especifica a coluna que o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usará para particionar as linhas. Esta coluna pode ser de qualquer tipo de dados. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] classifica os valores de coluna de partição em ordem crescente. A ordenação do menor ao maior vai da `LEFT` para a `RIGHT` na especificação `RANGE`. |  
| `RANGE LEFT` | Especifica que o valor de limite pertence à partição à esquerda (valores mais baixos). O padrão é LEFT. |
| `RANGE RIGHT` | Especifica que o valor de limite pertence à partição à direita (valores mais baixos). | 
| `FOR VALUES` ( *boundary_value* [,...*n*] ) | Especifica os valores de limite para a partição. *boundary_value* é uma expressão de constante. Ele não pode ser NULL. Ele deve corresponder ou ser implicitamente conversível no tipo de dados de *partition_column_name*. Ele não pode ser truncado durante a conversão implícita de modo que o tamanho e a escala do valor não correspondam ao tipo de dados de *partition_column_name*<br></br><br></br>Se você especificar a cláusula `PARTITION`, mas não especificar um valor de limite, o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] criará uma tabela particionada com uma partição. Caso seja necessário, você pode dividir a tabela em duas partições posteriormente.<br></br><br></br>Se você especificar um valor de limite, a tabela resultante terá duas partições: uma para os valores menores do que o valor de limite e outra para os valores maiores que o valor de limite. Se você mover uma partição para uma tabela não particionada, a tabela não particionada receberá os dados, mas não terá os limites de partição em seus metadados.| 

 Confira [Criar uma tabela particionada](#PartitionedTable) na seção de exemplos.

### <a name="ordered-clustered-columnstore-index-option-preview-for-azure-sql-data-warehouse"></a>Opção de índice columnstore clusterizado ordenado (versão prévia do SQL Data Warehouse do Azure)

O índice columnstore clusterizado é o padrão para a criação de tabelas no SQL Data Warehouse do Azure.  A especificação ORDER é padronizada para as teclas COMPOUND.  A classificação será sempre em ordem crescente. Se nenhuma cláusula ORDER for especificada, a columnstore não será classificada. Devido ao processo de ordenação, uma tabela com índice columnstore clusterizado e ordenado pode ter tempos de carregamento de dados maiores que os índices columnstore clusterizados e não ordenados. Se você precisar de mais espaço de tempdb ao carregar dados, poderá diminuir a quantidade de dados por inserção.

Durante a visualização, você pode executar essa consulta para verificar as colunas com ORDER habilitado.

```sql
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
```

### <a name="DataTypes"></a> Tipo de dados

O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] é compatível com os tipos de dados mais usados. Abaixo há uma lista dos tipos de dados compatíveis, juntamente com seus detalhes e bytes de armazenamento. Para entender melhor os tipos de dados e como usá-los, confira [Tipos de dados para tabelas no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types).

Para ver uma tabela de conversões de tipo de dados, confira a seção Conversões implícitas de [CAST e CONVERT (Transact-SQL)](https://msdn.microsoft.com/library/ms187928/).

>[!NOTE]
>Veja mais informações em [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql).

`datetimeoffset` [ ( *n* ) ]  
 O valor padrão de *n* é 7.  
  
 `datetime2` [ ( *n* ) ]  
Igual a `datetime`, exceto que você pode especificar o número de segundos fracionários. O valor padrão de *n* é `7`.  
  
|Valor de *n*|Precisão|Escala|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 Armazena a data e a hora do dia com 19 a 23 caracteres de acordo com o calendário gregoriano. A data pode conter ano, mês e dia. A hora contém horas, minutos e segundos. Como opção, você pode exibir três dígitos para segundos fracionários. O tamanho de armazenamento é de 8 bytes.  
  
 `smalldatetime`  
 Armazena uma data e uma hora. O tamanho de armazenamento é de 4 bytes.  
  
 `date`  
 Armazena uma data usando no máximo 10 caracteres para o ano, mês e dia, de acordo com o calendário gregoriano. O tamanho do armazenamento é 3 bytes. A data é armazenada como um inteiro.  
  
 `time` [ ( *n* ) ]  
 O valor padrão de *n* é `7`.  
  
 `float` [ ( *n* ) ]  
 Tipo de dados do número aproximado para ser usado com os dados numéricos de ponto flutuante. Os dados de ponto flutuante são aproximados, o que significa que nem todos os valores no intervalo de tipo de dados podem ser representados exatamente. *n* especifica o número de bits usados para armazenar a mantissa do `float` em notação científica. *n* determina o tamanho do armazenamento e a precisão. Se *n* for especificado, ele precisará ser um valor entre `1` e `53`. O valor padrão de *n* é `53`.  
  
| Valor de *n* | Precisão | Tamanho de armazenamento |  
| --------: | --------: | -----------: |  
| 1-24   | 7 dígitos  | 4 bytes      |  
| 25-53  | 15 dígitos | 8 bytes      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] trata *n* como um dos dois valores possíveis. Se `1`<= *n* <= `24`, *n* é tratado como `24`. Se `25` <= *n* <= `53`, *n* é tratado como `53`.  
  
 O tipo de dados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float` está em conformidade com o padrão ISO para todos os valores de *n* de `1` a `53`. O sinônimo de precisão dupla é `float(53)`.  
  
 `real` [ ( *n* ) ]  
 A definição de real é igual à de float. O sinônimo de ISO para `real` é `float(24)`.  
  
 `decimal` [ ( *precision* [ *, scale* ] ) ] | `numeric` [ ( *precision* [ *, scale* ] ) ]  
 Armazena a precisão fixa e os números de escala.  
  
 *precisão*  
 O número máximo total de dígitos decimais que podem ser armazenados, à esquerda e à direita do ponto decimal. A precisão precisa ser um valor de `1` até a precisão máxima de `38`. A precisão padrão é `18`.  
  
 *scale*  
 O número máximo de dígitos decimais que podem ser armazenados à direita do ponto decimal. *Scale* precisa ser um valor de `0` até *precision*. Você só poderá especificar *scale* se *precision* for especificado. A escala padrão é `0`, assim, `0` <= *scale* <= *precision*. Os tamanhos máximos de armazenamento variam, com base na precisão.  
  
| Precisão | Bytes de armazenamento  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10–19      |             9 |  
| 20–28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 Tipos de dados que representam valores de moeda.  
  
| Tipo de Dados | Bytes de armazenamento |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 Tipos de dados numéricos exatos que usam dados inteiros. O armazenamento é mostrado na tabela a seguir.  
  
| Tipo de Dados | Bytes de armazenamento |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 Um tipo de dados Integer que pode ter o valor `1`, `0` ou NULL. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] otimiza o armazenamento de colunas de bit. Se houver 8 ou menos colunas de bit em uma tabela, as colunas serão armazenadas como 1 byte. Se houver colunas de 9 a 16 bits, as colunas serão armazenadas como 2 bytes e assim por diante.  
  
 `nvarchar` [ ( *n* | `max` ) ] – `max` aplica-se somente ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Dados de caracteres Unicode de comprimento variável. *n* pode ser um valor de 1 a 4000. `max` indica que o tamanho de armazenamento máximo é 2^31-1 bytes (2 GB). O tamanho do armazenamento, em bytes, é duas vezes o número de caracteres inseridos + 2 bytes. Os dados digitados podem ter zero caracteres de comprimento.  
  
 `nchar` [ ( *n* ) ]  
 Dados de caractere Unicode de comprimento fixo com um tamanho de *n* caracteres. *n* precisa ser um valor de `1` a `4000`. O tamanho do armazenamento é duas vezes *n* bytes.  
  
 `varchar` [ ( *n*  | `max` ) ] – `max` aplica-se somente ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 Dados de caractere não Unicode de comprimento variável com um tamanho de *n* bytes. *n* precisa ser um valor de `1` a `8000`. `max` indica que o tamanho máximo do armazenamento é de 2^31-1 bytes (2 GB). O tamanho do armazenamento é o comprimento real dos dados inseridos + 2 bytes.  
  
 `char` [ ( *n* ) ]  
 Dados de caractere não Unicode de comprimento fixo com um tamanho de *n* bytes. *n* precisa ser um valor de `1` a `8000`. O tamanho do armazenamento é *n* bytes. O padrão para *n* é `1`.  
  
 `varbinary` [ ( *n*  | `max` ) ] – `max` aplica-se somente ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Dados binários de comprimento variável. *n* pode ser um valor de `1` a `8000`. `max` indica que o tamanho de armazenamento máximo é 2^31-1 bytes (2 GB). O tamanho de armazenamento é o comprimento real dos dados inseridos + 2 bytes. O valor padrão de *n* é 7.  
  
 `binary` [ ( *n* ) ]  
 Dados binários de comprimento fixo com um tamanho de *n* bytes. *n* pode ser um valor de `1` a `8000`. O tamanho do armazenamento é *n* bytes. O valor padrão de *n* é `7`.  
  
 `uniqueidentifier`  
 É um GUID de 16 bytes.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Permissões  
 A criação de uma tabela requer permissão na função de banco de dados fixa `db_ddladmin` ou:
 - Permissão `CREATE TABLE` no banco de dados
 - Permissão `ALTER SCHEMA` no esquema que conterá a tabela. 

A criação de uma tabela particionada requer permissão na função de banco de dados fixa `db_ddladmin` ou

- Permissão `ALTER ANY DATASPACE`
  
 O logon que cria uma tabela temporária local recebe as permissões `CONTROL`, `INSERT`, `SELECT` e `UPDATE` na tabela.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>Comentários gerais  
 
Para saber os limites mínimo e máximo, confira [Limites de capacidade do SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/). 
 
### <a name="determining-the-number-of-table-partitions"></a>Determinar o número de partições da tabela
Cada tabela definida pelo usuário é dividida em várias tabelas menores que são armazenadas em locais separados chamados distribuições. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usa 60 distribuições. No [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], o número de distribuições depende do número de nós de computação.
 
Cada distribuição contém todas as partições da tabela. Por exemplo, se houver 60 distribuições e quatro partições de tabela mais uma partição vazia, haverá 300 partições (5 x 60 = 300). Se a tabela for um índice columnstore clusterizado, haverá um índice columnstore por partição, ou seja, haverá 300 índices columnstore.

É recomendável usar menos partições de tabela para garantir que cada índice columnstore tenha linhas suficientes para aproveitar os benefícios dos índices columnstore. Confira mais informações em [Tabelas de partição no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) e [Tabelas de indexação no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-index/)  

### <a name="rowstore-table-heap-or-clustered-index"></a>Tabela rowstore (índice de heap ou clusterizado)

Uma tabela rowstore é uma tabela armazenada em ordem de linha por linha. É um índice de heap ou clusterizado. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] cria todas as tabelas rowstore com compactação de página; esse comportamento não é configurável pelo usuário.

### <a name="columnstore-table-columnstore-index"></a>Tabela columnstore (índice columnstore)

Uma tabela columnstore é uma tabela armazenada em ordem de coluna por coluna. O índice columnstore é a tecnologia que gerencia os dados armazenados em uma tabela columnstore.  O índice columnstore clusterizado não afeta como os dados são distribuídos, mas afeta como os dados são armazenados dentro de cada distribuição.

Para converter uma tabela rowstore em uma tabela columnstore, remova todos os índices existentes na tabela e crie um índice columnstore clusterizado. Para obter um exemplo, confira [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).

Para obter mais informações, consulte estes tópicos:
- [Resumo de recursos com versão dos índices columnstore](https://msdn.microsoft.com/library/dn934994/)
- [Indexando tabelas no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-index/)
- [Guia de Índices columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md) 

<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Não é possível definir uma restrição DEFAULT em uma coluna de distribuição.  
  
### <a name="partitions"></a>Partições
Ao usar partições, a coluna de partição não pode ter uma ordenação somente Unicode. Por exemplo, a instrução a seguir falhará.  
  
 ```sql
CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))
```  
 
 Se *boundary_value* for um valor literal que precise ser convertido implicitamente no tipo de dados em *partition_column_name*, ocorrerá uma discrepância. O valor literal é exibido por meio das exibições do sistema do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], mas o valor convertido é usado para operações do [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

### <a name="temporary-tables"></a>Tabelas temporárias

 Não há compatibilidade com tabelas temporárias globais que começam com ##.  
  
 As tabelas temporárias locais têm as seguintes limitações e restrições:  
  
-   Eles são visíveis apenas para a sessão atual. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] descarta-as automaticamente no final da sessão. Para removê-las explicitamente, use a instrução DROP TABLE.   
-   Não podem ser renomeados. 
-   Não podem ter partições nem exibições.  
-   Suas permissões não podem ser alteradas. As instruções `GRANT`, `DENY` e `REVOKE` não podem ser usadas com tabelas temporárias locais.   
-   Os comandos do console do banco de dados são bloqueados para tabelas temporárias.   
-   Se mais de uma tabela temporária local for usada em um lote, cada uma precisará ter um nome exclusivo. Se várias sessões estiverem executando o mesmo lote e criando a mesma tabela temporária local, o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] acrescentará internamente um sufixo numérico ao nome de cada tabela temporária local para manter um nome exclusivo para cada uma delas.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Usa um bloqueio exclusivo na tabela. Usa um bloqueio compartilhado nos objetos de banco de dados DATABASE, SCHEMA e SCHEMARESOLUTION.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>Exemplos de colunas

### <a name="ColumnCollation"></a> A. Especificar uma ordenação de coluna 
 No exemplo a seguir, a tabela `MyTable` é criada com duas ordenações de coluna diferentes. Por padrão, a coluna `mycolumn1`, tem a ordenação padrão Latin1_General_100_CI_AS_KS_WS. A coluna `mycolumn2` tem a ordenação Frisian_100_CS_AS.  
  
```sql
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  
  
### <a name="DefaultConstraint"></a> B. Especificar uma restrição DEFAULT para uma coluna

 O exemplo a seguir mostra a sintaxe para especificar um valor padrão para uma coluna. A coluna colA tem uma restrição padrão chamada constraint_colA e o valor padrão 0.  
  
```sql
CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```

### <a name="OrderedClusteredColumnstoreIndex"></a> C. Criar um índice columnstore clusterizado ordenado

O exemplo a seguir mostra como criar um índice columnstore clusterizado ordenado. O índice é ordenado em SHIPDATE.

```sql
CREATE TABLE Lineitem  
WITH (DISTRIBUTION = ROUND_ROBIN, CLUSTERED COLUMNSTORE INDEX ORDER(SHIPDATE))  
AS  
SELECT * FROM ext_Lineitem
```

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>Exemplos de tabelas temporárias

### <a name="TemporaryTable"></a> C. Criar uma tabela temporária local  
 O exemplo a seguir cria uma tabela temporária local denominada #myTable. A tabela é especificada com um nome de três partes, que começa com um #.
  
```sql
CREATE TABLE AdventureWorks.dbo.#myTable
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>Exemplos de estrutura de tabela

### <a name="ClusteredColumnstoreIndex"></a> D. Criar uma tabela com um índice columnstore clusterizado  
 O exemplo a seguir cria uma tabela distribuída com um índice columnstore clusterizado. Cada distribuição será armazenada como um columnstore.  
  
 O índice columnstore clusterizado não afeta como os dados são distribuídos. Os dados sempre são distribuídos por linha. O índice columnstore clusterizado afeta como os dados são armazenados dentro de cada distribuição.  
  
```sql
  CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```  
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>Exemplos de distribuição da tabela

### <a name="RoundRobin"></a> E. Criar uma tabela ROUND_ROBIN  
 O exemplo a seguir cria uma tabela ROUND_ROBIN com três colunas e sem partições. Os dados são difundidos entre todas as distribuições. A tabela é criada com um ÍNDICE COLUMNSTORE CLUSTERIZADO, que fornece melhor desempenho e melhor compactação de dados do que um índice clusterizado rowstore ou de heap.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. Criar uma tabela distribuída por hash

 O exemplo a seguir cria a mesma tabela que o exemplo anterior. No entanto, para essa tabela, as linhas são distribuídas (na coluna `id`) em vez de serem difundidas aleatoriamente como em uma tabela ROUND_ROBIN. A tabela é criada com um ÍNDICE COLUMNSTORE CLUSTERIZADO, que fornece melhor desempenho e melhor compactação de dados do que um índice clusterizado rowstore ou de heap.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="Replicated"></a> G. Criar uma tabela replicada  
 O exemplo a seguir cria uma tabela replicada semelhante à dos exemplos anteriores. As tabelas replicadas são copiadas por completo para cada nó de computação. Com essa cópia em cada nó de computação, a movimentação de dados é reduzida para as consultas. Este exemplo é criado com um ÍNDICE CLUSTERIZADO, que fornece melhor compactação de dados que um heap. Um heap pode não conter linhas suficientes para obter uma boa compactação de ÍNDICE COLUMNSTORE CLUSTERIZADO.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>Exemplos de partições de tabela

###  <a name="PartitionedTable"></a> H. Criar uma tabela particionada

 O exemplo a seguir cria a mesma tabela, conforme é mostrado no exemplo A, com a adição do particionamento RANGE LEFT na coluna `id`. Ele especifica quatro valores de limite de partição, o que resulta em cinco partições.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
  (
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```  
  
 Neste exemplo, os dados serão classificados nas partições a seguir:  
  
- Partição 1: col <= 10
- Partição 2: 10 < col <= 20
- Partição 3: 20 < col <= 30
- Partição 4: 30 < col <= 40
- Partição 5: 40 < col  
  
 Se essa mesma tabela fosse particionada RANGE RIGHT em vez de RANGE LEFT (padrão), os dados seriam classificados nas partições a seguir:  
  
- Partição 1: col < 10  
- Partição 2: 10 <= col < 20
- Partição 3: 20 <= col < 30
- Partição 4: 30 <= col < 40
- Partição 5: 40 <= col  
  
### <a name="OnePartition"></a> I. Criar uma tabela particionada com uma partição

 O exemplo a seguir cria uma tabela particionada com uma partição. Ele não especifica nenhum valor de limite, o que resulta em uma partição.  
  
```sql
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
    (
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="DatePartition"></a> J. Criar uma tabela com particionamento de data

 O exemplo a seguir cria uma nova tabela nomeada `myTable`, com o particionamento em uma coluna `date`. Usando datas e RANGE RIGHT para os valores de limite, ele coloca um mês de dados em cada partição.  
  
```sql
CREATE TABLE myTable (  
    l_orderkey      bigint,
    l_partkey       bigint,
    l_suppkey       bigint,
    l_linenumber    bigint,
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH
  (
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>
## <a name="see-also"></a>Confira também
 
[CREATE TABLE AS SELECT &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
[sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql?view=azure-sqldw-latest) 
  
