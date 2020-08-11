---
title: Exibir status do cluster
titleSuffix: SQL Server big data clusters
description: Este artigo explica como exibir o status de um cluster de Big Data usando o Azure Data Studio, notebooks e comandos azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5e3c7f2f34f949f16821ad7c1dd6a3c3b0d4681e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772824"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Como exibir o status de um cluster de Big Data 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como acessar os pontos de extremidade de serviço e exibir o status de componentes de um cluster de Big Data do SQL Server. É possível usar o Azure Data Studio e **azdata** e este artigo descreve as duas técnicas.

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> Usar o Azure Data Studio

Depois de baixar o **build para insiders** mais recente do [Azure Data Studio](https://aka.ms/getazuredatastudio), você pode exibir pontos de extremidade de serviço e o status de um cluster de Big Data com o painel do cluster de Big Data do SQL Server. Alguns dos recursos a seguir estão disponíveis apenas no build para insiders do Azure Data Studio.

1. Primeiro, crie uma conexão com o cluster de Big Data no Azure Data Studio. Para obter mais informações, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

1. Clique com o botão direito do mouse no ponto de extremidade do cluster de Big Data e clique em **Gerenciar**.

   ![clicar com o botão direito do mouse em gerenciar](media/view-cluster-status/right-click-manage.png)

1. Selecione a guia **Cluster de Big Data do SQL Server** para acessar o painel do cluster de Big Data.

   ![Painel do cluster de Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

É importante poder acessar facilmente os vários serviços em um cluster de Big Data. O painel do cluster de Big Data fornece uma tabela dos pontos de extremidade de serviço que permite ver e copiá-los.

![pontos de extremidade de serviço](media/view-cluster-status/service-endpoints.png)

Esses serviços listam os pontos de extremidade que podem ser copiados e colados quando você precisar do ponto de extremidade para se conectar a eles. Por exemplo, você pode clicar no ícone de copiar à direita do ponto de extremidade e colá-lo em uma janela de texto que solicita esse ponto de extremidade. O ponto de extremidade do Serviço de Gerenciamento do Cluster é necessário para executar o [notebook do status do cluster](#notebook).

### <a name="dashboards"></a>Painéis

A tabela de pontos de extremidade de serviço também expõe vários painéis para monitoramento:

- Métricas (Grafana)
- Logs (Kibana)
- Monitoramento de Trabalhos do Spark
- Gerenciamento de Recursos do Spark

Você pode clicar diretamente nesses links. Você será solicitado a autenticar ao acessar esses painéis. Para os painéis de métricas e logs, forneça as credenciais de administrador do controlador que você definiu no momento da implantação usando as variáveis de ambiente **AZDATA_USERNAME** e **AZDATA_PASSWORD**. Os painéis do Spark usarão as credenciais do gateway (Knox): a identidade do AD em um cluster integrado ao AD ou, se estiver usando a autenticação Básica no cluster, **AZDATA_USERNAME** e **AZDATA_PASSWORD**.

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> Notebook de Status do Cluster

1. Você também pode exibir o status do cluster de Big Data iniciando o notebook de Status do Cluster. Para iniciar o notebook, clique na tarefa **Status do Cluster**.

    ![inicialização](media/view-cluster-status/cluster-status-launch.png)

2. Antes de começar, você precisará dos seguintes itens:

    - Nome do cluster de Big Data
    - Nome de usuário do controlador
    - Senha do controlador
    - Pontos de extremidade do controlador

    O nome do cluster de Big Data padrão é **mssql-cluster**, a menos que você o tenha personalizado durante a implantação. É possível encontrar o ponto de extremidade do controlador no painel do cluster de Big Data na tabela Pontos de Extremidade do Serviço. O ponto de extremidade está listado como **Serviço de Gerenciamento do Cluster**. Se não conhecer as credenciais, peça ao administrador que implantou o cluster.

3. Clique em **Executar Células** na barra de ferramentas superior.

4. Siga o prompt para fornecer suas credenciais. Pressione ENTER depois de digitar cada credencial para o nome do cluster de Big Data, o nome de usuário do controlador e a senha do controlador.

    > [!Note]
    > Se você não tiver uma instalação de arquivo de configuração com seu Big Data, será solicitado que você informe o ponto de extremidade do controlador. Digite ou cole-o e pressione ENTER para continuar.

5. Se você tiver se conectado com êxito, o restante do notebook mostrará a saída de cada componente do cluster de Big Data. Quando quiser executar novamente uma determinada célula de código, passe o mouse sobre a célula de código e clique no ícone **Executar**.

## <a name="use-azdata"></a>Usar azdata

Você também pode usar comandos [azdata](deploy-install-azdata.md) para exibir os pontos de extremidade e o status do cluster.

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

1. Faça logon no cluster de Big Data usando [azdata login](reference-azdata.md). Defina o parâmetro **--controller-endpoint** como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (AZDATA_USERNAME e AZDATA_PASSWORD) durante a implantação. 
   Para a autenticação do AD, o comando é:

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. Execute [`azdata bdc endpoint list`](reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   A lista a seguir mostra a saída de exemplo deste comando:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>Exibir status do cluster

Você pode exibir o status do cluster com o comando [`azdata bdc status show`](reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Para executar os comandos de status, primeiro você precisa fazer logon usando o comando **azdata login**, que foi mostrado na seção anterior sobre pontos de extremidade.

Veja a seguir a saída de exemplo deste comando:

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>Exibir o status do recurso específico

Você pode exibir o status de um recurso específico dentro do cluster usando o comando o [azdata bdc status show](reference-azdata-bdc-status.md). Ao usar esse comando, você pode filtrar usando o parâmetro `--resource`. Alguns exemplos de entradas para o parâmetro `--resource` são:

- master
- controle
- compute-0
- storage-0
- gateway

Por exemplo, o comando a seguir exibe o status do pool de armazenamento:

```bash
azdata bdc status show --all --resource storage-0
```

Para ver o status de todos os componentes que estão executando um serviço específico, use o grupo de comandos correspondente `azdata bdc <serviceName> status show`. Por exemplo:

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

Aqui está um exemplo de saída:

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> Execute o comando de status com os parâmetros `--all` para obter detalhes adicionais de integridade, incluindo links para métricas e painéis de logs correspondentes à instância específica. Aqui está um exemplo de saída quando os parâmetros de `--all` são usados:

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

O valor de `logsUrl` vincula-se a um painel do Kibana:

![Painel do kibana](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> (Antigo) O navegador Microsoft Edge para iOS é incompatível com o Kibana, você deve usar o navegador baseado em Chrome para que o painel seja exibido corretamente. Você verá uma página em branco ao carregar os painéis usando um navegador sem suporte. Confira aqui os navegadores compatíveis com o Kibana.

Os valores `nodeMetricsUrl` e `sqlMetricsUrl` são vinculados a um painel do Grafana para monitorar as métricas do nó do Kubernetes e as métricas de serviço de cluster de Big Data:

![Painel do grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Exibir status do controlador

Você pode exibir o status do controlador com o comando [`azdata bdc control status show`](reference-azdata-bdc-control-status.md). Ele fornece links semelhantes aos painéis de monitoramento relacionados aos componentes do controlador do cluster de Big Data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).
