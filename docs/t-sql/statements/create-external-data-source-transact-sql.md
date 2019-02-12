---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f3c92067adfc0469802c81d78a7267af2cd28cc
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421193"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Cria uma fonte de dados externa para consultas do PolyBase ou do Banco de Dados Elástico. Dependendo do cenário, a sintaxe poderá variar consideravelmente. Uma fonte de dados externa criada para o PolyBase não pode ser usada para consultas do Banco de Dados Elástico.  Da mesma forma, uma fonte de dados externa criada para consultas do Banco de Dados Elástico não pode ser usada para o PolyBase, etc. 
  
> [!NOTE]  
>  O PolyBase é compatível apenas com o SQL Server 2016 (ou superior), o SQL Data Warehouse do Azure e o Parallel Data Warehouse. As consultas do Banco de Dados Elástico são compatíveis apenas com o Banco de Dados SQL do Azure v12 ou posterior.  
  
 Para cenários do PolyBase, a fonte de dados externa é um HDFS (Sistema de Arquivos Hadoop), um contêiner do Azure Storage Blob ou um Azure Data Lake Store. Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 Para cenários de consulta do Banco de Dados Elástico, a fonte externa é um gerenciador de mapa de fragmentos (no Banco de Dados SQL do Azure) ou um banco de dados remoto (no Banco de Dados SQL do Azure).  Use [sp_execute_remote &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) depois de criar uma fonte de dados externa. Para obter mais informações, confira [Consulta do Banco de Dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  A fonte de dados externa do Armazenamento de Blobs do Azure é compatível com as sintaxes de `BULK INSERT` e `OPENROWSET` e é diferente do Armazenamento de Blobs do Azure para o PolyBase.
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Azure Data Lake Store Gen 2
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE ABFS 
WITH
(
              TYPE=HADOOP,
              LOCATION='abfs://<container>@<AzureDataLake account_name>.dfs.core.windows.net',
              CREDENTIAL=ABFS_Credemt
);
GO


-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]
        [, CREDENTIAL = credential_name]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source   
-- (on Parallel Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_source_name* Especifica o nome da fonte de dados definido pelo usuário. O nome precisa ser exclusivo no banco de dados no SQL Server, no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure. O nome precisa ser exclusivo no servidor no Parallel Data Warehouse.
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Especifica o tipo de fonte de dados. Use HADOOP quando a fonte de dados externa for o Hadoop ou o Azure Storage Blob para Hadoop. Use SHARD_MAP_MANAGER ao criar uma fonte de dados externa para consulta do Banco de Dados Elástico, para fragmentação no Banco de Dados SQL do Azure. Use o RDBMS com fontes de dados externas para consultas entre bancos de dados com a consulta do Banco de Dados Elástico no Banco de Dados SQL do Azure.  Use BLOB_STORAGE ao executar operações em massa usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
LOCATION = \<location_path> **HADOOP**    
Para HADOOP, especifica o URI (Uniform Resource Indicator) para um cluster do Hadoop.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: o nome do computador ou o endereço IP do Namenode do cluster do Hadoop.  
port: a porta de IPC do Namenode. Indicada pelo parâmetro de configuração fs.default.name no Hadoop. Se o valor não for especificado, 8020 será usado por padrão.  
Exemplo: `LOCATION = 'hdfs://10.10.10.10:8020'`

Para o Armazenamento de Blobs do Azure com Hadoop, especifica o URI para conectar-se ao Armazenamento de Blobs do Azure.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]: especifica o protocolo para o Armazenamento de Blobs do Azure. [s] é opcional e especifica uma conexão SSL segura. Os dados enviados do SQL Server são criptografados com segurança pelo protocolo SSL. É altamente recomendável usar 'wasbs' em vez de 'wasb'. Observe que o local pode usar asv[s] em vez de wasb[s]. A sintaxe de asv[s] foi preterida e será removida em uma versão futura.  
container: especifica o nome do contêiner de Armazenamento de Blobs do Azure. Para especificar o contêiner raiz de uma conta de armazenamento do domínio, use o nome de domínio em vez do nome do contêiner. Os contêineres raiz são somente leitura, portanto, os dados não podem ser gravados no contêiner.  
account_name: o FQDN (nome de domínio totalmente qualificado) da conta de Armazenamento do Azure.  
Exemplo: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Para o Azure Data Lake Store, o local especifica o URI para conectar-se ao Azure Data Lake Store.



**SHARD_MAP_MANAGER**   
 Para SHARD_MAP_MANAGER, especifica o nome do servidor do Banco de Dados SQL que hospeda o gerenciador de mapa de fragmentos no Banco de Dados SQL do Azure ou em um banco de dados do SQL Server em uma máquina virtual do Azure.
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

Para obter um tutorial passo a passo, confira [Introdução a consultas elásticas para fragmentação (particionamento horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/).
  
**RDBMS**   
Para o RDBMS, especifica o nome do servidor do Banco de Dados SQL do banco de dados remoto no Banco de Dados SQL do Azure.  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
Para obter um tutorial passo a passo sobre o RDBMS, confira [Introdução às consultas entre bancos de dados (particionamento vertical)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Esse tipo é usado apenas para operações em massa, `LOCATION` precisa ser uma URL válida para o contêiner e o Armazenamento de Blobs do Azure. Não coloque **/**, nome de arquivo ou parâmetros de Assinatura de Acesso Compartilhado no final da URL de `LOCATION`. `CREDENTIAL` será necessário se o objeto de blob não é público. Por exemplo: 
```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH (  TYPE = BLOB_STORAGE, 
        LOCATION = 'https://****************.blob.core.windows.net/invoices', 
        CREDENTIAL= MyAzureBlobStorageCredential    --> CREDENTIAL is not required if a blob has public access!
);
```
A credencial usada, deve ser criada usando `SHARED ACCESS SIGNATURE` como a identidade, não deve ter o `?` à esquerda no token SAS, deve ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`), e o período de validade deve ser válido (todas as datas estão no horário UTC). Por exemplo:
```sql
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';
```

Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para obter um exemplo de como acessar o Armazenamento de Blobs, veja o exemplo F de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 
>[!NOTE] 
>Para fazer o carregamento do armazenamento de Blobs do Azure no SQL DW ou no Parallel Data Warehouse, o Segredo deve ser a Chave de Armazenamento do Azure.

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 Especifica o local do gerenciador de recursos do Hadoop. Quando especificado, o otimizador de consulta pode tomar uma decisão baseada em custo para pré-processar os dados de uma consulta do PolyBase usando recursos de computação do Hadoop com o MapReduce. Chamado de pushdown de predicado, isso pode reduzir significativamente o volume de dados transferidos entre o Hadoop e o SQL e, portanto, melhorar o desempenho da consulta.  
  
 Quando não for especificado, o envio de computação por push para o Hadoop estará desabilitado para consultas do PolyBase.  
 
Se a porta não for especificada, o valor padrão será determinado usando a definição atual da configuração 'conectividade do Hadoop'.

|Conectividade do Hadoop|Porta do Gerenciador de Recursos padrão|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Para obter uma lista completa das distribuições do Hadoop e das versões compatíveis com cada valor de conectividade, confira [Configuração de conectividade do PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  O valor de RESOURCE_MANAGER_LOCATION é uma cadeia de caracteres e não é validado quando você cria a fonte de dados externa. Inserir um valor incorreto poderá causar atrasos futuros ao acessar o local.  
  
 Exemplos do Hadoop:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. 2.3 no Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 no Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2 e 2.3 no Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Hortonworks HDP 1.3 no Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Cloudera 4.3 no Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Cloudera 5.1 a 5.11 no Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 Especifica uma credencial no escopo do banco de dados para a autenticação na fonte de dados externa. Para obter um exemplo, confira [C. Criar uma fonte de dados externa do Armazenamento de Blobs do Azure](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Para criar uma credencial, confira [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Observe que a CREDENTIAL não é necessária para conjuntos de dados públicos que permitem acesso anônimo. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 O nome do banco de dados que funciona como o gerenciador do mapa de fragmentos (para o SHARD_MAP_MANAGER) ou o banco de dados remoto (para o RDBMS).  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Somente para o SHARD_MAP_MANAGER. O nome do mapa de fragmentos. Para obter mais informações de como criar um mapa de fragmentos, confira [Introdução à consulta do Banco de Dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>Observações específicas do PolyBase  
Para obter uma lista completa de fontes de dados externas compatíveis, confira [Configuração de conectividade do PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Para usar o PolyBase, você precisa criar estes três objetos:  
  
-   Uma fonte de dados externa.  
  
-   Um formato de arquivo externo e  
  
-   Uma tabela externa que referencia a fonte de dados externa e o formato de arquivo externo.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no banco de dados no SQL DW, no SQL Server, no APS 2016 e no BD SQL.

> [!IMPORTANT]  
>  Nas versões anteriores do PDW, a criação de fonte de dados externa exigia as permissões ALTER ANY EXTERNAL DATA SOURCE.
  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se as fontes de dados externas do Hadoop estiverem inconsistentes em relação à definição de RESOURCE_MANAGER_LOCATION, ocorrerá um erro de tempo de execução. Ou seja, não é possível especificar duas fontes de dados externas que referenciem o mesmo cluster do Hadoop e, em seguida, fornecer o local do Gerenciador de Recursos para uma e não para a outra.  
  
 O mecanismo do SQL não verifica a existência de fonte de dados externa quando cria o objeto de fonte de dados externa. Se a fonte de dados não existir durante a execução da consulta, ocorrerá um erro.  
  
## <a name="general-remarks"></a>Comentários gerais  
Para o PolyBase, a fonte de dados externa está no escopo do banco de dados no SQL Server e no SQL Data Warehouse. Ela está no escopo do servidor no Parallel Data Warehouse.
  
Para o PolyBase, quando RESOURCE_MANAGER_LOCATION ou JOB_TRACKER_LOCATION for definido, o otimizador de consulta considerará a otimização de cada consulta iniciando um trabalho de redução de mapa na fonte externa do Hadoop e efetuando pushdown da computação. Essa é uma decisão totalmente baseada em custo.  

Para garantir o sucesso das consultas do PolyBase no caso de failover do NameNode do Hadoop, considere usar um endereço IP virtual para o NameNode do cluster do Hadoop. Se você não usar um endereço IP virtual para o NameNode do Hadoop, no caso de um failover do NameNode do Hadoop, será necessário efetuar ALTER EXTERNAL DATA SOURCE no objeto para apontar para o novo local.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Todas as fontes de dados definidas no mesmo local do cluster do Hadoop precisam usar a mesma configuração de RESOURCE_MANAGER_LOCATION ou JOB_TRACKER_LOCATION. Se houver inconsistência, ocorrerá um erro de tempo de execução.  
  
 Se o cluster do Hadoop for configurado com um nome e a fonte de dados externa usar o endereço IP do local do cluster, o PolyBase ainda precisará ser capaz de resolver o nome do cluster quando a fonte de dados for usada. Para resolver o nome, você precisa habilitar um encaminhador de DNS.  
  
## <a name="locking"></a>Bloqueio  
 Coloca um bloqueio compartilhado no objeto EXTERNAL DATA SOURCE.  
  
##  <a name="examples"></a> Exemplos: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Criar uma fonte de dados externa para referenciar o Hadoop  
Para criar uma fonte de dados externa para referenciar o cluster do Hadoop do Hortonworks ou do Cloudera, especifique o nome do computador ou o endereço IP do Namenode do Hadoop e a porta.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>b. Criar uma fonte de dados externa para referenciar o Hadoop com pushdown habilitado  
Especifique a opção RESOURCE_MANAGER_LOCATION para habilitar o pushdown de computação para o Hadoop em consultas do PolyBase. Quando essa opção estiver habilitada, o PolyBase usará uma decisão baseada em custo para determinar se a computação da consulta deve ser enviada por push para o Hadoop ou se todos os dados devem ser movidos para processar a consulta no SQL Server.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Criar uma fonte de dados externa para referenciar o Hadoop protegido pelo Kerberos  
Para verificar se o cluster do Hadoop está protegido pelo Kerberos, verifique o valor da propriedade hadoop.security.authentication no core-site.xml do Hadoop. Para referenciar um cluster do Hadoop protegido pelo Kerberos, você precisa especificar uma credencial no escopo do banco de dados contendo o nome de usuário e a senha do Kerberos. A chave mestra do banco de dados é usada para criptografar o segredo da credencial no escopo do banco de dados. 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Criar uma fonte de dados externa para referenciar o Armazenamento de Blobs do Azure
Para criar uma fonte de dados externa para referenciar o contêiner de Armazenamento de Blobs do Azure, especifique o URI do Armazenamento de Blobs do Azure e uma credencial no escopo do banco de dados contendo a chave de conta de Armazenamento do Azure.

Neste exemplo, a fonte de dados externa é um contêiner do Armazenamento de Blobs do Azure chamado dailylogs na conta de Armazenamento do Azure chamada myaccount. A fonte de dados externa do Armazenamento do Azure é destinada apenas para transferência de dados e não é compatível com pushdown de predicado.

Este exemplo mostra como criar a credencial no escopo do banco de dados para autenticação no Armazenamento do Azure. Especifique a chave de conta de Armazenamento do Azure no segredo da credencial do banco de dados. Especifique qualquer cadeia de caracteres na identidade da credencial no escopo do banco de dados. Ela não será usada para autenticação no Armazenamento do Azure. A credencial será usada na instrução que cria uma fonte de dados externa.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Exemplos: Banco de dados SQL do Azure

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Criar uma fonte de dados externa do gerenciador de mapa de fragmentos
Para criar uma fonte de dados externa para referenciar um SHARD_MAP_MANAGER, especifique o nome do servidor do Banco de Dados SQL que hospeda o gerenciador de mapa de fragmentos no Banco de Dados SQL do Azure ou em banco de dados do SQL Server em uma máquina virtual do Azure.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. Criar uma fonte de dados externa do RDBMS
Para criar uma fonte de dados externa para referenciar um RDBMS, especifica o nome do servidor do Banco de Dados SQL do banco de dados remoto no Banco de Dados SQL do Azure.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>Exemplos: Azure SQL Data Warehouse

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. Criar uma fonte de dados externa para referenciar o Azure Data Lake Store
A conectividade do Azure Data Lake Store baseia-se no URI do ADLS e na entidade de serviço do aplicativo do Azure Active Directory. A documentação para criar esse aplicativo pode ser encontrada em [Autenticação do Data Lake Store usando o Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>Exemplos: Parallel Data Warehouse

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. Criar uma fonte de dados externa para referenciar o Hadoop com pushdown habilitado
Especifique a opção JOB_TRACKER_LOCATION para habilitar a computação de pushdown para Hadoop em consultas do PolyBase. Quando essa opção estiver habilitada, o PolyBase usará uma decisão baseada em custo para determinar se a computação da consulta deve ser enviada por push para o Hadoop ou se todos os dados devem ser movidos para processar a consulta no SQL Server. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. Criar uma fonte de dados externa para referenciar o Armazenamento de Blobs do Azure
Para criar uma fonte de dados externa para referenciar o contêiner de Armazenamento de Blobs do Azure, especifique o URI do Armazenamento de Blobs do Azure como o LOCATION da fonte de dados externa. Adicione a chave de conta de Armazenamento do Azure no arquivo core-site.xml do PDW para autenticação.

Neste exemplo, a fonte de dados externa é um contêiner do Armazenamento de Blobs do Azure chamado dailylogs na conta de Armazenamento do Azure chamada myaccount. A fonte de dados externa do Armazenamento do Azure é destinada apenas para transferência de dados e não é compatível com pushdown de predicado.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Exemplos: Operações em Massa   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. Criar uma fonte de dados externa para operações em massa recuperando dados do Armazenamento de Blobs do Azure.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Use a seguinte fonte de dados para operações em massa com [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). A credencial usada, deve ser criada usando `SHARED ACCESS SIGNATURE` como a identidade, não deve ter o `?` à esquerda no token SAS, deve ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`), e o período de validade deve ser válido (todas as datas estão no horário UTC). Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '(REMOVE ? FROM THE BEGINNING)******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Para ver esse exemplo em uso, confira [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage).
  
## <a name="see-also"></a>Consulte Também
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

