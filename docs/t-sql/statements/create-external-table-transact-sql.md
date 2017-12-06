---
title: Criar tabela externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/27/2017
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
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs: TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: "30"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: eab36ee612c3e559bf13db948c128ea6428063ae
ms.sourcegitcommit: 3cc7ffde800b451923c523fd549e8f4b4994f052
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
# <a name="create-external-table-transact-sql"></a>Criar tabela externa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Cria uma tabela externa PolyBase que faz referência a dados armazenados em um cluster de Hadoop ou armazenamento de BLOBs do Azure. Também pode ser usado para criar uma tabela externa para [consulta de banco de dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Use uma tabela externa para:  
  
-   Consultar dados de armazenamento de blob do Azure ou Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções.  
  
-   Importar e armazenar dados de armazenamento de BLOBs do Azure ou Hadoop em seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
-   Criar uma tabela externa para uso com um banco de dados Elástico  
     consulta.  
     
- Importar e armazenar dados do repositório Azure Data Lake no Azure SQL Data Warehouse
  
 Consulte também [criar fonte de dados externa &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) e [Remover tabela externa &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_Name* . [schema_name]. | schema_name. ] *table_name*  
 Um a três - parte nome da tabela para criar. Para uma tabela externa, apenas os metadados da tabela são armazenados no SQL com estatísticas básicas sobre o arquivo e/ou pasta referenciado no armazenamento de BLOBs do Azure ou Hadoop. Nenhum dado real é movido ou armazenado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<column_definition > [,...  *n*  ] CREATE EXTERNAL TABLE permite que uma ou mais definições de coluna. CREATE EXTERNAL TABLE e CREATE TABLE usam a mesma sintaxe para definir uma coluna. Uma exceção a isso, você não pode usar a restrição padrão em tabelas externas. Para obter detalhes completos sobre definições de coluna e seus tipos de dados, consulte [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) e [criar tabela no banco de dados SQL do Azure](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 As definições de coluna, incluindo o número de colunas e tipos de dados deve corresponder aos dados dos arquivos externos. Se houver uma incompatibilidade, as linhas do arquivo serão rejeitadas ao consultar os dados reais.  
  
 Para tabelas externas que fazem referência a arquivos em fontes de dados externas, as definições de coluna e tipo devem mapear para o esquema exato do arquivo externo. Ao definir os tipos de dados que fazem referência a dados armazenados no Hive do Hadoop, use os seguintes mapeamentos entre tipos de dados SQL e o Hive e converter do tipo em um tipo de dados SQL ao selecionar a partir dele. Os tipos incluem todas as versões do Hive, a menos que indicado de outra forma.

> [!NOTE]  
>  SQL Server não dá suporte para o Hive _infinito_ valor dos dados em qualquer conversão. PolyBase falhará com um erro de conversão de tipo de dados.


|Tipo de dados SQL|Tipo de dados .NET|Tipo de dados de hive|Tipo de dados Hadoop/Java|Comentários|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|Para apenas números não assinados.|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|Booliano|booleano|BooleanWritable||  
|float|Double|double|DoubleWritable||  
|real|Single|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|nchar|Cadeia de caracteres<br /><br /> Char]|cadeia de caracteres|text||  
|nvarchar|Cadeia de caracteres<br /><br /> Char]|cadeia de caracteres|Texto||  
|char|Cadeia de caracteres<br /><br /> Char]|cadeia de caracteres|Texto||  
|varchar|Cadeia de caracteres<br /><br /> Char]|cadeia de caracteres|Texto||  
|binary|Byte[]|binary|BytesWritable|Aplica-se a seção 0,8 e posterior.|  
|varbinary|Byte[]|binary|BytesWritable|Aplica-se a seção 0,8 e posterior.|  
|date|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|datetime|DateTime|timestamp|TimestampWritable||  
|time|TimeSpan|timestamp|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|Aplica-se ao Hive0.11 e posterior.|  
  
 LOCAL = '*folder_or_filepath*'  
 Especifica a pasta ou o caminho do arquivo e o nome de arquivo para os dados reais no armazenamento de BLOBs do Azure ou Hadoop. Inicia o local da pasta raiz; a pasta raiz é o local de dados especificado na fonte de dados externa.  
  
 Se você especificar o local para uma pasta, uma consulta do PolyBase que seleciona da tabela externa recuperará os arquivos da pasta e todas as suas subpastas. Assim como Hadoop, PolyBase não retorna as pastas ocultas. Ele também não retornar os arquivos para o qual o nome do arquivo começa com um sublinhado (_) ou um ponto (.).  
  
 Neste exemplo, se local = 'webdata /', uma consulta do PolyBase retornará linhas de mydata.txt e mydata2.txt.  Ela não retornará mydata3.txt porque ela é uma subpasta de uma pasta oculta. Ela não retornará _hidden.txt porque ele é um arquivo oculto.  
  
 ![Dados recursivos para tabelas externas](../../t-sql/statements/media/aps-polybase-folder-traversal.png "dados recursivos para tabelas externas")  
  
 Para alterar o padrão e somente leitura na pasta raiz, defina o atributo \<polybase.recursive.traversal > como 'false' no arquivo de configuração Core-site.XML. Esse arquivo está localizado em `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Por exemplo, `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica o nome da fonte de dados externa que contém o local dos dados externos. Esse local é o armazenamento de BLOBs do Azure ou um Hadoop. Para criar uma fonte de dados externa, use [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica o nome do objeto de formato de arquivo externo que armazena o método de compactação e o tipo de arquivo para os dados externos. Para criar um formato de arquivo externo, use [CREATE EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Rejeitar opções  
 Você pode especificar parâmetros de rejeitar que determinam como manipulará PolyBase *sujas* registra recupera da fonte de dados externa. Um registro de dados é considerado 'sujos' se ele tipos de dados real ou o número de colunas não correspondem as definições de coluna da tabela externa.  
  
 Quando você não especificar ou alterar os valores de rejeitar, PolyBase usa valores padrão. Essas informações sobre os parâmetros de rejeitar são armazenadas como metadados adicionais quando você cria uma tabela externa com a instrução CREATE EXTERNAL TABLE.   Quando uma instrução SELECT futuras ou selecione INTO SELECT seleciona dados da tabela externa, o PolyBase usará as opções de rejeitar para determinar o número ou porcentagem de linhas que pode ser rejeitada antes que a consulta real falhe. . A consulta retornará resultados (parciais) até que o limite de rejeição for excedido; em seguida, falha com a mensagem de erro apropriado.  
  
 REJECT_TYPE = **valor** | porcentagem  
 Esclarece se a opção REJECT_VALUE é especificada como um valor literal ou uma porcentagem.  
  
 value  
 REJECT_VALUE é um valor literal, não uma porcentagem. A consulta do PolyBase falhará quando excede o número de linhas rejeitadas *reject_value*.  
  
 Por exemplo, se REJECT_VALUE = 5 e REJECT_TYPE = valor, o PolyBase consulta SELECT falhará após 5 linhas foram rejeitadas.  
  
 Porcentagem  
 REJECT_VALUE é uma porcentagem, não é um valor literal. Uma consulta do PolyBase falhará quando o *porcentagem* de linhas com falha excede *reject_value*. A porcentagem de linhas com falha é calculada em intervalos.  
  
 REJECT_VALUE = *reject_value*  
 Especifica o valor ou a porcentagem de linhas que pode ser rejeitada antes que a consulta falhe.  
  
 Para REJECT_TYPE = value, *reject_value* deve ser um inteiro entre 0 e 2.147.483.647.  
  
 Para REJECT_TYPE = porcentagem, *reject_value* deve ser um flutuante entre 0 e 100.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Esse atributo é necessário quando você especificar REJECT_TYPE = porcentagem. Determina o número de linhas para tentar recuperar antes que o PolyBase recalcula a porcentagem de linhas rejeitadas.  
  
 O *reject_sample_value* parâmetro deve ser um inteiro entre 0 e 2.147.483.647.  
  
 Por exemplo, se REJECT_SAMPLE_VALUE = 1000, PolyBase irá calcular a porcentagem de linhas com falha depois que ele tentou importar 1000 linhas do arquivo de dados externa. Se a porcentagem de linhas com falha for menor que *reject_value*, PolyBase tentará recuperar outro 1000 linhas. Ela continua a recalcular a porcentagem de linhas com falha quando ele tenta importar cada 1000 linhas adicionais.  
  
> [!NOTE]  
>  Desde que o PolyBase calcula a porcentagem de linhas com falha em intervalos, a porcentagem real de linhas com falha pode exceder *reject_value*.  
  
 Exemplo:  
  
 Este exemplo mostra como as três opções de rejeitar interagem entre si. Por exemplo, se REJECT_TYPE = porcentagem, REJECT_VALUE = 30 e REJECT_SAMPLE_VALUE = 100, o cenário a seguir pode ocorrer:  
  
-   PolyBase tenta recuperar as primeiras 100 linhas; 25 falharão e 75 bem-sucedida.  
  
-   Porcentagem de linhas com falha é calculada como 25%, que é menor que o valor de rejeição de 30%. Portanto, PolyBase continuará a recuperar dados da fonte de dados externa.  
  
-   PolyBase tenta carregar as próximo de 100 linhas; Esse tempo 25 êxito e falha de 75.  
  
-   Porcentagem de linhas com falha é recalculada como 50%. A porcentagem de linhas com falha excedeu o valor de rejeição de 30%.  
  
-   A consulta do PolyBase falhará com 50% rejeitadas linhas depois de tentar retornar as primeiras 200 linhas. Observe que as linhas correspondentes foram retornadas antes que a consulta do PolyBase detecta que excedeu o limite de rejeição.  
  
 Opções de tabela externa fragmentada  
 Especifica a fonte de dados externa (uma fonte de dados do SQL Server) e um método de distribuição para o [consulta de banco de dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Uma fonte de dados externa, como os dados armazenados em um sistema de arquivos Hadoop, o armazenamento de BLOBs do Azure, ou um [Gerenciador do mapa de fragmentos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 A cláusula SCHEMA_NAME fornece a capacidade de mapear a definição da tabela externa para uma tabela em um esquema diferente do banco de dados remoto. Use isto para resolver a ambiguidade entre os esquemas que existem no locais e remotos bancos de dados.  
  
 OBJECT_NAME  
 A cláusula OBJECT_NAME fornece a capacidade de mapear a definição da tabela externa para uma tabela com um nome diferente do banco de dados remoto. Use isto para resolver a ambiguidade entre os nomes de objeto que existem no locais e remotos bancos de dados.  
  
 DISTRIBUIÇÃO  
 Opcional. Isso só é necessário apenas para bancos de dados do tipo SHARD_MAP_MANAGER. Isso controla se uma tabela é tratada como uma tabela fragmentada ou uma tabela replicada. Com **SHARDED** (*nome de coluna*) tabelas, os dados de tabelas diferentes não se sobrepõem. **REPLICADAS** Especifica que as tabelas têm os mesmos dados em cada fragmento. **ROUND_ROBIN** indica que um método específico do aplicativo é usado para distribuir os dados.  
  
## <a name="permissions"></a>Permissões  
 Requer estas permissões de usuário:  
  
-   **CREATE TABLE**  
  
-   **ALTERAR QUALQUER ESQUEMA**  
  
-   **ALTERAR QUALQUER FONTE DE DADOS EXTERNA**  
  
-   **ALTERAR QUALQUER FORMATO DE ARQUIVO EXTERNO**  

-   **BANCO DE DADOS DE CONTROLE**
  
 Observe que o logon que cria a fonte de dados externa deve ter permissão para leitura e gravação para a fonte de dados externa, localizada no armazenamento de BLOBs do Azure ou Hadoop.  


 > [!IMPORTANT]  

>  A permissão ALTER ANY EXTERNAL DATA SOURCE concede qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais de banco de dados com escopo no banco de dados. Essa permissão deve ser considerada como altamente privilegiada e, portanto, deve ser concedida somente para entidades confiáveis no sistema.

## <a name="error-handling"></a>Tratamento de erros  
 Ao executar a instrução CREATE EXTERNAL TABLE, o PolyBase tenta se conectar à fonte de dados externa. Se a tentativa de conexão falhar, a instrução falhará e a tabela externa não será criada. Pode levar um minuto ou mais para o comando falha porque o PolyBase tentativas de conexão antes de falhar, eventualmente, a consulta.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Em cenários de consulta ad hoc, ou seja, selecione da tabela externa, o PolyBase armazena as linhas recuperadas da fonte de dados externa em uma tabela temporária. Após a conclusão da consulta, o PolyBase remove e exclui a tabela temporária. Nenhum dado permanente é armazenado em tabelas do SQL.  
  
 Por outro lado, o cenário de importação, ou seja, selecione em da tabela externa, o PolyBase armazena as linhas recuperadas da fonte de dados externa como permanente de dados na tabela SQL. A nova tabela é criada durante a execução de consulta quando Polybase recupera os dados externos.  
  
 PolyBase pode enviar alguns da computação de consulta para Hadoop para melhorar o desempenho da consulta. Isso é chamado de aplicação de predicado. Para habilitar isso, especifique a opção de local do Gerenciador de recursos Hadoop no [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Você pode criar várias tabelas externas que fazem referência a fontes de dados externas iguais ou diferentes.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 CTP2, a funcionalidade de exportação não tem suporte, ou seja, permanentemente armazenar dados do SQL na fonte de dados externa. Essa funcionalidade estará disponível no CTP3.  
  
 Como os dados para uma tabela externa residem fora do dispositivo, não está sob controle do PolyBase e pode ser alterada ou removida a qualquer momento por um processo externo. Por isso, os resultados de consulta em uma tabela externa não há garantia ser determinística. A mesma consulta pode retornar resultados diferentes cada vez que ele é executado em uma tabela externa. Da mesma forma, uma consulta pode falhar se os dados externos são removidos ou realocados.  
  
 Você pode criar várias tabelas externas que cada referência a fontes de dados externas diferentes. No entanto, se você executar consultas simultaneamente em diferentes fontes de dados do Hadoop, cada fonte de Hadoop deve usar a mesma configuração de configuração do servidor de 'conectividade do hadoop'. Por exemplo, você não pode executar simultaneamente uma consulta em relação a um cluster Cloudera Hadoop e um cluster Hortonworks Hadoop desde que essas configurações diferentes de uso. Para parâmetros de configuração e combinações com suporte, consulte [configuração do PolyBase &#40; Transact-SQL &#41; ](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Somente essas instruções de linguagem de definição de dados (DDL) são permitidas em tabelas externas:  
  
-   CREATE TABLE e DROP TABLE  
  
-   CRIAR estatísticas e DROP STATISTICS  
Observação: Criar e remover estatísticas em tabelas externas não têm suporte no banco de dados do SQL Azure. 
  
-   Criar modo de exibição e DROP VIEW  
  
 Construções e operações sem suporte:  
  
-   A restrição padrão em colunas de tabela externa  
  
-   Operações do Data Manipulation Language (DML) de delete, insert e update  
  
 Limitações de consulta:  
  
 PolyBase pode consumir um máximo de 33 k de arquivos por pasta durante a execução de 32 consultas simultâneas do PolyBase. O número máximo inclui arquivos e subpastas em cada pasta HDFS. Se o grau de simultaneidade é menor que 32, um usuário pode executar consultas do PolyBase em relação a pastas no HDFS que contêm mais de 33 k de arquivos. É recomendável que você mantenha caminhos de arquivo externo curtos e usa não mais do que 30 k de arquivos por pasta HDFS. Quando há muitos arquivos são referenciados, pode ocorrer uma exceção de falta de memória da máquina Virtual Java (JVM).  

Limitações de largura de tabela: PolyBase no SQL Server 2016 tem um limite de largura de linha de 32KB, com base no tamanho máximo de uma única linha válido por definição de tabela. Se a soma do esquema de coluna for maior do que 32KB, o PolyBase não poderão consultar os dados. 

No SQL Data Warehouse, essa limitação foi aumentada para 1MB.


## <a name="locking"></a>Bloqueio  
 Compartilhado bloqueio no objeto SCHEMARESOLUTION.  
  
## <a name="security"></a>Segurança  
 Os arquivos de dados para uma tabela externa é armazenado no armazenamento de BLOBs do Azure ou Hadoop. Esses arquivos de dados são criados e gerenciados por seus próprios processos. É sua responsabilidade de gerenciar a segurança dos dados externos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Crie uma tabela externa com dados em formato delimitado por texto.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tenha dados formatados em arquivos de texto delimitado. Define uma fonte de dados externa *minhaFonteDeDados* e um formato de arquivo externo *myfileformat*. Esses objetos de nível de banco de dados, em seguida, são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) e [criar formato de arquivo externo &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Crie uma tabela externa com dados no formato RCFile.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tenha dados formatados como RCFiles. Define uma fonte de dados externa *mydatasource_rc* e um formato de arquivo externo *myfileformat_rc*. Esses objetos de nível de banco de dados, em seguida, são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) e [criar formato de arquivo externo &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Crie uma tabela externa com dados no formato ORC.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tenha dados formatados como arquivos ORC. Ele define um mydatasource_orc de fonte de dados externa e um myfileformat_orc de formato de arquivo externo. Esses objetos de nível de banco de dados, em seguida, são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) e [criar formato de arquivo externo &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. Consultar dados do Hadoop  
 Sequência de cliques é uma tabela externa que se conecta ao arquivo de texto delimitado employee.tbl em um cluster Hadoop. A consulta a seguir se parece com uma consulta em uma tabela padrão. No entanto, essa consulta recupera dados do Hadoop e, em seguida, calcula o ocorrerá.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Unir dados Hadoop com dados do SQL  
 Essa consulta se parece com uma associação padrão em duas tabelas SQL. A diferença é que o PolyBase recupera os dados de sequência de cliques do Hadoop e une-o para a tabela UrlDescription. Uma tabela é uma tabela externa e a outra é uma tabela SQL padrão.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importar dados do Hadoop em uma tabela SQL  
 Este exemplo cria uma nova tabela ms_user do SQL que armazena o resultado de uma junção entre a tabela SQL padrão *usuário* e a tabela externa *ClickStream*.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Crie uma tabela externa para uma fonte de dados fragmentados  
 Este exemplo remapeia uma DMV remoto para uma tabela externa usando as cláusulas SCHEMA_NAME e OBJECT_NAME.  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importação de dados do ADLS no Azure[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. Unir tabelas externas  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Unir dados HDFS com dados do PDW  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importar dados de linha de HDFS para uma tabela distribuída do PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importar dados de linha de HDFS para uma tabela replicada do PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos comuns de consulta de metadados (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [Criar tabela externa como SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Criar tabela como SELECT &#40; Depósito de dados SQL do Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



