---
title: Exibir status do cluster
titleSuffix: SQL Server big data clusters
description: Este artigo explica como exibir o status de um cluster de Big Data usando o Azure Data Studio, notebooks e comandos azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 028864712658e35913fa04fb1a85e4ca960ad573
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653272"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Como exibir o status de um cluster de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como acessar os pontos de extremidade de serviço e exibir o status de um cluster de Big Data do SQL Server (versão prévia). É possível usar o Azure Data Studio e **azdata** e este artigo descreve as duas técnicas.

## <a id="datastudio"></a> Usar o Azure Data Studio

Depois de baixar o **build para insiders** mais recente do [Azure Data Studio](https://aka.ms/azdata-insiders), você pode exibir pontos de extremidade de serviço e o status de um cluster de Big Data com o painel do cluster de Big Data do SQL Server. Observe que alguns dos recursos a seguir estão disponíveis apenas no build para insiders do Azure Data Studio.

1. Primeiro, crie uma conexão com o cluster de Big Data no Azure Data Studio. Para obter mais informações, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

1. Clique com o botão direito do mouse no ponto de extremidade do cluster de Big Data e clique em **Gerenciar**.

   ![clicar com o botão direito do mouse em gerenciar](media/view-cluster-status/right-click-manage.png)

1. Selecione a guia **Cluster de Big Data do SQL Server** para acessar o painel do cluster de Big Data.

   ![Painel do cluster de Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

É importante poder acessar facilmente os vários serviços em um cluster de Big Data. O painel do cluster de Big Data fornece uma tabela dos pontos de extremidade de serviço que permite ver e copiá-los.

![pontos de extremidade de serviço](media/view-cluster-status/service-endpoints.png)

As primeiras linhas expõem os seguintes serviços:

- Proxy do Aplicativo
- Serviço de Gerenciamento do Cluster
- HDFS e Spark
- Proxy de Gerenciamento

Esses serviços listam os pontos de extremidade que podem ser copiados e colados quando você precisar do ponto de extremidade para se conectar a eles. Por exemplo, você pode clicar no ícone de copiar à direita do ponto de extremidade e colá-lo em uma janela de texto que solicita esse ponto de extremidade. O ponto de extremidade do Serviço de Gerenciamento do Cluster é necessário para executar o [notebook do status do cluster](#notebook).

### <a name="dashboards"></a>Painéis

A tabela de pontos de extremidade de serviço também expõe vários painéis para monitoramento:

- Métricas (Grafana)
- Logs (Kibana)
- Monitoramento de Trabalhos do Spark
- Gerenciamento de Recursos do Spark

Você pode clicar diretamente nesses links. Será solicitado duas vezes que você forneça seu nome de usuário e senha antes de se conectar ao serviço.

### <a id="notebook"></a> Notebook de Status do Cluster

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

Você pode obter os endereços IP dos pontos de extremidade externos do cluster de Big Data usando as etapas a seguir.

1. Localize o endereço IP do ponto de extremidade do controlador examinando a saída EXTERNAL-IP do seguinte comando **kubectl**:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se não tiver alterado o nome padrão durante a implantação, use `-n mssql-cluster` no comando anterior. **mssql-cluster** é o nome padrão do cluster de Big Data.

1. Faça logon no cluster de Big Data usando [azdata login](reference-azdata.md). Defina o parâmetro **--controller-endpoint** como o endereço IP externo do ponto de extremidade do controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores de porta e endereço IP correspondentes. 

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

Você pode exibir o status do cluster usando o comando o [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para executar os comandos de status, primeiro você precisa fazer logon usando o comando **azdata login**, que foi mostrado na seção anterior sobre pontos de extremidade.

Veja a seguir a saída de exemplo deste comando:

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

Você pode exibir o status dos pools dentro do cluster usando o comando o [azdata bdc pool status show](reference-azdata-bdc-pool-status.md). Para usar esse comando, especifique o tipo de pool com o parâmetro `--kind`. Os tipos de pool são:

- computação
- data
- master
- spark
- armazenamento

Por exemplo, o comando a seguir exibe o status do pool de armazenamento:

```bash
azdata bdc pool status show --kind storage
```

Será exibido um texto semelhante ao seguinte:

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

O valor `logsUrl` é vinculado a um painel do kibana com informações de log:

![Painel do kibana](./media/view-cluster-status/kibana-dashboard.png)

Os valores `nodeMetricsUrl` e `sqlMetricsUrl` são vinculados a um painel do grafana para monitorar a integridade do nó e as métricas do SQL:

![Painel do grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Exibir status do controlador

Você pode exibir o status do controlador usando o comando o [azdata bdc control status show](reference-azdata-bdc-control-status.md). Ele fornece links semelhantes aos painéis de monitoramento relacionados aos nós do controlador do cluster de Big Data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]que são ](big-data-cluster-overview.md).
