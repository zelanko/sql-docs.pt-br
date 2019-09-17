---
title: Notas de versão
titleSuffix: SQL Server big data clusters
description: Este artigo descreve as atualizações mais recentes e problemas conhecidos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] do (Preview).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bcbc3537a6ba26dc907bf348c565939ff869ea43
ms.sourcegitcommit: da8bb7abd256b2bebee7852dc0164171eeff11be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988101"
---
# <a name="release-notes-for-sql-server-big-data-clusters"></a>Notas de versão para SQL Server clusters de Big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo lista as atualizações e os problemas conhecidos para as versões mais recentes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]do.

## <a id="rc"></a>Release Candidate (agosto)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de Big Data no SQL Server Release Candidate 2019.

### <a name="whats-new"></a>O Que Há de Novo

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|SQL Server Always On grupo de disponibilidade |Ao implantar um SQL Server Cluster de Big data, você pode configurar a implantação para criar um grupo de disponibilidade para fornecer:<br/><br/>-Alta disponibilidade <br/><br/>-Leitura-escalar horizontalmente <br/><br/>– Inserção de dados de expansão no pool de dados<br/><br>Consulte [implantar com alta disponibilidade](../big-data-cluster/deployment-high-availability.md). |
|`azdata` |Instalação simplificada para a ferramenta com o [Gerenciador de instalação](./deploy-install-azdata-linux-package.md)<br/><br/>[`azdata notebook`linha](./reference-azdata-notebook.md)<br/><br/>[`azdata bdc status`linha](./reference-azdata-bdc-status.md) |
|Azure Data Studio|[Baixe a versão Release Candidate do Azure Data Studio](deploy-big-data-tools.md#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc).<br/><br/>Adicionado os notebooks de solução de problemas por meio do SQL Server guia Jupyter 2019 book.<br/><br/>Experiência de logon do controlador adicionada.<br/><br/>Painel do controlador adicionado para exibir pontos de extremidade de serviço, exibir o status de integridade do cluster e acessar os notebooks de solução de problemas.<br/><br/>Desempenho de edição/saída de célula de notebook aprimorado.|
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

* SQL Server o número de Build de atualização candidato da versão de clusters de Big data do 2019 é `15.0.1900.47`.

* Não há suporte para o perfil de implantação "kubeadm-Prod" na versão Release Candidate de clusters de Big data do SQL Server 2019 com o número de Build acima. Em vez disso, use o perfil "kubeadm-dev-Test" para implantações de Kubeadm.

## <a id="ctp32"></a> CTP 3.2 (julho)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 3.2.

### <a name="whats-new"></a>O Que Há de Novo

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Versão prévia pública |Antes do CTP 3.2, o cluster de Big Data do SQL Server estava disponível para os usuários pioneiros registrados. Esta versão permite que qualquer pessoa experimente os recursos dos clusters de Big Data do SQL Server. <br/><br/> Consulte [introdução ao [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deploy-get-started.md).|
|`azdata` |O CTP 3.2 apresenta o `azdata` – um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big Data por meio de APIs REST. O `azdata` substitui o `mssqlctl`. Confira [Instalar o `azdata`](deploy-install-azdata.md). |
|PolyBase |Os nomes de coluna da tabela externa agora são usados para consultar fontes de dados de SQL Server, Oracle, Teradata, MongoDB e ODBC. Nas versões CTP anteriores, as colunas na fonte de dados externa eram vinculadas com base apenas na posição ordinal e os nomes especificados na definição EXTERNAL TABLE não eram usados. |
|Atualização de camadas do HDFS |Introdução da funcionalidade de atualização de camadas do HDFS para que uma montagem existente possa ser atualizada para o instantâneo mais recente dos dados remotos. Confira [Camadas do HDFS](hdfs-tiering.md) |
|Solução de problemas baseada em notebook |O CTP 3.2 introduz notebooks Jupyter para auxiliar na [implantação](deploy-notebooks.md) e [descoberta, diagnóstico e solução de problemas](manage-notebooks.md) de componentes em um cluster de Big Data do SQL Server. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="polybase"></a>PolyBase

- O push-down da cláusula TOP quando a contagem é superior a 1000 não é compatível com esta versão. Todas as linhas serão lidas da fonte de dados remota nesses casos. (Corrigido na versão Release Candidate)

- O push-down de junções colocalizadas para fontes de dados externas não é compatível com esta versão. Por exemplo, o push-down de duas tabelas de pool de dados do tipo de distribuição ROUND_ROBIN fará com que os dados sejam movidos para a instância mestre do SQL ou a instância do pool de computação a fim de realizar a operação de junção.

#### <a name="compute-pool"></a>Pool de computação

- A implantação de cluster de Big Data só dá suporte ao pool de computação com uma instância. (Corrigido na versão Release Candidate)

#### <a name="storage-pool"></a>Pool de armazenamento

- A consulta de arquivos parquet no pool de armazenamento não dá suporte a determinados tipos de dados.

- As colunas pai MAP e LIST, bem como colunas pai sem um tipo anexado, não podem ser consultadas. Isso retornará um erro.

- Os nós REPEATED não podem ser consultados e podem retornar resultados incorretos.

## <a id="ctp31"></a> CTP 3.1 (junho)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 3.1.

### <a name="whats-new"></a>O Que Há de Novo

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Alterações de comando `mssqlctl` | Comandos `mssqlctl cluster` foram renomeados para `mssqlctl bdc`. Para obter mais informações, consulte a [referência do `mssqlctl`](reference-azdata.md). |
| Novos comandos de status `mssqlctl` e remoção do Portal de administração de cluster. | O Portal de administração de cluster foi removido nesta versão. Novos comandos de status que complementam os comandos de monitoramento existentes foram adicionados ao `mssqlctl`. |
| Pools de computação do Spark | Crie nós adicionais para aumentar a potência de computação do Spark sem precisar escalar verticalmente o armazenamento. Além disso, você pode iniciar nós de pool de armazenamento que não são usados para o Spark. O Spark e o armazenamento são separados. Para obter mais informações, consulte [Configurar o armazenamento sem o Spark](deployment-custom-configuration.md#sparkstorage). |
| Conector do Spark MSSQL | Suporte para leitura/gravação para tabelas externas do pool de dados. As versões anteriores eram compatíveis apenas com leitura/gravação para tabelas da instância MASTER. Para obter mais informações, consulte [Como ler e gravar para o SQL Server no Spark usando o Conector do Spark MSSQL](spark-mssql-connector.md). |
| Machine Learning usando o MLeap | [Treine um modelo de machine learning do MLeap no Spark e pontue-o no SQL Server usando a extensão da linguagem Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível.

   > [!IMPORTANT]
   > Você precisa fazer backup dos dados e, em seguida, excluir o cluster de Big Data existente ( usando a versão anterior do **azdata**) antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- A implantação de cluster de Big Data não cria mais as fontes de dados externas **SqlDataPool** e **SqlStoragePool**. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   > [!NOTE]
   > O URI para criar essas fontes de dados externas é diferente entre CTPs. Confira os comandos Transact-SQL abaixo para ver como criá-las 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que use tipos de dados de caractere, o assistente de virtualização do Azure Data Studio interpretará essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema Oracle para usar o tipo NVARCHAR2 ou crie instruções EXTERNAL TABLE manualmente e especifique NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação do aplicativo

- Ao chamar um aplicativo R, Python ou MLeap da API RESTful, o tempo limite da chamada é de 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

#### <a name="kibana-logs-dashboards"></a>Painéis de logs do Kibana

- Entre o CTP 3.0 e o 3.1, a versão do Kibana foi atualizada de 6.3.1 para 7.0.1.  Isso fez com que o navegador Microsoft Edge seja incompatível com o Kibana. Os usuários verão uma página em branco ao carregar a versão atual dos painéis do Kibana no Microsoft Edge. Confira [aqui]( https://www.elastic.co/support/matrix#matrix_browse) os navegadores compatíveis com o Kibana.rs 


## <a id="ctp30"></a> CTP 3.0 (maio)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 3.0.

### <a name="whats-new"></a>O Que Há de Novo

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Atualizações de **mssqlctl** | Várias [atualizações de comando e parâmetro](reference-azdata.md) do **mssqlctl**. Isso inclui uma atualização do comando **mssqlctl login**, que agora direciona o nome de usuário do controlador e o ponto de extremidade. |
| Melhorias no armazenamento | Suporte para diferentes configurações de armazenamento para logs e dados. Além disso, o número de declarações de volume persistente para um cluster de Big Data foi reduzido. |
| Várias instâncias do pool de computação | Suporte para várias instâncias do pool de computação. |
| Novas funcionalidades e novo comportamento do pool | O pool de computação agora é usado por padrão em operações do pool de dados e do pool de armazenamento apenas em uma distribuição **ROUND_ROBIN**. Agora o pool de dados pode usar um novo tipo de distribuição **REPLICATED**, o que significa que os mesmos dados estão presentes em todas as instâncias do pool de dados. |
| Melhorias na tabela externa | As tabelas externas do tipo de fonte de dados HADOOP agora dão suporte à leitura de linhas com até 1 MB. As tabelas externas (ODBC, pool de armazenamento, pool de dados) agora dão suporte a linhas da mesma largura de uma tabela do SQL Server. |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="hdfs"></a>HDFS

- O Azure Data Studio retorna um erro quando você tenta criar uma nova pasta no HDFS. Para habilitar essa funcionalidade, instale o insiders build do Azure Data Studio:
  
   - [Instalador de Usuário do Windows – **Insiders build**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Instalador de Sistema do Windows – **Insiders build**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP – **Insiders build**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP – **Insiders build**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [TAR.GZ do Linux – **Insiders build**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="deployment"></a>Implantação

- Os procedimentos de implantação anteriores para clusters de Big Data habilitados para GPU não são compatíveis com o CTP 3.0. Um procedimento de implantação alternativo está sendo investigado. Por enquanto, a publicação do artigo "Implantar um cluster de Big Data com suporte a GPU e executar o TensorFlow" foi temporariamente cancelada para evitar confusão.

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível.

   > [!IMPORTANT]
   > Você precisa fazer backup dos dados e, em seguida, excluir o cluster de Big Data existente ( usando a versão anterior do **azdata**) antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- A implantação de cluster de Big Data não cria mais as fontes de dados externas **SqlDataPool** e **SqlStoragePool**. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   > [!NOTE]
   > O URI para criar essas fontes de dados externas é diferente entre CTPs. Confira os comandos Transact-SQL abaixo para ver como criá-las 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que use tipos de dados de caractere, o assistente de virtualização do Azure Data Studio interpretará essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema Oracle para usar o tipo NVARCHAR2 ou crie instruções EXTERNAL TABLE manualmente e especifique NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação do aplicativo

- Ao chamar um aplicativo R, Python ou MLeap da API RESTful, o tempo limite da chamada é de 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp25"></a> CTP 2.5 (abril)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.5.

### <a name="whats-new"></a>O Que Há de Novo

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Perfis de implantação | Use os [arquivos JSON de configuração de implantação](deployment-guidance.md#configfile) para padrão e personalizados para implantações de cluster de Big Data, em vez de variáveis de ambiente. |
| Implantações solicitadas | O `azdata cluster create` agora solicitará qualquer configuração necessária para implantações padrão. |
| Alterações de nome de ponto de extremidade de serviço e de pod | Os nomes dos seguintes pontos de extremidade externos foram alterados:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| aprimoramentos do **azdata** | Use **azdata** para [listar pontos de extremidade externos](deployment-guidance.md#endpoints) e verifique a versão do **azdata** com o parâmetro `--version`. |
| Instalação offline | Diretrizes para implantações de cluster de Big Data offline. |
| Melhorias em camadas do HDFS | Nível S3, cache de montagem e OAuth para ADLS Gen2. |
| Novo conector `mssql` do Spark para SQL Server | |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível.

   > [!IMPORTANT]
   > Você precisa fazer backup dos dados e, em seguida, excluir o cluster de Big Data existente ( usando a versão anterior do **azdata**) antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- A implantação de cluster de Big Data não cria mais as fontes de dados externas **SqlDataPool** e **SqlStoragePool**. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que use tipos de dados de caractere, o assistente de virtualização do Azure Data Studio interpretará essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema Oracle para usar o tipo NVARCHAR2 ou crie instruções EXTERNAL TABLE manualmente e especifique NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação do aplicativo

- Ao chamar um aplicativo R, Python ou MLeap da API RESTful, o tempo limite da chamada é de 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp24"></a> CTP 2.4 (março)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.4.

### <a name="whats-new"></a>O Que Há de Novo

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Diretrizes de suporte de GPU para execução de aprendizado profundo com o TensorFlow no Spark. | [Implantar um cluster de Big Data com suporte GPU e executar o TensorFlow](spark-gpu-tensorflow.md). |
| As fontes de dados **SqlDataPool** e **SqlStoragePool** não são mais criadas por padrão. | Crie-os manualmente, se necessário. Veja os [problemas conhecidos](#externaltablesctp24). |
| Suporte a `INSERT INTO SELECT` para o pool de dados. | Para um exemplo, veja [Tutorial: Ingerir dados em um pool de dados do SQL Server com Transact-SQL](tutorial-data-pool-ingest-sql.md). |
| Opções `FORCE SCALEOUTEXECUTION` e `DISABLE SCALEOUTEXECUTION`. | Força ou desabilita o uso do pool de computação para consultas em tabelas externas. Por exemplo: `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Recomendações atualizadas de implantação do AKS. | Ao avaliar a clusters de Big Data no AKS, agora recomendamos usar um único nó de tamanho **Standard_L8s**. |
| Atualização de tempo de execução do Spark para o Spark 2.4. | |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível.

   > [!IMPORTANT]
   > Você precisa fazer backup dos dados e, em seguida, excluir o cluster de Big Data existente ( usando a versão anterior do **azdata**) antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="kubeadm-deployments"></a>implantações de kubeadm

Se você usar o kubeadm para implantar o Kubernetes em vários computadores, o portal de administração de cluster não exibirá corretamente os pontos de extremidade necessários para conexão ao cluster de Big Data. Se você estiver enfrentando esse problema, use a seguinte solução alternativa para descobrir os endereços IP do ponto de extremidade de serviço:

- Se você estiver se conectando de dentro do cluster, consulte o Kubernetes para o IP do serviço referente ao ponto de extremidade ao qual você deseja se conectar. Por exemplo, o comando **kubectl** a seguir exibe o endereço IP da instância mestre do SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se você estiver se conectando de fora do cluster, use as seguintes etapas para se conectar:

   1. Obtenha o endereço IP do nó que executa a instância mestre de SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conecte-se à instância mestre do SQL Server usando esse endereço IP.

   1. Consulte o **cluster_endpoint_table** no banco de dados mestre para outros pontos de extremidade externos.

      Se isso falhar atingindo um tempo limite de conexão, é possível que o respectivo nó esteja protegido por firewall. Nesse caso, você deve entrar em contato com o administrador do cluster do Kubernetes e solicitar o IP do nó exposto externamente. Esse pode ser qualquer nó. Você pode usar esse IP e a porta correspondente para se conectar a vários serviços em execução no cluster. Por exemplo, o administrador pode encontrar esse IP executando:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>A exclusão do cluster falha

Quando você tenta excluir um cluster com **azdata**, isso falha com o seguinte erro:

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

Um novo cliente Kubernetes do Python (versão 9.0.0) alterou a API de exclusão de namespaces, que atualmente interrompe o **azdata**. Isso só acontece se você tem um cliente Kubernetes do Python mais recente instalado. Você pode contornar esse problema excluindo diretamente o cluster usando **kubectl** (`kubectl delete ns <ClusterName>`) ou pode instalar a versão mais antiga usando `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a> Tabelas externas

- A implantação de cluster de Big Data não cria mais as fontes de dados externas **SqlDataPool** e **SqlStoragePool**. Você pode criar essas fontes de dados manualmente para dar suporte à virtualização de dados para o pool de dados e o pool de armazenamento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que use tipos de dados de caractere, o assistente de virtualização do Azure Data Studio interpretará essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema Oracle para usar o tipo NVARCHAR2 ou crie instruções EXTERNAL TABLE manualmente e especifique NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação do aplicativo

- Ao chamar um aplicativo R, Python ou MLeap da API RESTful, o tempo limite da chamada é de 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp23"></a> CTP 2.3 (fevereiro)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.3.

### <a name="whats-new"></a>O Que Há de Novo

| Novo recurso ou atualização | Detalhes |
| :---------- | :------ |
| Enviar trabalhos do Spark em clusters de Big Data no IntelliJ. | [Enviar trabalhos do Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| CLI comum para gerenciamento de cluster e de implantação do aplicativo. | [Como implantar um aplicativo em[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-create-apps.md) |
| Extensão do VS Code para implantar aplicativos em um cluster de Big Data. | [Como usar VS Code para implantar aplicativos no[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](app-deployment-extension.md) |
| Alterações no uso de comandos da ferramenta **azdata**. | Para obter mais detalhes, confira os [problemas conhecidos do azdata](#azdatactp23). |
| Usar o Sparklyr em um cluster de Big Data | [Usar o Sparklyr em clusters de Big Data do SQL Server 2019](sparklyr-from-RStudio.md) |
| Montar armazenamento compatível com HDFS externo no cluster de Big Data com a disposição em **camadas do HDFS**. | Veja [Camadas do HDFS](hdfs-tiering.md). |
| Nova experiência de conexão unificada para a instância principal do SQL Server e o Gateway do HDFS/Spark. | Veja [Instância principal do SQL Server e o Gateway do HDFS/Spark](connect-to-big-data-cluster.md). |
| Excluir um cluster com **azdata cluster delete** agora exclui somente os objetos no namespace que faziam parte do cluster de Big Data. | O namespace não é excluído. No entanto, em versões anteriores, esse comando excluía todo o namespace. |
| Nomes de ponto de extremidade de _segurança_ foram alterados e consolidados. | **service-security-lb** e **service-security-nodeport** foram consolidados no ponto de extremidade **endpoint-security**. |
| Nomes de ponto de extremidade de _proxy_ foram alterados e consolidados. | **service-proxy-lb** e **service-proxy-nodeport** foram consolidados no ponto de extremidade **endpoint-service-proxy**. |
| Nomes de ponto de extremidade de _controlador_ foram alterados e consolidados. | **service-mssql-controller-lb** e **service-mssql-controller-nodeport** foram consolidados no ponto de extremidade **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível.

   > [!IMPORTANT]
   > Você precisa fazer backup dos dados e, em seguida, excluir o cluster de Big Data existente ( usando a versão anterior do **azdata**) antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- A variável de ambiente **ACCEPT_EULA** deve ser "yes" ou "Yes" para aceitar os termos de licença. As versões anteriores permitiam "y" e "Y", mas essas opções não são mais aceitas e, se usadas, farão com que a implantação falhe.

- As variáveis de ambiente **CLUSTER_PLATFORM** não têm um padrão, assim como ocorria em versões anteriores.

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="kubeadm-deployments"></a>implantações de kubeadm

Se você usar o kubeadm para implantar o Kubernetes em vários computadores, o portal de administração de cluster não exibirá corretamente os pontos de extremidade necessários para conexão ao cluster de Big Data. Se você estiver enfrentando esse problema, use a seguinte solução alternativa para descobrir os endereços IP do ponto de extremidade de serviço:

- Se você estiver se conectando de dentro do cluster, consulte o Kubernetes para o IP do serviço referente ao ponto de extremidade ao qual você deseja se conectar. Por exemplo, o comando **kubectl** a seguir exibe o endereço IP da instância mestre do SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Se você estiver se conectando de fora do cluster, use as seguintes etapas para se conectar:

   1. Obtenha o endereço IP do nó que executa a instância mestre de SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conecte-se à instância mestre do SQL Server usando esse endereço IP.

   1. Consulte o **cluster_endpoint_table** no banco de dados mestre para outros pontos de extremidade externos.

      Se isso falhar atingindo um tempo limite de conexão, é possível que o respectivo nó esteja protegido por firewall. Nesse caso, você deve entrar em contato com o administrador do cluster do Kubernetes e solicitar o IP do nó exposto externamente. Esse pode ser qualquer nó. Você pode usar esse IP e a porta correspondente para se conectar a vários serviços em execução no cluster. Por exemplo, o administrador pode encontrar esse IP executando:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a> azdata

- A ferramenta **azdata** mudou de uma ordem de comando verbo-substantivo para uma ordem substantivo-verbo. Por exemplo, `azdata create cluster` agora é `azdata cluster create`.

- Agora o parâmetro `--name` é necessário ao criar um cluster com `azdata cluster create`.

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- Para obter informações importantes sobre como atualizar para a versão mais recente de clusters de Big Data e **azdata**, confira [Atualizar para uma nova versão](deployment-upgrade.md).

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Se você estiver criando uma tabela externa para o Oracle que use tipos de dados de caractere, o assistente de virtualização do Azure Data Studio interpretará essas colunas como VARCHAR na definição da tabela externa. Isso causará uma falha na DDL da tabela externa. Modifique o esquema Oracle para usar o tipo NVARCHAR2 ou crie instruções EXTERNAL TABLE manualmente e especifique NVARCHAR em vez de usar o assistente.

#### <a name="application-deployment"></a>Implantação do aplicativo

- Ao chamar um aplicativo R, Python ou MLeap da API RESTful, o tempo limite da chamada é de 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp22"></a> CTP 2.2 (dezembro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.2.

### <a name="new-features"></a>Novos recursos

- Portal de administração de cluster acessado com `/portal` (**https://\<endereço-ip\>:30777/portal**).
- O nome do serviço do pool mestre foi alterado de `service-master-pool-lb` e `service-master-pool-nodeport` para `endpoint-master-pool`.
- Nova versão do **azdata** e imagens atualizadas.
- Correções e aprimoramentos de bugs diversos.

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem os problemas conhecidos e as limitações dessa versão.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível. Você deve fazer backup e excluir todos os clusters de Big Data existentes antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="cluster-administration-portal"></a>Portal de administração de cluster

O Portal de administração de cluster não exibe o ponto de extremidade para a instância mestre do SQL Server. Para localizar o endereço IP e a porta para a instância mestre, use o seguinte comando **kubectl**:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp21"></a> CTP 2.1 (novembro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.1.

### <a name="new-features"></a>Novos recursos

- [Implantar aplicativos Python e R](big-data-cluster-create-apps.md) em um cluster de Big Data.
- Nova versão do **azdata** e imagens atualizadas. 
- Correções e aprimoramentos de bugs diversos.

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir fornecem problemas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] conhecidos no CTP 2,1.

#### <a name="deployment"></a>Implantação

- A atualização de um cluster de dados de Big Data de uma versão anterior não é compatível. Você deve fazer backup e excluir todos os clusters de Big Data existentes antes de implantar a versão mais recente. Para obter mais informações, confira [Atualizar para uma nova versão](deployment-upgrade.md).

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="admin-portal"></a>Portal de administração

- Quando você [cria um aplicativo usando o comando msqlctl-ctp](big-data-cluster-create-apps.md) e o implanta em um cluster de Big Data do SQL Server, o Portal de administração de cluster mostra os pods em que o aplicativo foi implantado como "Desconhecido" na seção Controlador da parte de Administração.

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a id="ctp20"></a> CTP 2.0 (outubro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos de clusters de Big Data no SQL Server 2019 CTP 2.0.

### <a name="new-features"></a>Novos recursos

- Experiência de implantação simples usando a ferramenta de gerenciamento azdata
- Experiência de notebook nativo no Azure Data Studio
- Consultar arquivos HDFS por meio da instância de armazenamento do SQL Server
- Virtualização de dados por meio do mestre para SQL Server, Oracle, MongoDB e HDFS
- Assistente de virtualização de dados para SQL Server e Oracle no Azure Data Studio
- Serviços de ML no mestre
- Portal de administração de cluster que você pode usar para monitoramento e solução de problemas
- Envio de trabalhos do Spark no Azure Data Studio 
- Interface do usuário do Spark no Portal de administração de cluster
- Montagem de volume para classes de armazenamento
- Consultas por pools de dados do mestre
- Mostrar plano para consultas distribuídas no SSMS
- Pacote pip para a ferramenta de gerenciamento azdata
- Mecanismo de implantação interno por meio do serviço de controlador

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir fornecem problemas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] conhecidos no CTP 2,0.

#### <a name="deployment"></a>Implantação

- Se você estiver usando o AKS (Serviço de Kubernetes do Azure), a versão recomendada do Kubernetes será 1.10.*, que não dá suporte ao redimensionamento de disco. Você deve verificar se está dimensionando o armazenamento adequadamente no momento da implantação. Para obter mais informações sobre como ajustar os tamanhos de armazenamento, confira o artigo [Persistência de dados](concept-data-persistence.md). Para o Kubernetes implantado em VMs, a versão recomendada é 1.11.

- Depois de implantar no AKS, você poderá ver os dois eventos de aviso a seguir originados da implantação. Esses dois eventos são problemas conhecidos, mas eles não impedem que você implante o cluster Big Data com êxito no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de Big Data falhar, o namespace associado não será removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem tipos de coluna sem suporte. Se você consultar a tabela externa, receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa de pool de armazenamento, poderá receber um erro se o arquivo subjacente estiver sendo copiado para o HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Os endereços IP de POD podem sofrer alterações no ambiente do Kubernetes quando os PODs são reiniciados. No cenário em que o pod mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com novos endereços IP.

- Se você já tiver o Jupyter instalado e um Python separado no Windows, os notebooks do Spark poderão falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um notebook, se você clicar no comando **Adicionar Texto**, a célula de texto será adicionada no modo de visualização, não no modo de edição. Você pode clicar no ícone de visualização para alternar para o modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se clicar com o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente, não há nenhuma maneira de visualizar arquivos com mais de 30 MB no Azure Data Studio.

- Alterações de configuração no HDFS que envolvam alterações a hdfs-site.xml não são compatíveis.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e é detectável (por exemplo, em um arquivo de despejo de núcleo). Você precisa redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, confira [Alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Os logs do AKS podem conter a senha SA para implantações de cluster de Big Data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]sobre o, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
