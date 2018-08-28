---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 6/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f30febe9ab31ac58bbdd993a3e5034e5abcb427c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077300"
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Cria uma tabela externa para consultas do PolyBase ou do Banco de Dados Elástico. Dependendo do cenário, a sintaxe poderá variar consideravelmente. Uma tabela externa criada para o PolyBase não pode ser usada para consultas de Banco de Dados Elástico.  Da mesma forma, uma tabela externa criada para consultas do Banco de Dados Elástico não pode ser usada para o PolyBase, etc. 
  
> [!NOTE]  
>  O PolyBase é compatível apenas com o SQL Server 2016 (ou superior), o SQL Data Warehouse do Azure e o Parallel Data Warehouse. As consultas do Banco de Dados Elástico são compatíveis apenas com o Banco de Dados SQL do Azure v12 ou posterior.  


- O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tabelas externas para acessar os dados armazenados em um cluster Hadoop, um armazenamento de Blobs do Azure ou uma tabela externa do PolyBase que referencia os dados armazenados em um cluster Hadoop ou um armazenamento de Blobs do Azure. Também pode ser usado para criar uma tabela externa para uma [consulta de Banco de Dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Use uma tabela externa para:  
  
-   Consulte dados do Hadoop ou do Armazenamento de Blobs do Azure com instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Importe e armazene dados do Hadoop ou do Armazenamento de Blobs do Azure no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Criar uma tabela externa para uso com uma consulta  
     do Banco de Dados Elástico.  
     
- Importar e armazenar dados do Azure Data Lake Store no SQL Data Warehouse do Azure
  
 Consulte também [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
    | REJECT_TYPE = value | percentage,  
    | REJECT_VALUE = reject_value,  
    | REJECT_SAMPLE_VALUE = reject_sample_value,
    | REJECTED_ROW_LOCATION = '\REJECT_Directory'
  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*. [ schema_name ]. | schema_name. ] *table_name*  
 O nome de uma a três partes da tabela a ser criada. Para uma tabela externa, apenas os metadados da tabela são armazenados no SQL, junto com estatísticas básicas sobre o arquivo e/ou a pasta referenciada no Hadoop ou no Armazenamento de Blobs do Azure. Nenhum dado real é movido ou armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE permite uma ou mais definições de coluna. CREATE EXTERNAL TABLE e CREATE TABLE usam a mesma sintaxe para definir uma coluna. Uma exceção a isso é o fato de que não é possível usar a DEFAULT CONSTRAINT em tabelas externas. Para obter detalhes completos sobre definições de coluna e seus tipos de dados, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [CREATE TABLE no Banco de Dados SQL do Azure](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 As definições de coluna, incluindo os tipos de dados e o número de colunas, devem corresponder aos dados nos arquivos externos. Se houver uma incompatibilidade, as linhas do arquivo serão rejeitadas durante a consulta dos dados reais.  
  
 Para tabelas externas que referenciam arquivos em fontes de dados externas, as definições de coluna e tipo devem ser mapeadas para o esquema exato do arquivo externo. Ao definir tipos de dados que referenciam dados armazenados no Hadoop/Hive, use os mapeamentos a seguir entre tipos de dados SQL e Hive e converta o tipo em um tipo de dados SQL ao selecionar uma opção nele. Os tipos incluem todas as versões do Hive, a menos que indicado de outra forma.

> [!NOTE]  
>  O SQL Server não dá suporte ao valor de dados _infinity_ do Hive em uma conversão. O PolyBase falhará com um erro de conversão de tipo de dados.


|Tipo de dados SQL|Tipo de dados .NET|Tipo de dados do Hive|Tipo de dados do Hadoop/Java|Comentários|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|Apenas para números sem sinal.|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|INT|Int32|INT|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|Booliano|booleano|BooleanWritable||  
|FLOAT|Double|double|DoubleWritable||  
|REAL|Single|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|Cadeia de caracteres<br /><br /> Char[]|cadeia de caracteres|text||  
|NVARCHAR|Cadeia de caracteres<br /><br /> Char[]|cadeia de caracteres|Texto||  
|char|Cadeia de caracteres<br /><br /> Char[]|cadeia de caracteres|Texto||  
|varchar|Cadeia de caracteres<br /><br /> Char[]|cadeia de caracteres|Texto||  
|BINARY|Byte[]|BINARY|BytesWritable|Aplica-se ao Hive 0.8 e posterior.|  
|varbinary|Byte[]|BINARY|BytesWritable|Aplica-se ao Hive 0.8 e posterior.|  
|Data|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|DATETIME|DateTime|timestamp|TimestampWritable||  
|time|TimeSpan|timestamp|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|Aplica-se ao Hive 0.11 e posterior.|  
  
 LOCATION = '*folder_or_filepath*'  
 Especifica a pasta ou o caminho do arquivo e o nome de arquivo para os dados reais no Hadoop ou no Armazenamento de Blobs do Azure. O local começa na pasta raiz; a pasta raiz é o local de dados especificado na fonte de dados externa.  


No SQL Server, a instrução CREATE EXTERNAL TABLE cria o caminho e a pasta, caso ela ainda não exista. Em seguida, use INSERT INTO para exportar dados de uma tabela local do SQL Server para uma fonte de dados externa. Para obter mais informações, consulte [Consultas do PolyBase](/sql/relational-databases/polybase/polybase-queries). 

No SQL Data Warehouse e no Analytics Platform System, a instrução [CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) cria o caminho e a pasta, caso ela não exista. Nesses dois produtos, CREATE EXTERNAL TABLE não cria o caminho e a pasta.

  
 Se você especificar LOCATION para que ele seja uma pasta, uma consulta do PolyBase que seleciona por meio da tabela externa recuperará os arquivos da pasta e todas as suas subpastas. Assim como o Hadoop, o PolyBase não retorna pastas ocultas. Ele também não retorna arquivos dos quais o nome do arquivo começa com um sublinhado (_) ou um ponto final (.).  
  
 Neste exemplo, se 'LOCATION='/webdata/', uma consulta do PolyBase retornará linhas de mydata.txt e mydata2.txt.  Ele não retornará mydata3.txt porque ele é uma subpasta de uma pasta oculta. Ele não retornará _hidden.txt porque ele é um arquivo oculto.  
  
 ![Dados recursivos para tabelas externas](../../t-sql/statements/media/aps-polybase-folder-traversal.png "Recursive data for external tables")  
  
 Para alterar o padrão e somente leitura da pasta raiz, defina o atributo \<polybase.recursive.traversal> como 'false' no arquivo de configuração core-site.xml. Esse arquivo está localizado em `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Por exemplo, `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica o nome da fonte de dados externa que contém o local dos dados externos. Esse local é o Hadoop ou o Armazenamento de Blobs do Azure. Para criar uma fonte de dados externa, use [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica o nome do objeto de formato de arquivo externo que armazena o tipo de arquivo e o método de compactação para os dados externos. Para criar um formato de arquivo externo, use [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Opções de rejeição  
 Especifique parâmetros de rejeição que determinam como o PolyBase manipulará registros *sujos* recuperados da fonte de dados externa. Um registro de dados é considerado 'sujo' se os tipos de dados reais ou o número de colunas não correspondem às definições de coluna da tabela externa.  
  
 Quando você não especifica nem altera os valores de rejeição, o PolyBase usa valores padrão. Essas informações sobre os parâmetros de rejeição são armazenadas como metadados adicionais quando você cria uma tabela externa com a instrução CREATE EXTERNAL TABLE.   Quando uma instrução SELECT futura ou instrução INTO SELECT selecionar dados da tabela externa, o PolyBase usará as opções de rejeição para determinar o número ou o percentual de linhas que pode ser rejeitado antes que a consulta real falhe. para obter informações sobre a ferramenta de configuração e recursos adicionais. A consulta retornará resultados (parciais) até que o limite de rejeição seja excedido; em seguida, ela falhará com a mensagem de erro apropriada.  
  
 REJECT_TYPE = **value** | percentage  
 Esclarece se a opção REJECT_VALUE é especificada como um valor literal ou um percentual.  
  
 value  
 REJECT_VALUE é um valor literal, não um percentual. A consulta do PolyBase falhará quando o número de linhas rejeitadas exceder *reject_value*.  
  
 Por exemplo, se REJECT_VALUE = 5 e REJECT_TYPE = value, a consulta SELECT do PolyBase falhará depois de 5 linhas serem rejeitadas.  
  
 percentage  
 REJECT_VALUE é um percentual, não um valor literal. Uma consulta do PolyBase falhará quando o *percentage* de linhas com falha exceder *reject_value*. O percentual de linhas com falha é calculado em intervalos.  
  
 REJECT_VALUE = *reject_value*  
 Especifica o valor ou o percentual de linhas que pode ser rejeitado antes da falha da consulta.  
  
 Para REJECT_TYPE = value, *reject_value* deve ser um inteiro entre 0 e 2.147.483.647.  
  
 Para REJECT_TYPE = percentage, *reject_value* deve ser um float entre 0 e 100.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Esse atributo é obrigatório quando você especifica REJECT_TYPE = percentage. Ele determina o número de linhas de tentativa de recuperação antes que o PolyBase recalcule a percentual de linhas rejeitadas.  
  
 O parâmetro *reject_sample_value* deve ser um inteiro entre 0 e 2.147.483.647.  
  
 Por exemplo, se REJECT_SAMPLE_VALUE = 1000, o PolyBase calculará o percentual de linhas com falha depois de tentar importar 1000 linhas do arquivo de dados externo. Se o percentual de linhas com falha for menor que *reject_value*, o PolyBase tentará recuperar outras 1.000 linhas. Ele continuará recalculando o percentual de linhas com falha depois de tentar importar cada 1.000 linhas adicionais.  
  
> [!NOTE]  
>  Como o PolyBase calcula o percentual de linhas com falha em intervalos, o percentual real de linhas com falha pode exceder *reject_value*.  
  

Exemplo:  
  
 Este exemplo mostra como as três opções REJECT interagem. Por exemplo, se REJECT_TYPE = percentage, REJECT_VALUE = 30 e REJECT_SAMPLE_VALUE = 100, o seguinte cenário poderá ocorrer:  
  
-   O PolyBase tenta recuperar as 100 primeiras linhas; 25 falharão e 75 serão bem-sucedidas.  
  
-   O percentual de linhas com falha é calculado como 25%, que é menor que o valor de rejeição de 30%. Portanto, o PolyBase continuará recuperando dados da fonte de dados externa.  
  
-   O PolyBase tenta carregar as próximas 100 linhas; agora, 25 são bem-sucedidas e 75 falham.  
  
-   O percentual de linhas com falha é recalculado como 50%. O percentual de linhas com falha excedeu o valor de rejeição de 30%.  
  
-   A consulta do PolyBase falha com 50% de linhas rejeitadas depois de tentar retornar as 200 primeiras linhas. Observe que as linhas correspondentes foram retornadas antes de a consulta do PolyBase detectar que o limite de rejeição foi excedido.  
  
REJECTED_ROW_LOCATION = *Local do diretório*
  
  Especifica o diretório na fonte de dados externos em que as linhas rejeitadas e o arquivo de erro correspondente devem ser gravados.
Se o caminho especificado não existir, PolyBase criará um em seu nome. Um diretório filho é criado com o nome "_rejectedrows". O caractere “_” garante que o diretório tenha escape para outro processamento de dados, a menos que explicitamente nomeado no parâmetro de local. Dentro desse diretório, há uma pasta criada com base na hora do envio do carregamento no formato YearMonthDay – HourMinuteSecond (por exemplo, 20180330-173205). Nessa pasta, dois tipos de arquivos são gravados, o arquivo _reason e o arquivo de dados. 

Os arquivos de motivo e os arquivos de dados têm o queryID associado à instrução CTAS. Como os dados e o motivo estão em arquivos separados, arquivos correspondentes têm um sufixo correspondente. 
  
 Opções de tabela externa fragmentada  
 Especifica a fonte de dados externa (uma fonte de dados não SQL Server) e um método de distribuição para a [consulta do Banco de Dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Uma fonte de dados externa, como os dados armazenados em um Sistema de Arquivos Hadoop, no Armazenamento de Blobs do Azure ou em um [gerenciador de mapa de fragmentos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 A cláusula SCHEMA_NAME fornece a capacidade de mapear a definição da tabela externa para uma tabela em um esquema diferente no banco de dados remoto. Use isto para remover a ambiguidade entre os esquemas que existem nos bancos de dados locais e remotos.  
  
 OBJECT_NAME  
 A cláusula OBJECT_NAME fornece a capacidade de mapear a definição da tabela externa para uma tabela com um nome diferente no banco de dados remoto. Use isto para remover a ambiguidade entre os nomes de objetos que existem nos bancos de dados locais e remotos.  
  
 DISTRIBUTION  
 Opcional. Isso é necessário apenas para bancos de dados do tipo SHARD_MAP_MANAGER. Isso controla se uma tabela é tratada como uma tabela fragmentada ou uma tabela replicada. Com tabelas **SHARDED** (*column name*), os dados de tabelas diferentes não se sobrepõem. **REPLICATED** especifica que as tabelas têm os mesmos dados em cada fragmento. **ROUND_ROBIN** indica que um método específico ao aplicativo é usado para distribuir os dados.  
  
## <a name="permissions"></a>Permissões  
 Exige estas permissões de usuário:  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 Observe que o logon que cria a fonte de dados externa deve ter a permissão de leitura e gravação na fonte de dados externa, localizada no Hadoop ou no Armazenamento de Blobs do Azure.  


 > [!IMPORTANT]  

>  A permissão ALTER ANY EXTERNAL DATA SOURCE concede a qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais no escopo do banco de dados no banco de dados. Essa permissão precisa ser considerada como altamente privilegiada e, portanto, ser concedida somente para entidades de segurança confiáveis no sistema.

## <a name="error-handling"></a>Tratamento de erros  
 Ao executar a instrução CREATE EXTERNAL TABLE, o PolyBase tenta se conectar à fonte de dados externa. Se a tentativa de conexão falhar, a instrução falhará e a tabela externa não será criada. Pode levar um minuto ou mais para que o comando falhe, porque o PolyBase tenta a conexão novamente antes de, no fim, falhar a consulta.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Em cenários de consulta ad hoc, ou seja, SELECT FROM EXTERNAL TABLE, o PolyBase armazena as linhas recuperadas da fonte de dados externa em uma tabela temporária. Após a conclusão da consulta, o PolyBase remove e exclui a tabela temporária. Nenhum dado permanente é armazenado em tabelas SQL.  
  
 Por outro lado, no cenário de importação, ou seja, SELECT INTO FROM EXTERNAL TABLE, o PolyBase armazena as linhas recuperadas da fonte de dados externa como dados permanentes na tabela SQL. A nova tabela é criada durante a execução de consulta quando o Polybase recupera os dados externos.  
  
 O PolyBase pode enviar por push uma parte da computação de consulta para o Hadoop para melhorar o desempenho da consulta. Isso é chamado de aplicação de predicado. Para habilitar isso, especifique a opção de local do gerenciador de recursos do Hadoop em [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Você pode criar várias tabelas externas que referenciam as mesmas fontes de dados externas ou fontes diferentes.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 No CTP2, a funcionalidade de exportação, ou seja, o armazenamento permanente de dados do SQL na fonte de dados externa não é compatível. Essa funcionalidade estará disponível no CTP3.  
  
 Como os dados de uma tabela externa residem fora do dispositivo, eles não estão sob o controle do PolyBase e podem ser alterados ou removidos a qualquer momento por um processo externo. Por isso, não há garantia de que os resultados da consulta em uma tabela externa sejam determinísticos. A mesma consulta pode retornar resultados diferentes a cada vez que ela é executada em uma tabela externa. Da mesma forma, uma consulta pode falhar se os dados externos são removidos ou realocados.  
  
 Você pode criar várias tabelas externas que referenciam fontes de dados externas diferentes. No entanto, se você executar consultas simultaneamente em diferentes fontes de dados do Hadoop, cada fonte do Hadoop deverá usar a mesma definição de configuração do servidor 'hadoop connectivity'. Por exemplo, não é possível executar simultaneamente uma consulta em um cluster Cloudera Hadoop e um cluster Hortonworks Hadoop, pois eles usam configurações diferentes. Para obter definições de configuração e combinações compatíveis, consulte [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Somente estas instruções DDL (linguagem de definição de dados) são permitidas em tabelas externas:  
  
-   CREATE TABLE e DROP TABLE  
  
-   CREATE STATISTICS e DROP STATISTICS  
Observação: CREATE e DROP STATISTICS não são permitidas em tabelas externas no Banco de Dados SQL do Azure. 
  
-   CREATE VIEW e DROP VIEW  
  
 Constructos e operações não compatíveis:  
  
-   A restrição DEFAULT em colunas de tabela externa  
  
-   Operações DML (linguagem de manipulação de dados) de exclusão, inserção e atualização  
  
 Limitações da consulta:  
  
 O PolyBase pode consumir um máximo de 33 mil arquivos por pasta durante a execução de 32 consultas simultâneas do PolyBase. O número máximo inclui arquivos e subpastas em cada pasta do HDFS. Se o grau de simultaneidade é menor que 32, um usuário pode executar consultas do PolyBase em pastas do HDFS que contêm mais de 33 mil arquivos. Recomendamos que você mantenha os caminhos de arquivo externo curtos e use, no máximo, 30 mil arquivos por pasta do HDFS. Quando muitos arquivos são referenciados, pode ocorrer uma exceção de memória insuficiente da JVM (Máquina Virtual Java).  

Limitações de largura de tabela: o PolyBase no SQL Server 2016 tem um limite de largura de linha de 32 KB, com base no tamanho máximo de uma única linha válida por definição de tabela. Se a soma do esquema de coluna for maior que 32 KB, o PolyBase não poderá consultar os dados. 

No SQL Data Warehouse, essa limitação foi aumentada para 1 MB.


## <a name="locking"></a>Bloqueio  
 Bloqueio compartilhado no objeto SCHEMARESOLUTION.  
  
## <a name="security"></a>Segurança  
 Os arquivos de dados para uma tabela externa são armazenados no Hadoop ou no Armazenamento de Blobs do Azure. Esses arquivos de dados são criados e gerenciados por seus próprios processos. É sua responsabilidade gerenciar a segurança dos dados externos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Crie uma tabela externa com os dados em um formato delimitado por texto.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tem os dados formatados em arquivos delimitados por texto. Ele define uma fonte de dados externa *mydatasource* e um formato de arquivo externo *myfileformat*. Em seguida, esses objetos no nível do banco de dados são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Crie uma tabela externa com os dados no formato RCFile.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tem os dados formatados como RCFiles. Ele define uma fonte de dados externa *mydatasource_rc* e um formato de arquivo externo *myfileformat_rc*. Em seguida, esses objetos no nível do banco de dados são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
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
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Crie uma tabela externa com os dados no formato ORC.  
 Este exemplo mostra todas as etapas necessárias para criar uma tabela externa que tem os dados formatados como arquivos ORC. Ele define uma fonte de dados externa mydatasource_orc e um formato de arquivo externo myfileformat_orc. Em seguida, esses objetos no nível do banco de dados são referenciados na instrução CREATE EXTERNAL TABLE. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="d-querying-hadoop-data"></a>D. Consultando dados do Hadoop  
 Clickstream é uma tabela externa que se conecta ao arquivo de texto delimitado employee.tbl em um cluster Hadoop. A consulta a seguir se parece com uma consulta em uma tabela padrão. No entanto, essa consulta recupera dados do Hadoop e, em seguida, calcula os resultados.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Unir dados do Hadoop a dados do SQL  
 Essa consulta se parece com um JOIN padrão em duas tabelas SQL. A diferença é que o PolyBase recupera os dados de Clickstream do Hadoop e, em seguida, une-os na tabela UrlDescription. Uma tabela é uma tabela externa e a outra é uma tabela SQL padrão.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importar dados do Hadoop para uma tabela SQL  
 Este exemplo cria uma nova tabela SQL ms_user que armazena permanentemente o resultado de uma junção entre a tabela SQL padrão *user* e a tabela externa *ClickStream*.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Criar uma tabela externa para uma fonte de dados fragmentada  
 Este exemplo remapeia uma DMV remota para uma tabela externa usando as cláusulas SCHEMA_NAME e OBJECT_NAME.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importando dados do ADLS para o Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
WITH
(
    FORMAT_TYPE = DELIMITEDTEXT 
    , FORMAT_OPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
)


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH
(
    LOCATION='/DimProduct/' , 
    DATA_SOURCE = AzureDataLakeStore , 
    FILE_FORMAT = TextFileFormat , 
    REJECT_TYPE = VALUE ,
    REJECT_VALUE = 0
) ;


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
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Unir dados do HDFS a dados do PDW  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importar dados de linha do HDFS para uma Tabela distribuída do PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importar dados de linha do HDFS para uma Tabela replicada do PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos comuns de consulta de metadados (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



