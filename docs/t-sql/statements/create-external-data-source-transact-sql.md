---
title: Criar fonte de dados externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
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
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: "58"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 283971bbd1bfe04b26860f56601c315ac5244717
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="create-external-data-source-transact-sql"></a>Criar fonte de dados externa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Cria uma fonte de dados externa para o PolyBase, consultas de banco de dados Elástico ou armazenamento de BLOBs do Azure. Dependendo do cenário, a sintaxe irá diferir significativamente. Uma fonte de dados criada para PolyBase não pode ser usada para consultas de banco de dados Elástico.  Da mesma forma, uma fonte de dados criada para consultas de banco de dados Elástico não pode ser usada para o PolyBase, etc. 
  
> [!NOTE]  
>  PolyBase só tem suporte em SQL Server 2016, o Azure SQL Data Warehouse e o Parallel Data Warehouse. Consultas de banco de dados Elásticos têm suporte apenas no banco de dados SQL v12 ou posterior.  
  
 Para cenários de PolyBase, a fonte de dados externa é um sistema de arquivo Hadoop (HDFS), um contêiner de blob de armazenamento do Azure ou repositório Azure Data Lake. Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 Para cenários de consulta de banco de dados Elástico fonte externa é um Gerenciador de mapa do fragmento (no banco de dados SQL Azure) ou um banco de dados remoto (no banco de dados SQL Azure).  Use [sp_execute_remote &#40; Banco de dados SQL do Azure &#41; ](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) depois de criar uma fonte de dados externa. Para obter mais informações, consulte [consulta de banco de dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  Fonte de dados externos de armazenamento de BLOBs do Azure dá suporte a `BULK INSERT` e `OPENROWSET` sintaxe e é diferente de armazenamento de BLOBs do Azure para PolyBase.
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
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

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
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
 *data_source_name* Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo no banco de dados no SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse. O nome deve ser exclusivo dentro do servidor no Parallel Data Warehouse.
  
 TIPO = [HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Especifica o tipo de fonte de dados. Use o HADOOP quando a fonte de dados externa é Hadoop ou blob de armazenamento do Azure para Hadoop. Use SHARD_MAP_MANAGER ao criar uma fonte de dados externa para consulta de banco de dados Elástico fragmentação no banco de dados do SQL Azure. Use o RDBMS com fontes de dados externas para consultas de bancos de dados com a consulta de banco de dados Elástico no banco de dados do SQL Azure.  Use BLOB_STORAGE ao executar operações em massa usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
LOCAL = \<location_path > **HADOOP**    
Para HADOOP, especifica o URI Uniform Resource Indicator () para um cluster Hadoop.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: O nome do computador ou endereço IP do cluster Hadoop Namenode.  
porta: porta de IPC de Namenode o. Isso é indicado pelo parâmetro de configuração fs.default.name no Hadoop. Se o valor não for especificado, 8020 será usado por padrão.  
Exemplo: `LOCATION = 'hdfs://10.10.10.10:8020'`

Para o armazenamento de BLOBs do Azure com Hadoop, especifica o URI para se conectar ao armazenamento de BLOBs do Azure.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: Especifica o protocolo para o armazenamento de BLOBs do Azure. [S] é opcional e especifica uma conexão SSL segura; dados enviados do SQL Server são criptografados com segurança por meio do protocolo SSL. É altamente recomendável usar wasbs em vez de 'wasb'. Observe que o local pode usar asv [s] em vez de wasb [s]. A sintaxe de asv [s] foi substituída e será removida em uma versão futura.  
contêiner: Especifica o nome do contêiner de armazenamento de BLOBs do Azure. Para especificar o contêiner raiz do domínio conta de armazenamento, use o nome de domínio em vez do nome do contêiner. Contêineres de raiz são somente leitura, para que os dados não podem ser gravados para o contêiner.  
account_name: O nome de domínio totalmente qualificado (FQDN) da conta de armazenamento do Azure.  
Exemplo: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Para o repositório do Azure Data Lake local Especifica o URI para se conectar ao seu repositório Azure Data Lake.



**SHARD_MAP_MANAGER**   
 Para SHARD_MAP_MANAGER, especifica o nome do servidor lógico que hospeda o Gerenciador de mapa de fragmento no banco de dados SQL ou um banco de dados do SQL Server em uma máquina virtual do Azure.
 
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

Para obter um tutorial passo a passo, consulte [guia de Introdução com consultas Elásticos de fragmentação (particionamento horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/).
  
**RDBMS**   
Para o RDBMS, especifica o nome do servidor lógico do banco de dados remoto no banco de dados do SQL Azure.  

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
  
Para obter um tutorial passo a passo em RDBMS, consulte [guia de Introdução com consultas de bancos de dados (particionamento vertical)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Para as operações em massa, `LOCATION` devem ser válidas a URL para o armazenamento de BLOBs do Azure e o contêiner. Não coloque  **/** , nome de arquivo ou compartilhado parâmetros de assinatura de acesso no final de `LOCATION` URL.   
A credencial usada, deve ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para obter um exemplo de como acessar o armazenamento de blob, consulte o exemplo F de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*porta*]'  
 Especifica o local do Gerenciador de recursos Hadoop. Quando especificado, o otimizador de consulta pode fazer uma decisão baseada em custo para pré-processar dados de uma consulta do PolyBase usando recursos de computação do Hadoop com MapReduce. Chamado a aplicação de predicado, isso pode reduzir significativamente o volume de dados transferidos entre Hadoop e SQL e, portanto, melhorar o desempenho da consulta.  
  
 Quando isso não for especificado, envio de computação para Hadoop está desabilitada para consultas do PolyBase.  
 
Se a porta não for especificada, o valor padrão é determinado usando a configuração atual para a configuração de 'conectividade do hadoop'.

|Conectividade do Hadoop|Porta do Gerenciador de recursos padrão|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Para obter uma lista completa de distribuições do Hadoop e versões compatíveis com cada valor de conectividade, consulte [configuração do PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  O valor RESOURCE_MANAGER_LOCATION é uma cadeia de caracteres e não é validado quando você criar a fonte de dados externa. Inserir um valor incorreto pode causar atrasos futuros ao acessar o local.  
  
 Exemplos de Hadoop:  
  
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
  
-   Cloudera 5.1 5.11 no Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENCIAL = *credential_name*  
 Especifica uma credencial no escopo do banco de dados para autenticar a fonte de dados externa. Para obter um exemplo, consulte [C. Crie uma fonte de dados externos de armazenamento de BLOBs do Azure](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Para criar uma credencial, consulte [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Observe que a CREDENCIAL não é necessária para conjuntos de dados públicos que permitem o acesso anônimo. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 O nome do banco de dados que funciona como o Gerenciador do mapa de fragmento (para SHARD_MAP_MANAGER) ou o banco de dados remoto (para o RDBMS).  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Para SHARD_MAP_MANAGER. O nome do mapa do fragmento. Para obter mais informações sobre como criar um mapa do fragmento, consulte [Introdução à consulta de banco de dados Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>Anotações específicas para PolyBase  
Para obter uma lista completa de fontes de dados externas com suporte, consulte [configuração do PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Para usar o PolyBase, você precisa criar essas três objetos:  
  
-   Uma fonte de dados externa.  
  
-   Um formato de arquivo externo, e  
  
-   Uma tabela externa que referencia a fonte de dados externa e o formato de arquivo externo.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CONTROL no banco de dados no SQL DW, SQL Server, APS 2016 e banco de dados SQL.

> [!IMPORTANT]  
>  Em versões anteriores do PDW, crie permissões de ALTER ANY EXTERNAL DATA SOURCE de necessárias de fonte de dados externa.
  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se as fontes de dados externas do Hadoop são inconsistentes sobre ter RESOURCE_MANAGER_LOCATION definida, ocorrerá um erro de tempo de execução. Ou seja, você não pode especificar duas fontes de dados externas que referenciam o mesmo cluster de Hadoop e, em seguida, fornecer o local do Gerenciador de recursos para um e não para outros.  
  
 O mecanismo do SQL não verifica a existência de fonte de dados externa quando ele cria o objeto de fonte de dados externa. Se a fonte de dados não existe durante a execução de consulta, ocorrerá um erro.  
  
## <a name="general-remarks"></a>Comentários gerais  
Para PolyBase, a fonte de dados externa é o escopo do banco de dados no SQL Server e SQL Data Warehouse. Ele está no escopo do servidor no Parallel Data Warehouse.
  
Para o PolyBase, quando RESOURCE_MANAGER_LOCATION ou JOB_TRACKER_LOCATION é definida, o otimizador de consulta considerará otimizando a cada consulta por meio de um mapa de reduzir o trabalho na fonte externa do Hadoop e enviar por push para baixo de computação. Isso é totalmente uma decisão baseada em custo.  

Para garantir que as consultas do PolyBase com êxito no caso de failover de Hadoop NameNode, considere o uso de um endereço IP virtual para NameNode do cluster Hadoop. Se você não usar um endereço IP virtual para o Hadoop NameNode, no caso de um failover de Hadoop NameNode você terá ao objeto de fonte de dados externa ALTER para apontar para o novo local.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Todas as fontes de dados definidas no mesmo local do cluster Hadoop devem usar a mesma configuração para RESOURCE_MANAGER_LOCATION ou JOB_TRACKER_LOCATION. Se houver uma inconsistência, ocorrerá um erro de tempo de execução.  
  
 Se o cluster Hadoop é configurado com um nome e a fonte de dados externos usa o endereço IP para o local do cluster, PolyBase ainda deve ser capaz de resolver o nome do cluster quando a fonte de dados é usada. Para resolver o nome, você deve habilitar um encaminhador DNS.  
  
## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado no objeto de fonte de dados externa.  
  
##  <a name="examples"></a>Exemplos: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Criar fonte de dados externa a referência de Hadoop  
Para criar uma fonte de dados externa para fazer referência a seu cluster Hortonworks ou Cloudera Hadoop, especifique o nome do computador ou endereço IP do Namenode de Hadoop e a porta.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Criar fonte de dados externa para referência Hadoop com a aplicação de habilitado  
Especifique a opção RESOURCE_MANAGER_LOCATION para habilitar a computação de propagação para Hadoop para consultas do PolyBase. Uma vez habilitada, o PolyBase usa uma decisão baseada em custo para determinar se a computação de consulta deve ser enviada para o Hadoop ou todos os dados devem ser movidos para processar a consulta no SQL Server.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Criar fonte de dados externa para fazer referência a Hadoop protegido por Kerberos  
Para verificar se o cluster Hadoop é protegido por Kerberos, verifique o valor da propriedade hadoop.security.authentication no Hadoop Core-site.XML. Para fazer referência a um cluster Hadoop protegido por Kerberos, você deve especificar uma credencial no escopo do banco de dados que contém o nome de usuário do Kerberos e a senha. A chave mestra de banco de dados é usada para criptografar o segredo de credencial no escopo do banco de dados. 
  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Criar fonte de dados externa para referenciar o armazenamento de BLOBs do Azure
Para criar uma fonte de dados externa para fazer referência a seu contêiner de armazenamento de BLOBs do Azure, especifique o URI de armazenamento de BLOBs do Azure e uma credencial no escopo do banco de dados que contém a chave da conta de armazenamento do Azure.

Neste exemplo, a fonte de dados externa é um contêiner de armazenamento de BLOBs do Azure chamado dailylogs sob a conta de armazenamento do Azure chamada minha conta. O armazenamento do Azure é de fonte de dados externa para a transferência de dados. e não dá suporte a aplicação de predicado.

Este exemplo mostra como criar a credencial no escopo do banco de dados para autenticação no armazenamento do Azure. Especifique a chave de conta de armazenamento do Azure o segredo de credencial de banco de dados. Especifique a identidade da credencial no escopo de qualquer cadeia de caracteres no banco de dados, ele não é usado para autenticação no armazenamento do Azure. Em seguida, a credencial é usada na instrução que cria uma fonte de dados externa.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Exemplos: Banco de dados do SQL Azure

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Criar uma fonte de dados externos de Gerenciador de mapa de fragmento
Para criar uma fonte de dados externa para fazer referência a um SHARD_MAP_MANAGER, especifique o nome do servidor lógico que hospeda o Gerenciador de mapa de fragmento no banco de dados SQL ou um banco de dados do SQL Server em uma máquina virtual do Azure.

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
Para criar uma fonte de dados externa para fazer referência a um RDBMS, especifica o nome de servidor lógico do banco de dados remoto no banco de dados do SQL Azure.

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

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. Criar fonte de dados externa para referência repositório Azure Data Lake
Conectividade do repositório Azure Data lake baseia-se em seu URI ADLS e entidade de serviço do Azure Active directory do seu aplicativo. Documentação para criar esse aplicativo pode ser encontrada em[autenticação do repositório Data lake usando o Active Directory](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

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

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. Criar fonte de dados externa para referência Hadoop com a aplicação de habilitado
Especifique a opção JOB_TRACKER_LOCATION para habilitar a computação de propagação para Hadoop para consultas do PolyBase. Uma vez habilitada, o PolyBase usa uma decisão baseada em custo para determinar se a computação de consulta deve ser enviada para o Hadoop ou todos os dados devem ser movidos para processar a consulta no SQL Server. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. Criar fonte de dados externa para referenciar o armazenamento de BLOBs do Azure
Para criar um externo fonte de dados para fazer referência a seu contêiner de armazenamento de BLOBs do Azure, especifique o URI de armazenamento de BLOBs do Azure como os dados externos local de origem. Adicione sua chave de conta de armazenamento do Azure para arquivo de Core-site.XML PDW para autenticação.

Neste exemplo, a fonte de dados externa é um contêiner de armazenamento de BLOBs do Azure chamado dailylogs sob a conta de armazenamento do Azure chamada minha conta. A fonte de dados externa do armazenamento do Azure destina-se somente a transferência de dados e não oferece suporte para aplicação de predicado.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Exemplos: Operações em massa   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. Crie uma fonte de dados externa para operações em massa recuperando dados do armazenamento de BLOBs do Azure.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Use a fonte de dados para operações em massa usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). A credencial usada, deve ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Para ver esse exemplo em uso, consulte [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).
  
## <a name="see-also"></a>Consulte Também
[ALTERAR a fonte de dados externa (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[Criar tabela externa como SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[Criar tabela como SELECT &#40; Depósito de dados SQL do Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

