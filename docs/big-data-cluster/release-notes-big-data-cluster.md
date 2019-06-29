---
title: Notas de versão
titleSuffix: SQL Server big data clusters
description: Este artigo descreve as últimas atualizações e problemas conhecidos para clusters de big data de 2019 do SQL Server (versão prévia).
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1f2d7f5a1d4a966edbce3c4ad96a7b31bd604b48
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469127"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Notas de versão para clusters de grandes dados no SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo lista as atualizações e saiba que esses problemas para as versões mais recentes dos clusters de grandes dados do SQL Server.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp31"></a> CTP 3.1 (junho)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 3.1.

### <a name="whats-new"></a>What's New

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| `mssqlctl` alterações de comando | `mssqlctl cluster` comandos foram renomeados para `mssqlctl bdc`. Para obter mais informações, consulte o [ `mssqlctl` referência](reference-mssqlctl.md). |
| Novo `mssqlctl` comandos de status e remoção do Portal de administração do Cluster. | O Portal de administração de Cluster é removido nesta versão. Foram adicionados novos comandos de status ao `mssqlctl` complemento existentes comandos de monitoramento. |
| Pools de computação do Spark | Crie nós adicionais para aumentar a potência de computação do Spark sem precisar dimensionar o armazenamento. Além disso, você pode iniciar nós de pool de armazenamento que não são usados para o Spark. Spark e o armazenamento são separados. Para obter mais informações, consulte [configurar o armazenamento sem spark](deployment-custom-configuration.md#sparkstorage). |
| Conector do Spark MSSQL | Suporte para leitura/gravação para tabelas externas do pool de dados. Somente tabelas da instância anterior leitura/gravação de versões com suporte para o mestre. Para obter mais informações, consulte [como ler e gravar para o SQL Server no Spark usando o conector do Spark MSSQL](spark-mssql-connector.md). |
| Aprendizado de máquina usando MLeap | [Treinar um modelo de aprendizado de máquina MLeap no Spark e pontuá-lo no SQL Server usando a extensão da linguagem Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior.

   > [!IMPORTANT]
   > Você deve fazer backup dos dados e, em seguida, exclua seu cluster de big data existente (usando a versão anterior do **mssqlctl**) antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- Implantação de cluster de big data não cria mais o **SqlDataPool** e **SqlStoragePool** fontes de dados externas. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   > [!NOTE]
   > O URI para a criação destas fontes de dados externas é diferente entre CTPs. Consulte os comandos Transact-SQL abaixo para ver como criá-los 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que usam tipos de dados de caractere, o Assistente de virtualização do Azure Data Studio interpreta essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema do Oracle para usar o tipo de NVARCHAR2, ou criar instruções de tabela externa manualmente e especificar NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação de aplicativo

- Ao chamar um aplicativo de R, Python ou MLeap da API RESTful, a chamada expirará em 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp30"></a> CTP 3.0 (maio)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 3.0.

### <a name="whats-new"></a>What's New

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Atualizações de **mssqlctl** | Várias [atualizações de comando e parâmetro](../big-data-cluster/reference-mssqlctl.md) do **mssqlctl**. Isso inclui uma atualização do comando **mssqlctl login**, que agora direciona o nome de usuário do controlador e o ponto de extremidade. |
| Melhorias no armazenamento | Suporte para diferentes configurações de armazenamento para logs e dados. Além disso, o número de declarações de volume persistente para um cluster de Big Data foi reduzido. |
| Várias instâncias do pool de computação | Suporte para várias instâncias do pool de computação. |
| Novas funcionalidades e novo comportamento do pool | O pool de computação agora é usado por padrão em operações do pool de dados e do pool de armazenamento apenas em uma distribuição **ROUND_ROBIN**. O pool de dados agora pode usar um novo tipo de distribuição **REPLICATED**, o que significa que os mesmos dados estão presentes em todas as instâncias do pool de dados. |
| Melhorias na tabela externa | As tabelas externas do tipo de fonte de dados HADOOP agora dão suporte à leitura de linhas com até 1 MB. As tabelas externas (ODBC, pool de armazenamento, pool de dados) agora dão suporte a linhas da mesma largura de uma tabela do SQL Server. |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="hdfs"></a>HDFS

- O estúdio de dados do Azure retornará um erro ao tentar criar uma nova pasta no HDFS. Para habilitar essa funcionalidade, instale o build insiders do Studio de dados do Azure:
  
   - [Instalador de usuário do Windows - **build Insiders**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Instalador de sistema do Windows - **build Insiders**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP - **build Insiders**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP - **build Insiders**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR. GZ - **build Insiders**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="deployment"></a>Implantação

- Não há suporte para os procedimentos de implantação anterior para clusters grandes de dados habilitadas para GPU no CTP 3.0. Um procedimento de alternativas de implantação está sendo investigado. Por enquanto, o artigo "Implantar um big data com suporte GPU do cluster e executar o TensorFlow" tenha sido temporariamente não publicado para evitar confusão.

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior.

   > [!IMPORTANT]
   > Você deve fazer backup dos dados e, em seguida, exclua seu cluster de big data existente (usando a versão anterior do **mssqlctl**) antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- Implantação de cluster de big data não cria mais o **SqlDataPool** e **SqlStoragePool** fontes de dados externas. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   > [!NOTE]
   > O URI para a criação destas fontes de dados externas é diferente entre CTPs. Consulte os comandos Transact-SQL abaixo para ver como criá-los 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que usam tipos de dados de caractere, o Assistente de virtualização do Azure Data Studio interpreta essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema do Oracle para usar o tipo de NVARCHAR2, ou criar instruções de tabela externa manualmente e especificar NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação de aplicativo

- Ao chamar um aplicativo de R, Python ou MLeap da API RESTful, a chamada expirará em 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp25"></a> CTP 2.5 (abril)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.5.

### <a name="whats-new"></a>What's New

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Perfis de implantação | Use os [arquivos JSON de configuração de implantação](deployment-guidance.md#configfile) para padrão e personalizados para implantações de cluster de Big Data, em vez de variáveis de ambiente. |
| Implantações solicitadas | O `mssqlctl cluster create` agora solicitará qualquer configuração necessária para implantações padrão. |
| Alterações de nome de ponto de extremidade de serviço e de pod | Os seguintes pontos de extremidade externos foram alteradas nomes:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| Melhorias a **mssqlctl** | Use **mssqlctl** para [listar pontos de extremidade externos](deployment-guidance.md#endpoints) e verifique a versão do **mssqlctl** com o parâmetro `--version`. |
| Instalação offline | Diretrizes para implantações de cluster de grandes dados off-line. |
| Melhorias em camadas do HDFS | Suportam a disposição em camadas S3, cache de montagem e OAuth para Gen2 ADLS. |
| Novo `mssql` conector do Spark SQL Server | |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior.

   > [!IMPORTANT]
   > Você deve fazer backup dos dados e, em seguida, exclua seu cluster de big data existente (usando a versão anterior do **mssqlctl**) antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- Implantação de cluster de big data não cria mais o **SqlDataPool** e **SqlStoragePool** fontes de dados externas. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que usam tipos de dados de caractere, o Assistente de virtualização do Azure Data Studio interpreta essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema do Oracle para usar o tipo de NVARCHAR2, ou criar instruções de tabela externa manualmente e especificar NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação de aplicativo

- Ao chamar um aplicativo de R, Python ou MLeap da API RESTful, a chamada expirará em 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp24"></a> CTP 2.4 (março)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.4.

### <a name="whats-new"></a>What's New

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Diretrizes de suporte de GPU para execução de aprendizado profundo com o TensorFlow no Spark. | [Implantar um cluster de Big Data com suporte GPU e executar o TensorFlow](spark-gpu-tensorflow.md). |
| As fontes de dados **SqlDataPool** e **SqlStoragePool** não são mais criadas por padrão. | Crie-os manualmente, se necessário. Veja os [problemas conhecidos](#externaltablesctp24). |
| Suporte a `INSERT INTO SELECT` para o pool de dados. | Para um exemplo, veja [Tutorial: Ingerir dados em um pool de dados do SQL Server com Transact-SQL](tutorial-data-pool-ingest-sql.md). |
| Opções `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Força ou desabilita o uso da computação do pool para consultas em tabelas externas. Por exemplo, `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Recomendações atualizadas de implantação do AKS. | Ao avaliar a clusters de Big Data no AKS, agora recomendamos usar um único nó de tamanho **Standard_L8s**. |
| Atualização de tempo de execução do Spark para o Spark 2.4. | |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior.

   > [!IMPORTANT]
   > Você deve fazer backup dos dados e, em seguida, exclua seu cluster de big data existente (usando a versão anterior do **mssqlctl**) antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="kubeadm-deployments"></a>implantações de kubeadm

Se você usar kubeadm implantar Kubernetes em vários computadores, o portal de administração de cluster não exibe corretamente os pontos de extremidade necessários para se conectar ao cluster de big data. Se você estiver enfrentando esse problema, use a seguinte solução alternativa para descobrir os endereços IP do ponto de extremidade de serviço:

- Se você estiver se conectando de dentro do cluster, consulte Kubernetes para o IP do serviço para o ponto de extremidade que você deseja se conectar. Por exemplo, a seguinte **kubectl** comando exibe o endereço IP de instância mestre do SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se você estiver se conectando de fora do cluster, use as seguintes etapas para conectar-se:

   1. Obtenha o endereço IP do nó que executa a instância mestre do SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conecte-se à instância mestre do SQL Server usando este endereço IP.

   1. Consulta de **cluster_endpoint_table** no banco de dados mestre para outros pontos de extremidade externos.

      Se isso falhar com um tempo limite de conexão, é possível que o respectivo nó passa pelo firewall. Nesse caso, você deve entre em contato com seu administrador de cluster do Kubernetes e peça para o IP do nó que é exposto externamente. Isso pode ser qualquer nó. Em seguida, você pode usar esse IP e a porta correspondente para se conectar a vários serviços em execução no cluster. Por exemplo, o administrador pode encontrar esse IP executando:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Excluir cluster falha

Quando você tenta excluir um cluster com **mssqlctl**, ele falhará com o seguinte erro:

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

Um novo cliente de Python Kubernetes (versão 9.0.0) alterado os namespaces de exclusão API, que atualmente interrompe **mssqlctl**. Isso ocorre apenas se você tiver um cliente de python Kubernetes mais recente instalado. Você pode contornar esse problema excluindo diretamente o cluster usando **kubectl** (`kubectl delete ns <ClusterName>`), ou você pode instalar a versão mais antiga usando `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a> Tabelas externas

- Implantação de cluster de big data não cria mais o **SqlDataPool** e **SqlStoragePool** fontes de dados externas. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que usam tipos de dados de caractere, o Assistente de virtualização do Azure Data Studio interpreta essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema do Oracle para usar o tipo de NVARCHAR2, ou criar instruções de tabela externa manualmente e especificar NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação de aplicativo

- Ao chamar um aplicativo de R, Python ou MLeap da API RESTful, a chamada expirará em 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp23"></a> CTP 2.3 (fevereiro)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.3.

### <a name="whats-new"></a>What's New

| Novo recurso ou atualização | Detalhes |
| :---------- | :------ |
| Enviar trabalhos do Spark em clusters de Big Data no IntelliJ. | [Enviar trabalhos do Spark em clusters de Big Data do SQL Server no IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| CLI comum para gerenciamento de cluster e de implantação do aplicativo. | [Como implantar um aplicativo no cluster de Big Data do SQL Server 2019 (versão prévia)](big-data-cluster-create-apps.md) |
| Extensão do VS Code para implantar aplicativos em um cluster de Big Data. | [Como usar o VS Code para implantar aplicativos em clusters de Big Data do SQL Server](app-deployment-extension.md) |
| Muda para o uso de comando de ferramenta **mssqlctl**. | Para obter mais detalhes, veja o [problemas conhecidos de mssqlctl](#mssqlctlctp23). |
| Usar Sparklyr no cluster de big data | [Usar o Sparklyr em clusters de Big Data do SQL Server 2019](sparklyr-from-RStudio.md) |
| Montar armazenamento compatível com HDFS externo no cluster de Big Data com a disposição em **camadas do HDFS**. | Veja [Camadas do HDFS](hdfs-tiering.md). |
| Nova experiência de conexão unificada para a instância principal do SQL Server e o Gateway do HDFS/Spark. | Veja [Instância principal do SQL Server e o Gateway do HDFS/Spark](connect-to-big-data-cluster.md). |
| Excluir um cluster com **mssqlctl cluster delete** agora exclui somente os objetos no namespace que faziam parte do cluster de big data. | O namespace não é excluído. No entanto, em versões anteriores, esse comando excluía todo o namespace. |
| Nomes de ponto de extremidade de _segurança_ foram alterados e consolidados. | **service-security-lb** e **service-security-nodeport** foram consolidados no ponto de extremidade **endpoint-security**. |
| Nomes de ponto de extremidade de _proxy_ foram alterados e consolidados. | **service-proxy-lb** e **service-proxy-nodeport** foram consolidados no ponto de extremidade **endpoint-service-proxy**. |
| Nomes de ponto de extremidade de _controlador_ foram alterados e consolidados. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** foram consolidados no ponto de extremidade **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior.

   > [!IMPORTANT]
   > Você deve fazer backup dos dados e, em seguida, exclua seu cluster de big data existente (usando a versão anterior do **mssqlctl**) antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- O **ACCEPT_EULA** variável de ambiente deve ser "Sim" ou "Sim" para aceitar o EULA. Versões anteriores permitidas "y" e "Y", mas eles não serão mais aceitos e causarão falha na implantação.

- O **CLUSTER_PLATFORM** variáveis de ambiente não tem um padrão como fazia nas versões anteriores.

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="kubeadm-deployments"></a>implantações de kubeadm

Se você usar kubeadm implantar Kubernetes em vários computadores, o portal de administração de cluster não exibe corretamente os pontos de extremidade necessários para se conectar ao cluster de big data. Se você estiver enfrentando esse problema, use a seguinte solução alternativa para descobrir os endereços IP do ponto de extremidade de serviço:

- Se você estiver se conectando de dentro do cluster, consulte Kubernetes para o IP do serviço para o ponto de extremidade que você deseja se conectar. Por exemplo, a seguinte **kubectl** comando exibe o endereço IP de instância mestre do SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se você estiver se conectando de fora do cluster, use as seguintes etapas para conectar-se:

   1. Obtenha o endereço IP do nó que executa a instância mestre do SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conecte-se à instância mestre do SQL Server usando este endereço IP.

   1. Consulta de **cluster_endpoint_table** no banco de dados mestre para outros pontos de extremidade externos.

      Se isso falhar com um tempo limite de conexão, é possível que o respectivo nó passa pelo firewall. Nesse caso, você deve entre em contato com seu administrador de cluster do Kubernetes e peça para o IP do nó que é exposto externamente. Isso pode ser qualquer nó. Em seguida, você pode usar esse IP e a porta correspondente para se conectar a vários serviços em execução no cluster. Por exemplo, o administrador pode encontrar esse IP executando:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- O **mssqlctl** ferramenta alterado de um comando de verbo-substantivo ordenação para uma ordem de verbo-substantivo. Por exemplo, `mssqlctl create cluster` agora é `mssqlctl cluster create`.

- O `--name` parâmetro agora é necessário ao criar um cluster com `mssqlctl cluster create`.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- Para obter informações importantes sobre a atualização para a versão mais recente dos clusters de big data e **mssqlctl**, consulte [atualizar para uma nova versão](deployment-upgrade.md).

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que usam tipos de dados de caractere, o Assistente de virtualização do Azure Data Studio interpreta essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema do Oracle para usar o tipo de NVARCHAR2, ou criar instruções de tabela externa manualmente e especificar NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação de aplicativo

- Ao chamar um aplicativo de R, Python ou MLeap da API RESTful, a chamada expirará em 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp22"></a> CTP 2.2 (dezembro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.2.

### <a name="new-features"></a>Novos recursos

- Portal de administração de cluster é acessado com `/portal` (**https://\<endereço ip\>: 30777/portal**).
- Nome do serviço mestre do pool é alterado de `service-master-pool-lb` e `service-master-pool-nodeport` para `endpoint-master-pool`.
- Nova versão do **mssqlctl** e atualizada de imagens.
- Diversas correções de bugs e melhorias.

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações desta versão.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior. Você deve fazer backup e excluir qualquer cluster de big data existente antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="cluster-administration-portal"></a>Portal de administração de cluster

O portal de administração de cluster não exibe o ponto de extremidade para a instância mestre do SQL Server. Para localizar o endereço IP e porta para a instância mestre, use o seguinte **kubectl** comando:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp21"></a> CTP 2.1 (novembro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.1.

### <a name="new-features"></a>Novos recursos

- [Implantar aplicativos de Python e R](big-data-cluster-create-apps.md) em um cluster de big data.
- Nova versão do **mssqlctl** e atualizada de imagens. 
- Diversas correções de bugs e melhorias.

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir fornecem os problemas conhecidos para clusters de grandes dados do SQL Server no CTP 2.1.

#### <a name="deployment"></a>Implantação

- Não há suporte para atualizar um cluster de dados de grandes dados de uma versão anterior. Você deve fazer backup e excluir qualquer cluster de big data existente antes de implantar a versão mais recente. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="admin-portal"></a>Portal de administração

- Quando você [criar um aplicativo usando o comando msqlctl ctp](big-data-cluster-create-apps.md) e implantá-lo em um cluster de big data, o Portal de administração de Cluster mostra os pods em que o aplicativo foi implantado como "Desconhecido" na seção de controlador da parte do administrador do SQL Server.

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a id="ctp20"></a> CTP 2.0 (outubro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.0.

### <a name="new-features"></a>Novos recursos

- Experiência de implantação simples usando a ferramenta de gerenciamento mssqlctl
- Experiência de notebook nativo no estúdio de dados do Azure
- Arquivos HDFS de consulta por meio do armazenamento de instância do SQL Server
- Virtualização de dados por meio do mestre do SQL Server, Oracle, MongoDB e HDFS
- Assistente de virtualização de dados do SQL Server e Oracle no estúdio de dados do Azure
- Serviços de ML no mestre
- Portal de administração de cluster que você pode usar para monitoramento e solução de problemas
- Envio de trabalho do Spark no estúdio de dados do Azure 
- Interface do usuário do Spark no portal de administração do cluster
- Volume de montagem para classes de armazenamento
- Consultas em pools de dados do mestre
- Mostrar plano para consultas distribuídas no SSMS
- Pacote de PIP para a ferramenta de gerenciamento mssqlctl
- Mecanismo de implantação interna por meio do serviço de controlador

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir fornecem os problemas conhecidos para clusters de grandes dados do SQL Server no CTP 2.0.

#### <a name="deployment"></a>Implantação

- Se você estiver usando o serviço de Kubernetes do Azure (AKS), a versão recomendada do Kubernetes é 1.10. *, que não oferece suporte a redimensionamento de disco. Você deve verificar se você está dimensionando o armazenamento de forma adequada no momento da implantação. Para obter mais informações sobre como ajustar os tamanhos de armazenamento, consulte o [persistência de dados](concept-data-persistence.md) artigo. Para o Kubernetes implantado em VMs, a versão recomendada é 1.11.

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
