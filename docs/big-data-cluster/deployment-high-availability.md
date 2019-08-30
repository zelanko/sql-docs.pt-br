---
title: Implantar SQL Server Cluster de Big data com alta disponibilidade
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: Saiba como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia) no com alta disponibilidade.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2c0e5f5a5f194045b5d1b48a383f9d4dfd282649
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158161"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>Implantar SQL Server Cluster de Big data com alta disponibilidade

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

No momento da implantação de um BDC (cluster de Big Data), você pode configurar SQL Server mestre a ser implantado em uma configuração de grupo de disponibilidade. Essa configuração aumenta a confiabilidade do SQL Server mestre, além do que a infraestrutura kubernetes permite com seus mecanismos internos de monitoramento de integridade, detecção de falha e failover. Os grupos de disponibilidade (AG) adicionam redundância à instância de SQL Server. Nessa configuração, o monitoramento, a detecção de falhas e as tarefas de failover são gerenciados pelo serviço de gerenciamento de cluster Big Data, ou seja, o serviço de controle.

Além disso, outras tarefas de administração, como a configuração de pontos de extremidade de espelhamento de banco de dados, a criação do grupo de disponibilidade e a adição de bancos de dados ao grupo de disponibilidade são fornecidas pela plataforma de cluster Big Data.

Aqui estão alguns dos recursos que os grupos de disponibilidade habilitam:

1. Se as configurações de alta disponibilidade forem especificadas no arquivo de configuração de implantação, um único grupo `containedag` de disponibilidade chamado será criado. Por padrão, `containedag` o tem três réplicas, incluindo a primária. Todas as operações CRUD para o grupo de disponibilidade são gerenciadas internamente.
1. Todos os bancos de dados são adicionados automaticamente ao grupo de disponibilidade, `master` incluindo `msdb`e. Bancos de dados de configuração do polybase não são incluídos no grupo de disponibilidade porque incluem metadados de nível de instância específicos para cada réplica.
1. Um ponto de extremidade externo é provisionado automaticamente para se conectar aos bancos de dados AG. Esse ponto `master-svc-external` de extremidade desempenha a função do ouvinte AG.
1. Um segundo ponto de extremidade externo é provisionado para conexões somente leitura para as réplicas secundárias. 

# <a name="deploy"></a>Implantar

Para implantar SQL Server mestre em um grupo de disponibilidade:

1. Habilitar o `hadr` recurso
1. Especifique o número de réplicas para o AG (o mínimo é 3)
1. Configurar os detalhes do segundo ponto de extremidade externo criado para conexões com as réplicas secundárias somente leitura

As etapas a seguir mostram como criar um arquivo de patch que inclui essas configurações e como aplicá-lo a `aks-dev-test` um `kubeadm-dev-test` ou mais perfis de configuração. Estas etapas percorrem um exemplo de como corrigir o `aks-dev-test` perfil para adicionar os atributos de alta disponibilidade.

1. Criar um `ha-patch.json` arquivo

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. Clonar seu perfil de destino

    ```bash
    azdata config init --source aks-dev-test --target custom-aks
    ```

1. Aplicar o arquivo de patch ao seu perfil personalizado

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```

## <a name="connect-to-sql-server-databases"></a>Conectar-se a bancos de dados SQL Server

Dependendo do tipo de carga de trabalho que você deseja executar em SQL Server mestre, você pode se conectar ao primário para cargas de trabalho de leitura/gravação ou aos bancos de dados nas réplicas secundárias para o tipo somente leitura de cargas de trabalho. Aqui está uma estrutura de tópicos para cada tipo de conexão:

### <a name="connect-to-databases-on-the-primary-replica"></a>Conectar-se a bancos de dados na réplica primária

Para conexões com a réplica primária, use `sql-server-master` o ponto de extremidade. Esse ponto de extremidade também é o ouvinte para o AG. Todas as conexões estão no contexto do grupo de disponibilidade. Por exemplo, uma conexão padrão usando esse ponto de extremidade resultará na conexão `master` com o banco de dados no AG, não `master` no banco de dados de SQL Server instância.

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

### <a name="connect-to-databases-on-the-secondary-replicas"></a>Conectar-se a bancos de dados nas réplicas secundárias

Para conexões somente leitura para bancos de dados em réplicas secundárias, use o `sql-server-master-readonly` ponto de extremidade. Esse ponto de extremidade funciona como um balanceador de carga em todas as réplicas secundárias. Forneça o contexto do banco de dados do usuário na cadeia de conexão.

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>Conectar-se à instância do SQL Server

Para determinadas operações, como definir configurações de nível de servidor ou adicionar manualmente um banco de dados ao grupo de disponibilidade (caso o banco de dados tenha sido criado com um fluxo de trabalho de restauração), você precisa de uma conexão com a instância. Para fornecer essa conexão, expor um ponto de extremidade externo. Aqui está um exemplo que mostra como expor esse ponto de extremidade e, em seguida, adicionar o banco de dados que foi criado com um fluxo de trabalho de restauração ao grupo de disponibilidade.

- Determine o Pod que hospeda a réplica primária conectando-se `sql-server-master` ao ponto de extremidade e execute:

    ```sql
    SELECT @@SERVERNAME
   ```

- Expor o ponto de extremidade externo criando um novo serviço kubernetes

    Para um cluster kubeadm, execute o comando abaixo. Substitua `podName` pelo nome do servidor retornado na etapa anterior, `serviceName` com o nome preferencial para o serviço kubernetes criado e `namespaceName`* com o nome do seu cluster BDC.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    Para uma execução de cluster AKs, execute o mesmo comando, exceto que o tipo de serviço criado será `LoadBalancer`. Por exemplo: 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    Aqui está um exemplo desse comando executado em AKs, onde o Pod que hospeda o primário é `master-0`:

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    Obtenha o IP do serviço kubernetes criado:

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> Como prática recomendada, você deve limpar excluindo o serviço kubernetes criado acima executando este comando:
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- Adicione um banco de dados ao grupo de disponibilidade.

    Para que o banco de dados seja adicionado ao AG, ele precisa ser executado no modo de recuperação completa e um backup de log deve ser feito. Use o IP do serviço kubernetes criado acima e conecte-se à instância de SQL Server, em seguida, execute as instruções TSQL, conforme mostrado abaixo.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    O exemplo a seguir adiciona um banco `sales` de dados chamado que foi restaurado na instância:

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>Limitações conhecidas

Estes são os problemas conhecidos e as limitações com grupos de disponibilidade para SQL Server mestre no cluster Big Data:

- Os bancos de dados criados como resultado de fluxos de trabalho `CREATE DATABASE` diferentes `RESTORE`de `CREATE DATABASE FROM SNAPSHOT` like não são adicionados automaticamente ao grupo de disponibilidade. [Conecte-se à instância](#instance-connect) e adicione o banco de dados ao grupo de disponibilidade manualmente.
- Determinadas operações, como a `sp_configure` execução de definições de configuração do servidor, exigem uma conexão com a instância mestra. Você não pode usar o ponto de extremidade primário correspondente. Siga [as instruções](#instance-connect) para se conectar à instância de SQL Server e `sp_configure`executar.
- A configuração de alta disponibilidade deve ser criada quando o BDC é implantado. Não é possível habilitar a configuração de alta disponibilidade com grupos de disponibilidade após a implantação.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações sobre como usar arquivos de configuração no Big data implantações de cluster, consulte [como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em kubernetes](deployment-guidance.md#configfile).
- Para obter mais informações sobre o recurso de grupos de disponibilidade para SQL Server, consulte [visão geral de Always on grupos de disponibilidade (SQL Server)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017).
