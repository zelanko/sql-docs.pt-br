---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91711ce160dcb653d9e05e8b0a445214a247d337
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981881"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)

Cria uma fonte de dados externa para consultas do SQL Server, do Banco de Dados SQL, do SQL Data Warehouse ou do Analytics Platform System (Parallel Data Warehouse ou PDW).

Este artigo fornece a sintaxe, os argumentos, os comentários, as permissões e os exemplos de qualquer produto SQL que você escolher.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

|                               |                                                              |                                                              |                                                              |      |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| **_\* SQL Server \*_** &nbsp; | [Banco de Dados SQL](create-external-data-source-transact-sql.md?view=azuresqldb-current) | [SQL Data<br />Warehouse](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                               |                                                              |                                                              |                                                              |      |

&nbsp;

## <a name="overview-sql-server"></a>Visão geral: SQL Server

Cria uma fonte de dados externa para consultas do PolyBase. Fontes de dados externas são usadas para estabelecer a conectividade e dar suporte a estes casos de uso principal:

- Virtualização de dados e carregamento dados usando o [PolyBase][intro_pb]
- Operações de carregamento em massa usando `BULK INSERT` ou `OPENROWSET`

**APLICA-SE A**: SQL Server 2016 (ou posterior)

## <a name="syntax"></a>Sintaxe

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>  
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CONNECTION_OPTIONS        = '<name_value_pairs>']
[,   CREDENTIAL                = <credential_name> ]
[,   PUSHDOWN                  = ON | OFF]
[,   TYPE                      = HADOOP | BLOB_STORAGE ]
[,   RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]'
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo no banco de dados no SQL Server.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Fornece o protocolo de conectividade e o caminho para a fonte de dados externa.

| Fonte de dados externa    | Prefixo de local | Caminho de local                                         | Locais com suporte por produto/serviço |
| ----------------------- | --------------- | ----------------------------------------------------- | ---------------------------------------- |
| Cloudera ou Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   | SQL Server (2016+)                       |
| Armazenamento de blobs do Azure      | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` | SQL Server (2016+)                       |
| SQL Server              | `sqlserver`     | `<server_name>[\<instance_name>][:port]`              | SQL Server (2019+)                       |
| Oracle                  | `oracle`        | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| Teradata                | `teradata`      | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| MongoDB ou CosmosDB     | `mongodb`       | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| ODBC                    | `odbc`          | `<server_name>[:port]`                                | SQL Server (2019+) – somente Windows        |
| Operações em Massa         | `https`         | `<storage_account>.blob.core.windows.net/<container>` | SQL Server (2017+)                       |

Caminho de local:

- `<`Namenode`>` = o nome do computador, o URI do serviço de nome ou o endereço IP do `Namenode` no cluster do Hadoop. O PolyBase deve resolver qualquer nome DNS usado pelo cluster do Hadoop. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = a porta em que fonte de dados externa está escutando. No Hadoop, a porta pode ser encontrada usando o parâmetro de configuração `fs.defaultFS`. O padrão é 8020.
- `<container>` = o contêiner da conta de armazenamento que contém os dados. Os contêineres raiz são somente leitura, não é possível gravar dados no contêiner.
- `<storage_account>` = o nome da conta de armazenamento do recurso do Azure.
- `<server_name>` = o nome de host.
- `<instance_name>` = o nome de uma instância nomeada do SQL Server. Usado se você tiver o Serviço SQL Server Browser em execução na instância de destino.

Observações e orientação adicionais ao definir o local:

- O mecanismo do SQL não verifica a existência da fonte de dados externa quando o objeto é criado. Para validar, crie uma tabela externa usando a fonte de dados externa.
- Use a mesma fonte de dados externa para todas as tabelas ao consultar o Hadoop para garantir semântica de consulta consistente.
- Você pode usar o prefixo de local `sqlserver` para conectar o SQL Server 2019 ao SQL Server, Banco de Dados SQL ou SQL Data Warehouse.
- Especifique o `Driver={<Name of Driver>}` ao se conectar por meio de `ODBC`.
- `wasb` é o protocolo padrão para o armazenamento de blobs do Azure. `wasbs` é opcional, mas recomendado, pois os dados serão enviados usando uma conexão SSL segura.
- Para garantir consultas do PolyBase com êxito durante um failover `Namenode` do Hadoop, considere usar um endereço IP virtual para o `Namenode` do cluster do Hadoop. Se você não fizer isso, execute um comando [ALTER EXTERNAL DATA SOURCE][alter_eds] para apontar para o novo local.

### <a name="connection_options--key_value_pair"></a>CONNECTION_OPTIONS = *key_value_pair*

Especifica opções adicionais ao se conectar por meio de `ODBC` a uma fonte de dados externa.

O nome do driver é necessário como um mínimo, mas há outras opções, como `APP='<your_application_name>'` ou `ApplicationIntent= ReadOnly|ReadWrite`, que também é útil definir e podem ajudar a solucionar problemas.

Consulte a documentação do produto `ODBC` para obter uma lista de [CONNECTION_OPTIONS][connection_options] permitidas

### <a name="pushdown--on--off"></a>PUSHDOWN = *ON | OFF*

Informa se é possível realizar a aplicação da computação para a fonte de dados externa. Está ativado por padrão.

Há suporte para `PUSHDOWN` ao se conectar ao SQL Server, ao Oracle, ao Teradata, ao MongoDB ou ao ODBC no nível da fonte de dados externa.

Habilitar ou desabilitar a aplicação no nível da consulta é feito por meio de uma [dica][hint_pb].

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica uma credencial no escopo do banco de dados para a autenticação na fonte de dados externa.

Observações e orientações adicionais ao criar uma credencial:

- `CREDENTIAL` será necessário apenas se o blob tiver sido protegido. `CREDENTIAL` não é necessário para conjuntos de dados que permitem acesso anônimo.
- Quando o `TYPE` = `BLOB_STORAGE`, credencial usada precisa ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Além disso, o token SAS deve ser configurado da seguinte maneira:
  - Excluir o `?` à esquerda quando configurado como o segredo
  - Ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`)
  - Use um período de término válido (todas as datas estão no horário UTC).

Para ver um exemplo de como usar um `CREDENTIAL` com `SHARED ACCESS SIGNATURE` e `TYPE` = `BLOB_STORAGE`, veja [Criar uma fonte de dados externa para executar operações em massa e recuperar dados do Armazenamento de Blobs do Azure no Banco de Dados SQL](#f-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage)

Para criar uma credencial no escopo do banco de dados, veja [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type---hadoop--blob_storage-"></a>TYPE = *[ HADOOP | BLOB_STORAGE ]*

Especifica o tipo de fonte de dados externa que está sendo configurada. Esse parâmetro não é sempre necessário.

- Use HADOOP quando a fonte de dados externa for Cloudera, Hortonworks ou Armazenamento de Blobs do Azure.
- Use BLOB_STORAGE ao executar operações em massa com [BULK INSERT][bulk_insert] ou [OPENROWSET][openrowset] com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].

> [!IMPORTANT]
> Não defina `TYPE` se estiver usando qualquer outra fonte de dados externa.

Para ver um exemplo de como usar `TYPE` = `HADOOP` para carregar dados do Armazenamento de Blobs do Azure, veja [Criar fonte de dados externa para referenciar o Armazenamento de Blobs do Azure](#e-create-external-data-source-to-reference-azure-blob-storage).

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Configure esse valor opcional ao se conectar ao Hortonworks ou ao Cloudera.

Quando o `RESOURCE_MANAGER_LOCATION` for definido, o otimizador de consulta tomará uma decisão baseada em custo para melhorar o desempenho. Um trabalho MapReduce pode ser usado para aplicar a computação para o Hadoop. Especificar o `RESOURCE_MANAGER_LOCATION` pode reduzir significativamente o volume de dados transferidos entre o Hadoop e o SQL, o que pode levar a um desempenho de consultas aprimorado.  

Se o Resource Manager não tiver sido especificado, o envio de computação por push para o Hadoop estará desabilitado para consultas do PolyBase.

Se a porta não for especificada, o valor padrão será escolhido usando a definição atual da configuração 'conectividade do Hadoop'.

| Conectividade do Hadoop | Porta do Gerenciador de Recursos padrão |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

Para ver uma lista completa de versões do Hadoop compatíveis, veja [Configuração de conectividade do PolyBase (Transact-SQL)][connectivity_pb].

> [!IMPORTANT]  
> O valor de RESOURCE_MANAGER_LOCATION e não é validado quando você cria a fonte de dados externa. Inserir um valor incorreto pode causar falha de consulta em tempo de execução sempre que for feita uma tentativa de aplicação, uma vez que o valor fornecido não poderá ser resolvido.

[Criar fonte de dados externa para referenciar o Hadoop com aplicação habilitada](#c-create-external-data-source-to-reference-hadoop-with-push-down-enabled) apresenta um exemplo concreto e diretrizes adicionais.

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL no banco de dados no SQL Server.

## <a name="locking"></a>Bloqueio

Coloca um bloqueio compartilhado no objeto EXTERNAL DATA SOURCE.  

## <a name="security"></a>Segurança

O PolyBase dá suporte para autenticação baseada em proxy para a maioria das fontes de dados externas. Crie uma credencial no escopo do banco de dados para criar a conta proxy.

Quando você se conecta ao pool de armazenamento ou de dados em um cluster de Big Data do SQL Server, as credenciais do usuário são passadas para o sistema de back-end. Crie logons no pool de dados propriamente dito para habilitar a autenticação de passagem.

No momento, não há suporte para um token SAS com o tipo `HADOOP`. Ele só é compatível com uma chave de acesso da conta de armazenamento. Tentar criar uma fonte de dados externa com o tipo `HADOOP` e uma credencial SAS falha com o seguinte erro:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples-sql-server-2016"></a>Exemplos: SQL Server (2016+)

### <a name="a-create-external-data-source-in-sql-2019-to-reference-oracle"></a>A. Criar fonte de dados externa no SQL de 2019 para fazer referência ao Oracle

Para criar uma fonte de dados externa que faça referência ao Oracle, verifique se que você tem uma credencial no escopo do banco de dados. Opcionalmente, você também poderá habilitar ou desabilitar a aplicação de computação em relação a essa fonte de dados.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '!MyC0mpl3xP@ssw0rd!
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL OracleProxyAccount
WITH
     IDENTITY   = 'oracle_username'
,    SECRET     = 'oracle_password'
;

CREATE EXTERNAL DATA SOURCE MyOracleServer
WITH
(    LOCATION   = 'oracle://145.145.145.145:1521'
,    CREDENTIAL = OracleProxyAccount
,    PUSHDOWN   = ON
,    TYPE=BLOB_STORAGE
)
;
```

Para ver mais exemplos para outras fontes de dados, como o MongoDB, veja [Configurar o PolyBase para acessar dados externos no MongoDB][mongodb_pb]

### <a name="b-create-external-data-source-to-reference-hadoop"></a>B. Criar uma fonte de dados externa para referenciar o Hadoop

Para criar uma fonte de dados externa para referenciar o cluster do Hadoop do Hortonworks ou do Cloudera, especifique o nome do computador ou o endereço IP do `Namenode` do Hadoop e a porta. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION = 'hdfs://10.10.10.10:8050'
,    TYPE     = HADOOP
)
;
```

### <a name="c-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>C. Criar uma fonte de dados externa para referenciar o Hadoop com aplicação habilitada

Especifique a opção `RESOURCE_MANAGER_LOCATION` para habilitar a computação de aplicação para Hadoop em consultas do PolyBase. Uma vez habilitado, o PolyBase toma uma decisão baseada em custo para determinar se a computação de consulta deve ser enviada por push para o Hadoop.

```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8020'
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="d-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>D. Criar uma fonte de dados externa para referenciar o Hadoop protegido pelo Kerberos

Para verificar se o cluster do Hadoop está protegido pelo Kerberos, verifique o valor da propriedade hadoop.security.authentication no core-site.xml do Hadoop. Para referenciar um cluster do Hadoop protegido pelo Kerberos, você precisa especificar uma credencial no escopo do banco de dados contendo o nome de usuário e a senha do Kerberos. A chave mestra do banco de dados é usada para criptografar o segredo da credencial no escopo do banco de dados.

```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
     IDENTITY   = '<hadoop_user_name>'
,    SECRET     = '<hadoop_password>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8050'
,    CREDENTIAL                = HadoopUser1
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="e-create-external-data-source-to-reference-azure-blob-storage"></a>E. Criar uma fonte de dados externa para referenciar o Armazenamento de Blobs do Azure

Neste exemplo, a fonte de dados externa é um contêiner do Armazenamento de Blobs do Azure chamado `daily` na conta de Armazenamento do Azure chamada `logs`. A fonte de dados externa do armazenamento do Azure destina-se somente a transferência de dados. Não dá suporte a aplicação de predicado.

Este exemplo mostra como criar a credencial no escopo do banco de dados para autenticação no Armazenamento do Azure. Especifique a chave de conta de Armazenamento do Azure no segredo da credencial do banco de dados. Você pode especificar qualquer cadeia de caracteres na identidade da credencial no escopo do banco de dados, pois ela não será usada durante a autenticação no Armazenamento do Azure.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

## <a name="examples-bulk-operations"></a>Exemplos: Operações em Massa

> [!NOTE]
> Não coloque parâmetros de assinatura de acesso compartilhado, nome de arquivo ou **/** à direita no fim da URL `LOCATION` ao configurar uma fonte de dados externa para operações em massa.

### <a name="f-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>F. Criar uma fonte de dados externa para operações em massa recuperando dados do Armazenamento de Blobs do Azure

**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Use a seguinte fonte de dados para operações em massa com [BULK INSERT][bulk_insert] ou [OPENROWSET][openrowset]. A credencial deve ser definida como `SHARED ACCESS SIGNATURE` como a identidade, não deve ter o `?` à esquerda no token SAS, deve ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`), e o período de término deve ser válido (todas as datas estão no horário UTC). Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token].

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
     IDENTITY = 'SHARED ACCESS SIGNATURE'
--   REMOVE ? FROM THE BEGINNING OF THE SAS TOKEN
,    SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************'
;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
(    LOCATION   = 'https://newinvoices.blob.core.windows.net/week3'
,    CREDENTIAL = AccessAzureInvoices
,    TYPE       = BLOB_STORAGE
)
;
```

Para ver esse exemplo em uso, confira [BULK INSERT][bulk_insert_example].

## <a name="see-also"></a>Consulte Também

- [ALTER EXTERNAL DATA SOURCE (Transact-SQL)][alter_eds]
- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-transact-sql
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown

<!-- Azure Docs -->
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

|                                                              |                                 |                                                              |                                                              |      |
| ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | **_\* Banco de Dados SQL \*_** &nbsp; | [SQL Data<br />Warehouse](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                                                              |                                 |                                                              |                                                              |      |

&nbsp;

## <a name="overview-azure-sql-database"></a>Visão geral: Banco de dados SQL do Azure

Cria uma fonte de dados externa para consultas elásticas. Fontes de dados externas são usadas para estabelecer a conectividade e dar suporte a estes casos de uso principal:

- Operações de carregamento em massa usando `BULK INSERT` ou `OPENROWSET`
- Consultar instâncias remotas do Banco de Dados SQL ou do SQL Data Warehouse usando o Banco de Dados SQL com [consulta elástica][remote_eq]
- Consultar um Banco de Dados SQL do Azure fragmentado usando [consulta elástica][sharded_eq]

## <a name="syntax"></a>Sintaxe

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>  
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      = BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER ]
[,   DATABASE_NAME             = '<database_name>' ]
[,   SHARD_MAP_NAME            = '<shard_map_manager>' ]
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo no banco de dados no BD SQL (Banco de Dados SQL).

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Fornece o protocolo de conectividade e o caminho para a fonte de dados externa.

| Fonte de dados externa   | Prefixo de local | Caminho de local                                         |
| ---------------------- | --------------- | ----------------------------------------------------- |
| Operações em Massa        | `https`         | `<storage_account>.blob.core.windows.net/<container>` |
| Consulta Elástica (fragmento)  | Não obrigatório    | `<shard_map_server_name>.database.windows.net`        |
| Consulta Elástica (remota) | Não obrigatório    | `<remote_server_name>.database.windows.net`           |

Caminho de local:

- `<shard_map_server_name>` = o nome do servidor lógico do Azure que está hospedando o gerenciador de mapa de fragmentos. O argumento `DATABASE_NAME` fornece o banco de dados usado para hospedar o mapa de fragmentos e `SHARD_MAP_NAME` é usado para o mapa de fragmentos em si.
- `<remote_server_name>` = o nome do servidor lógico de destino para a consulta elástica. O nome do banco de dados é especificado usando o argumento `DATABASE_NAME`.

Observações e orientação adicionais ao definir o local:

- O mecanismo de Banco de Dados SQL não verifica a existência da fonte de dados externa quando o objeto é criado. Para validar, crie uma tabela externa usando a fonte de dados externa.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica uma credencial no escopo do banco de dados para a autenticação na fonte de dados externa.

Observações e orientações adicionais ao criar uma credencial:

- Para fazer o carregamento de dados do Armazenamento de Blobs do Azure no Banco de Dados SQL, use a Chave de Armazenamento do Azure.
- `CREDENTIAL` será necessário apenas se o blob tiver sido protegido. `CREDENTIAL` não é necessário para conjuntos de dados que permitem acesso anônimo.
- Quando o `TYPE` = `BLOB_STORAGE`, credencial usada precisa ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Além disso, o token SAS deve ser configurado da seguinte maneira:
  - Excluir o `?` à esquerda quando configurado como o segredo
  - Ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`)
  - Use um período de término válido (todas as datas estão no horário UTC).

Para ver um exemplo de como usar um `CREDENTIAL` com `SHARED ACCESS SIGNATURE` e `TYPE` = `BLOB_STORAGE`, veja [Criar uma fonte de dados externa para executar operações em massa e recuperar dados do Armazenamento de Blobs do Azure no Banco de Dados SQL](#c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage)

Para criar uma credencial no escopo do banco de dados, veja [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type---blob_storage--rdbms--shard_map_manager"></a>TYPE = *[ BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER]*

Especifica o tipo de fonte de dados externa que está sendo configurada. Esse parâmetro não é sempre necessário.

- Use o RDBMS para consultas entre bancos de dados usando a consulta elástica do Banco de Dados SQL.  
- Use SHARD_MAP_MANAGER ao criar uma fonte de dados externos ao se conectar a um Banco de Dados SQL fragmentado.
- Use BLOB_STORAGE ao executar operações em massa com [BULK INSERT][bulk_insert] ou [OPENROWSET][openrowset].

> [!IMPORTANT]
> Não defina `TYPE` se estiver usando qualquer outra fonte de dados externa.

### <a name="database_name--database_name"></a>DATABASE_NAME = *database_name*

Configure esse argumento quando o `TYPE` estiver definido como `RDBMS` ou `SHARD_MAP_MANAGER`.

| TYPE              | Valor de DATABASE_NAME                                       |
| ----------------- | ------------------------------------------------------------ |
| RDBMS             | O nome do banco de dados remoto no servidor fornecido usando `LOCATION` |
| SHARD_MAP_MANAGER | Nome do banco de dados operacional, como o gerenciador de mapa de fragmentos      |

Para obter um exemplo que mostra como criar uma fonte de dados externa em que `TYPE` = `RDBMS`, veja [Criar uma fonte de dados externa do RDBMS](#b-create-an-rdbms-external-data-source)

### <a name="shard_map_name--shard_map_name"></a>SHARD_MAP_NAME = *shard_map_name*

Usado quando o argumento `TYPE` é definido como `SHARD_MAP_MANAGER` apenas para definir o nome do mapa de fragmentos.

Para ver um exemplo que mostra como criar uma fonte de dados externa em que `TYPE` = `SHARD_MAP_MANAGER`, veja [Criar uma fonte de dados externa do gerenciador de mapa de fragmentos](#a-create-a-shard-map-manager-external-data-source)

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL no Banco de Dados SQL.

## <a name="locking"></a>Bloqueio

Coloca um bloqueio compartilhado no objeto EXTERNAL DATA SOURCE.  

## <a name="examples"></a>Exemplos:

### <a name="a-create-a-shard-map-manager-external-data-source"></a>A. Criar uma fonte de dados externa do gerenciador de mapa de fragmentos

Para criar uma fonte de dados externa para referenciar um SHARD_MAP_MANAGER, especifique o nome do servidor do Banco de Dados SQL que hospeda o gerenciador de mapa de fragmentos no Banco de Dados SQL ou em banco de dados do SQL Server em uma máquina virtual.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
WITH
     IDENTITY   = '<username>'
,    SECRET     = '<password>'
;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
(    TYPE             = SHARD_MAP_MANAGER
,    LOCATION         = '<server_name>.database.windows.net'
,    DATABASE_NAME    = 'ElasticScaleStarterKit_ShardMapManagerDb'
,    CREDENTIAL       = ElasticDBQueryCred
,    SHARD_MAP_NAME   = 'CustomerIDShardMap'
)
;
```

Para obter um tutorial passo a passo, confira [Introdução a consultas elásticas para fragmentação (particionamento horizontal)][sharded_eq_tutorial].

### <a name="b-create-an-rdbms-external-data-source"></a>B. Criar uma fonte de dados externa do RDBMS

Para criar uma fonte de dados externa para referenciar um RDBMS, especifica o nome do servidor do Banco de Dados SQL do banco de dados remoto no Banco de Dados SQL.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH
     IDENTITY  = '<username>'
,    SECRET    = '<password>'
;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
(    TYPE          = RDBMS
,    LOCATION      = '<server_name>.database.windows.net'
,    DATABASE_NAME = 'Customers'
,    CREDENTIAL    = SQL_Credential
)
;
```

Para obter um tutorial passo a passo sobre o RDBMS, confira [Introdução às consultas entre bancos de dados (particionamento vertical)][remote_eq_tutorial].

## <a name="examples-bulk-operations"></a>Exemplos: Operações em Massa

> [!NOTE]
> Não coloque parâmetros de assinatura de acesso compartilhado, nome de arquivo ou **/** à direita no fim da URL `LOCATION` ao configurar uma fonte de dados externa para operações em massa.

### <a name="c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>C. Criar uma fonte de dados externa para operações em massa recuperando dados do Armazenamento de Blobs do Azure

Use a seguinte fonte de dados para operações em massa com [BULK INSERT][bulk_insert] ou [OPENROWSET][openrowset]. A credencial deve ser definida como `SHARED ACCESS SIGNATURE` como a identidade, não deve ter o `?` à esquerda no token SAS, deve ter pelo menos permissão de leitura no arquivo que deve ser carregado (por exemplo `srt=o&sp=r`), e o período de término deve ser válido (todas as datas estão no horário UTC). Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token].

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
     IDENTITY = 'SHARED ACCESS SIGNATURE'
--   REMOVE ? FROM THE BEGINNING OF THE SAS TOKEN
,    SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************'
;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
(    LOCATION   = 'https://newinvoices.blob.core.windows.net/week3'
,    CREDENTIAL = AccessAzureInvoices
,    TYPE       = BLOB_STORAGE
)
;
```

Para ver esse exemplo em uso, confira [BULK INSERT][bulk_insert_example].

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token]
- [Introdução à consulta elástica][intro_eq]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql
[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql
[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

|                                                              |                                                              |                                            |                                                              |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ | ------------------------------------------------------------ | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | [Banco de Dados SQL](create-external-data-source-transact-sql.md?view=azuresqldb-current) | **_\* SQL Data<br />Warehouse \*_** &nbsp; | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                                                              |                                                              |                                            |                                                              |      |

&nbsp;

## <a name="overview-azure-sql-data-warehouse"></a>Visão geral: Azure SQL Data Warehouse

Cria uma fonte de dados externa para o PolyBase. Fontes de dados externas são usadas para estabelecer a conectividade e a compatibilidade com estes casos de uso principal: Virtualização de dados e carregamento dados usando o [PolyBase][intro_pb]

> [!IMPORTANT]  
> Para criar uma fonte de dados externa para consultar instâncias do SQL Data Warehouse usando o Banco de Dados SQL com [consulta elástica][remote_eq], confira [Banco de Dados SQL](create-external-data-source-transact-sql.md?view=azuresqldb-current).

## <a name="syntax"></a>Sintaxe

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>  
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      =  HADOOP
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo no banco de dados no SQL DW (SQL Data Warehouse).

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Fornece o protocolo de conectividade e o caminho para a fonte de dados externa.

| Fonte de dados externa        | Prefixo de local | Caminho de local                                         |
| --------------------------- | --------------- | ----------------------------------------------------- |
| Armazenamento de blobs do Azure          | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |
| Azure Data Lake Storage Gen 1 | `adl`           | `<storage_account>.azuredatalake.net`                 |
| Azure Data Lake Storage Gen 2 | `abfs[s]`       | `<container>@<storage_account>.dfs.core.windows.net`  |

Caminho de local:

- `<container>` = o contêiner da conta de armazenamento que contém os dados. Os contêineres raiz são somente leitura, não é possível gravar dados no contêiner.
- `<storage_account>` = o nome da conta de armazenamento do recurso do Azure.

Observações e orientação adicionais ao definir o local:

- A opção padrão é habilitar conexões SSL seguras ao provisionar o Azure Data Lake Storage Gen 2. Quando isso estiver habilitado, você deverá usar `abfss` quando uma conexão SSL segura for selecionada. Observe que `abfss`funciona para conexões SSL não seguras também. 
- O mecanismo do SQL Data Warehouse não verifica a existência da fonte de dados externa quando o objeto é criado. Para validar, crie uma tabela externa usando a fonte de dados externa.
- Use a mesma fonte de dados externa para todas as tabelas ao consultar o Hadoop para garantir semântica de consulta consistente.
- `wasb` é o protocolo padrão para o armazenamento de blobs do Azure. `wasbs` é opcional, mas recomendado, pois os dados serão enviados usando uma conexão SSL segura.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica uma credencial no escopo do banco de dados para a autenticação na fonte de dados externa.

Observações e orientações adicionais ao criar uma credencial:

- Para carregar dados do Armazenamento de Blobs do Azure ou do ADLS (Azure Data Lake Storage) Gen 2 no SQL DW, use uma Chave de Armazenamento do Azure.
- `CREDENTIAL` será necessário apenas se o blob tiver sido protegido. `CREDENTIAL` não é necessário para conjuntos de dados que permitem acesso anônimo.

Para criar uma credencial no escopo do banco de dados, veja [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type--hadoop"></a>TYPE = *HADOOP*

Especifica o tipo de fonte de dados externa que está sendo configurada. Esse parâmetro não é sempre necessário.

- Use HADOOP quando a fonte de dados externa for Armazenamento de Blobs do Azure, ADLS Gen 1 ou ADLS Gen 2.

> [!IMPORTANT]
> Não defina `TYPE` se estiver usando qualquer outra fonte de dados externa.

Para ver um exemplo de como usar `TYPE` = `HADOOP` para carregar dados do Armazenamento de Blobs do Azure, veja [Criar fonte de dados externa para referenciar o Armazenamento de Blobs do Azure](#a-create-external-data-source-to-reference-azure-blob-storage).

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL no banco de dados no SQL Data Warehouse.

## <a name="locking"></a>Bloqueio

Coloca um bloqueio compartilhado no objeto EXTERNAL DATA SOURCE.  

## <a name="security"></a>Segurança

O PolyBase dá suporte para autenticação baseada em proxy para a maioria das fontes de dados externas. Crie uma credencial no escopo do banco de dados para criar a conta proxy.

Quando você se conecta ao pool de armazenamento ou de dados em um cluster de Big Data do SQL Server, as credenciais do usuário são passadas para o sistema de back-end. Crie logons no pool de dados propriamente dito para habilitar a autenticação de passagem.

No momento, não há suporte para um token SAS com o tipo `HADOOP`. Ele só é compatível com uma chave de acesso da conta de armazenamento. Tentar criar uma fonte de dados externa com o tipo `HADOOP` e uma credencial SAS falha com o seguinte erro:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>Exemplos:

### <a name="a-create-external-data-source-to-reference-azure-blob-storage"></a>A. Criar uma fonte de dados externa para referenciar o Armazenamento de Blobs do Azure

Neste exemplo, a fonte de dados externa é um contêiner do Armazenamento de Blobs do Azure chamado `daily` na conta de Armazenamento do Azure chamada `logs`. A fonte de dados externa do armazenamento do Azure destina-se somente a transferência de dados. Não dá suporte a aplicação de predicado.

Este exemplo mostra como criar a credencial no escopo do banco de dados para autenticação no Armazenamento do Azure. Especifique a chave de conta de Armazenamento do Azure no segredo da credencial do banco de dados. Você pode especificar qualquer cadeia de caracteres na identidade da credencial no escopo do banco de dados, pois ela não será usada durante a autenticação no Armazenamento do Azure.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

### <a name="b-create-external-data-source-to-reference-azure-data-lake-store-gen-1-or-2-using-a-service-principal"></a>B. Criar fonte de dados externa para referenciar o Azure Data Lake Storage Gen 1 ou 2 usando uma entidade de serviço

A conectividade do Azure Data Lake Storage pode estar baseada no URI do ADLS e na entidade de serviço do aplicativo do Azure Active Directory. A documentação para criar esse aplicativo pode ser encontrada em [Autenticação do Data Lake Storage usando o Active Directory][azure_ad[].

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
--   IDENTITY   = '<clientID>@<OAuth2.0TokenEndPoint>'
     IDENTITY   = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token'
--,  SECRET     = '<KEY>'
,    SECRET     = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;

-- For Gen 1 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 1 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
(    LOCATION       = 'adl://newyorktaxidataset.azuredatalakestore.net'
,    CREDENTIAL     = ADLS_credential
,    TYPE           = HADOOP
)
;

-- For Gen 2 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 2 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
(    LOCATION       = 'abfss://newyorktaxidataset.azuredatalakestore.net' -- Please note the abfss endpoint when your account has secure transfer enabled
,    CREDENTIAL     = ADLS_credential
,    TYPE           = HADOOP
)
;
```

### <a name="c-create-external-data-source-to-reference-azure-data-lake-store-gen-2-using-the-storage-account-key"></a>C. Criar fonte de dados externa para referenciar o Azure Data Lake Storage Gen 2 usando a chave de conta de armazenamento

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
--   IDENTITY   = '<storage_account_name>'
     IDENTITY   = 'newyorktaxidata'
--,  SECRET     = '<storage_account_key>'
,    SECRET     = 'yz5N4+bxSb89McdiysJAzo+9hgEHcJRJuXbF/uC3mhbezES/oe00vXnZEl14U0lN3vxrFKsphKov16C0w6aiTQ=='
;

-- Note this example uses a Gen 2 secured endpoint (abfss)
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION   = 'abfss://2013@newyorktaxidataset.dfs.core.windows.net'
,    CREDENTIAL = ADLS_credential
,    TYPE       = HADOOP
)
[;]
```

### <a name="d-create-external-data-source-to-reference-polybase-connectivity-to-azure-data-lake-store-gen-2"></a>D. Criar uma fonte de dados externa para referenciar a conectividade do Polybase com o Azure Data Lake Storage Gen 2

Não há necessidade de especificar SECRET ao se conectar à conta do Azure Data Lake Storage Gen2 com o mecanismo de [Identidade Gerenciada](/azure/active-directory/managed-identities-azure-resources/overview
).

```sql
-- If you do not have a Master Key on your DW you will need to create one
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'

--Create database scoped credential with **IDENTITY = 'Managed Service Identity'**

CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Service Identity';

--Create external data source with abfss:// scheme for connecting to your Azure Data Lake Store Gen2 account

CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss WITH (TYPE = hadoop, LOCATION = 'abfss://myfile@mystorageaccount.dfs.core.windows.net', CREDENTIAL = msi_cred);
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [CREATE EXTERNAL TABLE AS SELECT (SQL Data Warehouse do Azure)][create_etb_as_sel]
- [CREATE TABLE AS SELECT (SQL Data Warehouse do Azure)][create_tbl_as_sel]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

|                                                              |                                                              |                                                              |                                                         |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------- | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | [Banco de Dados SQL](create-external-data-source-transact-sql.md?view=azuresqldb-current) | [SQL Data<br />Warehouse](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | **_\* Analytics<br />Platform System (PDW) \*_** &nbsp; |      |
|                                                              |                                                              |                                                              |                                                         |      |

&nbsp;

## <a name="overview-analytics-platform-system"></a>Visão geral: Sistema de plataforma de análise

Cria uma fonte de dados externa para consultas do PolyBase. Fontes de dados externas são usadas para estabelecer a conectividade e a compatibilidade com estes casos de uso: Virtualização de dados e carregamento dados usando o [PolyBase][intro_pb]

## <a name="syntax"></a>Sintaxe

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>  
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      = HADOOP ]
[,   RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]'
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica o nome da fonte de dados definido pelo usuário. O nome precisa ser exclusivo no servidor no Analytics Platform System (Parallel Data Warehouse ou PDW).

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Fornece o protocolo de conectividade e o caminho para a fonte de dados externa.

| Fonte de dados externa    | Prefixo de local | Caminho de local                                         |
| ----------------------- | --------------- | ----------------------------------------------------- |
| Cloudera ou Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   |
| Armazenamento de blobs do Azure      | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |

Caminho de local:

- `<`Namenode`>` = o nome do computador, o URI do serviço de nome ou o endereço IP do `Namenode` no cluster do Hadoop. O PolyBase deve resolver qualquer nome DNS usado pelo cluster do Hadoop. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = a porta em que fonte de dados externa está escutando. No Hadoop, a porta pode ser encontrada usando o parâmetro de configuração `fs.defaultFS`. O padrão é 8020.
- `<container>` = o contêiner da conta de armazenamento que contém os dados. Os contêineres raiz são somente leitura, não é possível gravar dados no contêiner.
- `<storage_account>` = o nome da conta de armazenamento do recurso do Azure.

Observações e orientação adicionais ao definir o local:

- O mecanismo do PDW não verifica a existência da fonte de dados externa quando o objeto é criado. Para validar, crie uma tabela externa usando a fonte de dados externa.
- Use a mesma fonte de dados externa para todas as tabelas ao consultar o Hadoop para garantir semântica de consulta consistente.
- `wasb` é o protocolo padrão para o armazenamento de blobs do Azure. `wasbs` é opcional, mas recomendado, pois os dados serão enviados usando uma conexão SSL segura.
- Para garantir consultas do PolyBase com êxito durante um failover `Namenode` do Hadoop, considere usar um endereço IP virtual para o `Namenode` do cluster do Hadoop. Se você não fizer isso, execute um comando [ALTER EXTERNAL DATA SOURCE][alter_eds] para apontar para o novo local.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica uma credencial no escopo do banco de dados para a autenticação na fonte de dados externa.

Observações e orientações adicionais ao criar uma credencial:

- Para carregar dados do armazenamento de Blobs do Azure ou do ADLS (Azure Data Lake Storage) Gen 2 no SQL DW ou no PDW, use uma Chave de Armazenamento do Azure.
- `CREDENTIAL` será necessário apenas se o blob tiver sido protegido. `CREDENTIAL` não é necessário para conjuntos de dados que permitem acesso anônimo.

### <a name="type---hadoop-"></a>TYPE = *[ HADOOP ]*

Especifica o tipo de fonte de dados externa que está sendo configurada. Esse parâmetro não é sempre necessário.

- Use HADOOP quando a fonte de dados externa for Cloudera, Hortonworks ou Armazenamento de Blobs do Azure.

> [!IMPORTANT]
> Não defina `TYPE` se estiver usando qualquer outra fonte de dados externa.

Para ver um exemplo de como usar `TYPE` = `HADOOP` para carregar dados do Armazenamento de Blobs do Azure, veja [Criar fonte de dados externa para referenciar o Armazenamento de Blobs do Azure](#d-create-external-data-source-to-reference-azure-blob-storage).

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Configure esse valor opcional ao se conectar ao Hortonworks ou ao Cloudera.

Quando o `RESOURCE_MANAGER_LOCATION` for definido, o otimizador de consulta tomará uma decisão baseada em custo para melhorar o desempenho. Um trabalho MapReduce pode ser usado para aplicar a computação para o Hadoop. Especificar o `RESOURCE_MANAGER_LOCATION` pode reduzir significativamente o volume de dados transferidos entre o Hadoop e o SQL, o que pode levar a um desempenho de consultas aprimorado.  

Se o Resource Manager não tiver sido especificado, o envio de computação por push para o Hadoop estará desabilitado para consultas do PolyBase.

Se a porta não for especificada, o valor padrão será escolhido usando a definição atual da configuração 'conectividade do Hadoop'.

| Conectividade do Hadoop | Porta do Gerenciador de Recursos padrão |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

Para ver uma lista completa de versões do Hadoop compatíveis, veja [Configuração de conectividade do PolyBase (Transact-SQL)][connectivity_pb].

> [!IMPORTANT]  
> O valor de RESOURCE_MANAGER_LOCATION e não é validado quando você cria a fonte de dados externa. Inserir um valor incorreto pode causar falha de consulta em tempo de execução sempre que for feita uma tentativa de aplicação, uma vez que o valor fornecido não poderá ser resolvido.

[Criar fonte de dados externa para referenciar o Hadoop com aplicação habilitada](#b-create-external-data-source-to-reference-hadoop-with-push-down-enabled) apresenta um exemplo concreto e diretrizes adicionais.

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL no banco de dados no Analytics Platform System (Parallel Data Warehouse ou PDW).

> [!NOTE]
> Nas versões anteriores do PDW, a criação de fonte de dados externa exigia as permissões ALTER ANY EXTERNAL DATA SOURCE.

## <a name="locking"></a>Bloqueio

Coloca um bloqueio compartilhado no objeto EXTERNAL DATA SOURCE.  

## <a name="security"></a>Segurança

O PolyBase dá suporte para autenticação baseada em proxy para a maioria das fontes de dados externas. Crie uma credencial no escopo do banco de dados para criar a conta proxy.

No momento, não há suporte para um token SAS com o tipo `HADOOP`. Ele só é compatível com uma chave de acesso da conta de armazenamento. Tentar criar uma fonte de dados externa com o tipo `HADOOP` e uma credencial SAS falha com o seguinte erro:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>Exemplos:

### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Criar uma fonte de dados externa para referenciar o Hadoop

Para criar uma fonte de dados externa para referenciar o cluster do Hadoop do Hortonworks ou do Cloudera, especifique o nome do computador ou o endereço IP do `Namenode` do Hadoop e a porta. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION = 'hdfs://10.10.10.10:8050'
,    TYPE     = HADOOP
)
;
```

### <a name="b-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>B. Criar uma fonte de dados externa para referenciar o Hadoop com aplicação habilitada

Especifique a opção `RESOURCE_MANAGER_LOCATION` para habilitar a computação de aplicação para Hadoop em consultas do PolyBase. Uma vez habilitado, o PolyBase toma uma decisão baseada em custo para determinar se a computação de consulta deve ser enviada por push para o Hadoop.

```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8020'
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="c-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>C. Criar uma fonte de dados externa para referenciar o Hadoop protegido pelo Kerberos

Para verificar se o cluster do Hadoop está protegido pelo Kerberos, verifique o valor da propriedade hadoop.security.authentication no core-site.xml do Hadoop. Para referenciar um cluster do Hadoop protegido pelo Kerberos, você precisa especificar uma credencial no escopo do banco de dados contendo o nome de usuário e a senha do Kerberos. A chave mestra do banco de dados é usada para criptografar o segredo da credencial no escopo do banco de dados.

```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
     IDENTITY   = '<hadoop_user_name>'
,    SECRET     = '<hadoop_password>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8050'
,    CREDENTIAL                = HadoopUser1
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Criar uma fonte de dados externa para referenciar o Armazenamento de Blobs do Azure

Neste exemplo, a fonte de dados externa é um contêiner do Armazenamento de Blobs do Azure chamado `daily` na conta de Armazenamento do Azure chamada `logs`. A fonte de dados externa do armazenamento do Azure destina-se somente a transferência de dados. Não dá suporte a aplicação de predicado.

Este exemplo mostra como criar a credencial no escopo do banco de dados para autenticação no Armazenamento do Azure. Especifique a chave de conta de Armazenamento do Azure no segredo da credencial do banco de dados. Você pode especificar qualquer cadeia de caracteres na identidade da credencial no escopo do banco de dados, pois ela não será usada durante a autenticação no Armazenamento do Azure.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Usando SAS (Assinatura de Acesso Compartilhado)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
