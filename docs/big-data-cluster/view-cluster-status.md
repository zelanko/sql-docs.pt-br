---
title: Exibir status do cluster
titleSuffix: SQL Server big data clusters
description: Este artigo explica como exibir o status de um cluster de big data usando o Studio de dados do Azure, os blocos de anotações e mssqlctl comandos.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b3cc78e36fe427966c7730533104c63aa3ed9332
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727323"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Como exibir o status de um cluster de big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como acessar os pontos de extremidade de serviço e exibir o status de um cluster de big data do SQL Server (versão prévia). Você pode usar ambos os Studio de dados do Azure e **mssqlctl**, e este artigo aborda ambas as técnicas.

## <a id="datastudio"></a> Usar o Studio de dados do Azure

Depois de baixar a versão mais recente **build insiders** dos [Studio do Azure Data](https://aka.ms/azdata-insiders), você pode exibir os pontos de extremidade de serviço e o status de um grande de dados de cluster com o painel do cluster grande de dados do SQL Server. Observe que alguns dos recursos a seguir estão apenas pela primeira vez disponíveis no build insiders do estúdio de dados do Azure.

1. Primeiro, crie uma conexão para seu cluster de big data no estúdio de dados do Azure. Para obter mais informações, consulte [conectar-se a um SQL Server cluster de big data com o Azure Data Studio](connect-to-big-data-cluster.md).

1. Clique com botão direito no ponto de extremidade de cluster de big data e, em seguida, clique em **gerenciar**.

   ![gerenciar o botão direito do mouse](media/view-cluster-status/right-click-manage.png)

1. Selecione o **Cluster grande de dados do SQL Server** tab para acessar o painel do cluster de big data.

   ![Painel do cluster de big data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

É importante ser capaz de acessar facilmente os vários serviços dentro de um cluster de big data. O painel do cluster de big data fornece uma tabela de pontos de extremidade de serviço que permite que você veja e copie os pontos de extremidade de serviço.

![Pontos de extremidade de serviço](media/view-cluster-status/service-endpoints.png)

As primeiras linhas expõem os seguintes serviços:

- Proxy de aplicativo
- Serviço de gerenciamento de cluster
- HDFS e Spark
- Proxy de gerenciamento

Esses serviços listam os pontos de extremidade que podem ser copiados e colados quando precisar que o ponto de extremidade para se conectar a esses serviços. Você pode, por exemplo, clique no ícone de cópia à direita do ponto de extremidade e, em seguida, cole-o em uma janela de texto, solicitando esse ponto de extremidade. O ponto de extremidade do serviço de gerenciamento de Cluster é necessário executar o [bloco de anotações do cluster status](#notebook).

### <a name="dashboards"></a>Painéis

A tabela de pontos de extremidade de serviço também expõe vários painéis de monitoramento:

- Métricas (Grafana)
- Logs (Kibana)
- Monitoramento de trabalho do Spark
- Gerenciamento de recursos do Spark

Você pode clicar diretamente nesses links. Você será solicitado duas vezes a fornecer seu nome de usuário e senha antes de se conectar ao serviço.

### <a id="notebook"></a> Bloco de anotações de Status de cluster

1. Você também pode exibir o status do cluster do cluster de big data iniciando o bloco de anotações do Status do Cluster. Para iniciar o bloco de anotações, clique o **Status do Cluster** tarefa.

    ![Iniciar](media/view-cluster-status/cluster-status-launch.png)

2. Antes de começar, você precisará dos seguintes itens:

    - Nome do cluster de big data
    - Nome de usuário do controlador
    - Senha do controlador
    - Pontos de extremidade do controlador

    É o nome padrão do cluster de big data **mssql-cluster** , a menos que você o personalizado durante a implantação. Você pode encontrar o ponto de extremidade de controlador do painel do cluster de big data na tabela de pontos de extremidade de serviço. O ponto de extremidade está listado como **serviço de gerenciamento de Cluster**. Se você não souber as credenciais, peça ao administrador que implantado o cluster.

3. Clique em **células executar** na barra de ferramentas superior.

4. Siga os prompts para suas credenciais. Pressione pressione ENTER depois de digitar cada credencial para o nome do cluster de big data, nome de usuário do controlador e a senha do controlador.

    > [!Note]
    > Se você não tiver uma configuração de arquivo de configuração com seu big data, você será solicitado para o ponto de extremidade do controlador. Digite ou cole-o e, em seguida, pressione ENTER para continuar.

5. Se você estiver conectado com êxito, o restante do bloco de anotações mostra a saída de cada componente do cluster de big data. Quando você quiser executar novamente uma célula de código determinados, passe o mouse sobre a célula de código e clique no **executar** ícone.

## <a name="use-mssqlctl"></a>Usar mssqlctl

Você também pode usar [mssqlctl](deploy-install-mssqlctl.md) comandos para exibir os pontos de extremidade e o status do cluster.

### <a name="service-endpoints"></a>Pontos de extremidade de serviço

Você pode obter os endereços IP dos pontos de extremidade externos para o cluster de big data usando as etapas a seguir.

1. Localizar o endereço IP do ponto de extremidade controlador examinando a saída EXTERNAL-IP dos seguintes **kubectl** comando:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se você não alterou o nome padrão durante a implantação, use `-n mssql-cluster` no comando anterior. **MSSQL-cluster** é o nome padrão para o cluster de big data.

1. Faça logon no cluster de big data com [mssqlctl logon](reference-mssqlctl.md). Defina a **– controlador de ponto de extremidade** parâmetro para o endereço IP externo do ponto de extremidade de controlador.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique o nome de usuário e a senha que você configurou para o controlador (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante a implantação.

1. Execute [lista de ponto de extremidade do bdc mssqlctl](reference-mssqlctl-bdc-endpoint.md) para obter uma lista com uma descrição de cada ponto de extremidade e seus valores correspondentes de porta e endereço IP. 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   A lista a seguir mostra um exemplo de saída deste comando:

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

Você pode exibir o status do cluster com o [show de status do bdc mssqlctl](reference-mssqlctl-bdc-status.md) comando.

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> Para executar os comandos de status, você deve primeiro fazer logon com o **mssqlctl logon** comando, que foi mostrado na seção de pontos de extremidade anterior.

O exemplo a seguir mostra o exemplo de saída desse comando:

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

Você pode exibir o status dos pools dentro do cluster com o [mssqlctl show de status de pool de bdc](reference-mssqlctl-bdc-pool-status.md) comando. Para usar esse comando, especifique o tipo de pool com o `--kind` parâmetro. Os tipos de pool são:

- Computação
- data
- master
- Spark
- Armazenamento

Por exemplo, o comando a seguir exibe o status do pool do pool de armazenamento:

```bash
mssqlctl bdc pool status show --kind storage
```

Você deve ver o texto semelhante à seguinte saída:

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

O `logsUrl` links para um painel kibana com informações do log de valor:

![painel kibana](./media/view-cluster-status/kibana-dashboard.png)

O `nodeMetricsUrl` e `sqlMetricsUrl` valores vincular a um painel do grafana para monitoramento de integridade do nó e métricas SQL:

![Painel do Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Status do controlador de exibição

Você pode exibir o status do controlador com o [mssqlctl bdc controle status mostrar](reference-mssqlctl-bdc-control-status.md) comando. Ele fornece links semelhantes para os painéis de monitoramentos relacionados a nós de cluster de big data controlador.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters de grandes dados do SQL Server](big-data-cluster-overview.md).
