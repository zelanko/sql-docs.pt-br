---
title: Exibir status do cluster
titleSuffix: SQL Server big data clusters
description: Este artigo explica como exibir o status de um cluster Big Data usando os comandos Azure Data Studio, notebooks e azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419291"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Como exibir o status de um cluster Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como acessar os pontos de extremidade de serviço e exibir o status de um cluster SQL Server Big Data (versão prévia). Você pode usar o Azure Data Studio e o **azdata**, e este artigo aborda as duas técnicas.

## <a id="datastudio"></a>Usar Azure Data Studio

Depois de baixar a **versão** mais recente do [Azure Data Studio](https://aka.ms/azdata-insiders), você pode exibir pontos de extremidade de serviço e o status de um cluster Big Data com o painel SQL Server Big data cluster. Observe que alguns dos recursos a seguir estão disponíveis apenas na compilação de insiders de Azure Data Studio.

1. Primeiro, crie uma conexão com o cluster Big Data no Azure Data Studio. Para obter mais informações, consulte [conectar-se a um cluster SQL Server Big data com o Azure Data Studio](connect-to-big-data-cluster.md).

1. Clique com o botão direito do mouse no ponto de extremidade do cluster Big Data e clique em **gerenciar**.

   ![Clique com o botão direito gerenciar](media/view-cluster-status/right-click-manage.png)

1. Selecione a guia **SQL Server Cluster de Big data** para acessar o painel de cluster Big Data.

   ![Painel de cluster de Big data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

É importante poder acessar facilmente os vários serviços em um cluster Big Data. O painel de cluster Big Data fornece uma tabela de pontos de extremidade de serviço que permite ver e copiar os pontos de extremidade de serviço.

![pontos de extremidade de serviço](media/view-cluster-status/service-endpoints.png)

As primeiras várias linhas expõem os seguintes serviços:

- Proxy de aplicativo
- Serviço de gerenciamento de cluster
- HDFS e Spark
- Proxy de gerenciamento

Esses serviços listam os pontos de extremidade que podem ser copiados e colados quando você precisa do ponto de extremidades para se conectar a esses serviços. Por exemplo, você pode clicar no ícone de cópia à direita do ponto de extremidade e, em seguida, colá-lo em uma janela de texto solicitando esse ponto de extremidade. O ponto de extremidade do serviço de gerenciamento de cluster é necessário para executar o [bloco de anotações de status do cluster](#notebook).

### <a name="dashboards"></a>Painéis

A tabela de pontos de extremidade de serviço também expõe vários painéis para monitoramento:

- Métricas (Grafana)
- Logs (Kibana)
- Monitoramento de trabalhos do Spark
- Gerenciamento de recursos do Spark

Você pode clicar diretamente nesses links. Você é solicitado duas vezes a fornecer seu nome de usuário e senha antes de se conectar ao serviço.

### <a id="notebook"></a>Bloco de anotações de status do cluster

1. Você também pode exibir o status do cluster do Big Data cluster iniciando o bloco de anotações de status do cluster. Para iniciar o bloco de anotações, clique na tarefa **status do cluster** .

    ![Iniciar](media/view-cluster-status/cluster-status-launch.png)

2. Antes de começar, você precisará dos seguintes itens:

    - Nome do cluster de Big data
    - Nome de usuário do controlador
    - Senha do controlador
    - Pontos de extremidade do controlador

    O nome de cluster Big Data padrão é **MSSQL-cluster** , a menos que você o tenha personalizado durante a implantação. Você pode encontrar o ponto de extremidade do controlador no painel Big Data cluster na tabela pontos de extremidade de serviço. O ponto de extremidade é listado como **serviço de gerenciamento de cluster**. Se você não souber as credenciais, peça ao administrador que implantou o cluster.

3. Clique em **executar células** na barra de ferramentas superior.

4. Siga o prompt para suas credenciais. Pressione ENTER depois de digitar cada credencial para o Big Data nome do cluster, o nome de usuário do controlador e a senha do controlador.

    > [!Note]
    > Se você não tiver uma configuração de arquivo de configuração com seu Big Data, você será solicitado para o ponto de extremidade do controlador. Digite ou cole-o e pressione ENTER para continuar.

5. Se você se conectou com êxito, o restante do notebook mostrará a saída de cada componente do cluster de Big Data. Quando você quiser executar novamente uma determinada célula de código, passe o mouse sobre a célula de código e clique no ícone **executar** .

## <a name="use-azdata"></a>Usar azdata

Você também pode usar comandos [azdata](deploy-install-azdata.md) para exibir os dois pontos de extremidade e o status do cluster.

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

Você pode obter os endereços IP dos pontos de extremidade externos para o cluster Big Data usando as etapas a seguir.

1. Localize o endereço IP do ponto de extremidade do controlador examinando a saída de IP externo do seguinte comando **kubectl** :

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome padrão durante a implantação, `-n mssql-cluster` use no comando anterior. **MSSQL-cluster** é o nome padrão para o cluster de Big Data.

1. Faça logon no cluster Big Data com [logon azdata](reference-azdata.md). Defina o parâmetro **--Controller-Endpoint** como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute a [lista de pontos de extremidade do BDC do azdata](reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

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

Você pode exibir o status do cluster com o comando [azdata BDC status show](reference-azdata-bdc-status.md) .

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para executar os comandos de status, primeiro você deve fazer logon com o comando de **logon azdata** , que foi mostrado na seção pontos de extremidade anteriores.

Veja a seguir uma saída de exemplo deste comando:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

### <a name="view-pool-status"></a>Exibir status do pool

Você pode exibir o status dos pools no cluster com o comando [azdata BDC pool status show](reference-azdata-bdc-pool-status.md) . Para usar esse comando, especifique o tipo de pool com o `--kind` parâmetro. Os tipos de pool são:

- Nós
- data
- master
- Spark
- Repositório

Por exemplo, o comando a seguir exibe o status do pool do pool de armazenamento:

```bash
azdata bdc pool status show --kind storage
```

Você deve ver um texto semelhante à seguinte saída:

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

O `logsUrl` valor é vinculado a um painel do kibana com informações de log:

![Painel do Kibana](./media/view-cluster-status/kibana-dashboard.png)

Os `nodeMetricsUrl` valores `sqlMetricsUrl` e são vinculados a um painel do grafana para monitorar a integridade do nó e as métricas do SQL:

![Painel do Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Exibir status do controlador

Você pode exibir o status do controlador com o comando [azdata BDC Control status show](reference-azdata-bdc-control-status.md) . Ele fornece links semelhantes aos painéis de monitoramento relacionados aos nós do controlador do cluster Big Data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são SQL Server Big data clusters](big-data-cluster-overview.md).
