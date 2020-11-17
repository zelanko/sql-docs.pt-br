---
title: Implantar o cluster de Big Data do SQL Server com alta disponibilidade
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: Saiba como implantar o cluster de Big Data do SQL Server com alta disponibilidade.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 09/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 08645672c1aa8b7b980b4ffe86b4029a691fa1cf
ms.sourcegitcommit: 275fd02d60d26f4e66f6fc45a1638c2e7cedede7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94447102"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>Implantar o cluster de Big Data do SQL Server com alta disponibilidade

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Como Clusters de Big Data do SQL Server estão no Kubernetes como aplicativos em contêineres e usam recursos como conjuntos com estado e armazenamento persistente, essa infraestrutura tem monitoramento de integridade, detecção de falha e mecanismos de failover internos que os componentes do cluster utilizam para manter a integridade do serviço. Para proporcionar maior confiabilidade, você também pode configurar a instância mestra do SQL Server e/ou o nó de nome do HDFS e serviços compartilhados do Spark para implantar com réplicas adicionais em uma configuração de alta disponibilidade. O monitoramento, a detecção de falha e o failover automático são gerenciados pelo serviço de gerenciamento de cluster de Big Data, ou seja, o serviço de controle. Esse serviço é fornecido sem a intervenção do usuário – tudo, desde a configuração do grupo de disponibilidade e da configuração dos pontos de extremidade de espelhamento de banco de dados, à adição do bancos de dados ao grupo de disponibilidade ou à coordenação de failover e atualização. 

A imagem a seguir representa como um grupo de disponibilidade é implantado em um Cluster de Big Data do SQL Server:

:::image type="content" source="media/deployment-high-availability/contained-ag.png" alt-text="high-availability-ag-bdc":::

Aqui estão alguns dos recursos que os grupos de disponibilidade habilitam:

- Se as configurações de alta disponibilidade forem especificadas no arquivo de configuração de implantação, será criado um único grupo de disponibilidade chamado `containedag`. Por padrão, `containedag` tem três réplicas, incluindo a primária. Todas as operações CRUD para o grupo de disponibilidade são gerenciadas internamente, incluindo a criação do grupo de disponibilidade ou a adição de réplicas ao grupo de disponibilidade criado. Não é possível criar grupos de disponibilidade adicionais na instância mestra do SQL Server em um cluster de Big Data.
- Todos os bancos de dados são adicionados automaticamente ao grupo de disponibilidade, incluindo todos os bancos de dados do usuário e do sistema, como `master` e `msdb`. Essa funcionalidade fornece um modo de exibição do sistema único entre as réplicas do grupo de disponibilidade. Bancos de dados de modelo adicionais (`model_replicatedmaster` e `model_msdb`) são usadas para propagar a parte replicada dos bancos de dados do sistema. Além desses bancos de dados, você verá bancos de dados `containedag_master` e `containedag_msdb` caso conecte-se diretamente à instância. Os bancos de dados do `containedag` representam o `master` e o `msdb` dentro do grupo de disponibilidade.

  > [!IMPORTANT]
  > Os bancos de dados criados na instância como resultado de outros fluxos de trabalho, como anexar banco de dados, não são adicionados automaticamente ao grupo de disponibilidade, e o administrador de cluster de Big Data precisaria fazer isso manualmente. Confira a seção [Conectar à instância do SQL Server](#instance-connect) para obter instruções sobre como habilitar um ponto de extremidade temporário no banco de dados mestre de instância SQL Server. Antes da versão do SQL Server 2019 CU2, os bancos de dados criados como resultado de uma instrução RESTORE tinham o mesmo comportamento e exigiam a adição manual dos bancos de dados ao grupo de disponibilidade contido.
  >
- Bancos de dados de configuração do polybase não são incluídos no grupo de disponibilidade porque eles incluem metadados em nível de instância específicos de cada réplica.
- Um ponto de extremidade externo é provisionado automaticamente para conectar-se a bancos de dados dentro do grupo de disponibilidade. Esse ponto de extremidade `master-svc-external` desempenha a função do ouvinte do grupo de disponibilidade.
- Um segundo ponto de extremidade externo é provisionado para conexões somente leitura para as réplicas secundárias para escalar horizontalmente as cargas de trabalho de leitura.

## <a name="deploy"></a>Implantar

Para implantar o SQL Server mestre em um grupo de disponibilidade:

1. Habilitar o recurso `hadr`
1. Especifique o número de réplicas para o AG (o mínimo são 3)
1. Configurar os detalhes do segundo ponto de extremidade externo criado para conexões com as réplicas secundárias somente leitura

Você pode usar o `aks-dev-test-ha` ou os perfis de configuração internos do `kubeadm-prod` para iniciar a personalização do cluster de Big Data. Esses perfis incluem as configurações necessárias para os recursos que você pode definir para alta disponibilidade adicional. Por exemplo, abaixo está uma seção no arquivo de configuração `bdc.json` relevante para habilitar grupos de disponibilidade para a instância mestra do SQL Server.  

```json
{
  ...
    "spec": {
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
  ...
}
```

As etapas a seguir explicam um exemplo de como iniciar do perfil do `aks-dev-test-ha` e personalizar sua configuração de implantação de cluster de Big Data. Para uma implantação em um cluster de `kubeadm`, etapas semelhantes seriam aplicáveis, mas verifique se você está usando `NodePort` para o `serviceType` na seção `endpoints`.

1. Clonar seu perfil de destino

    ```bash
    azdata bdc config init --source aks-dev-test-ha --target custom-aks-ha
    ```

1. Opcionalmente, faça as edições no perfil personalizado conforme necessário. 
1. Comece a implantação do cluster usando o perfil de configuração de cluster criado acima

    ```bash
    azdata bdc create --config-profile custom-aks-ha --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases-in-the-availability-group"></a>Conectar-se a bancos de dados do SQL Server no grupo de disponibilidade

Dependendo do tipo de carga de trabalho que você deseja executar no SQL Server mestre, você pode se conectar à primária para cargas de trabalho de leitura/gravação ou aos bancos de dados nas réplicas secundárias para o tipo somente leitura de cargas de trabalho. Aqui está uma estrutura de tópicos para cada tipo de conexão:

### <a name="connect-to-databases-on-the-primary-replica"></a>Conectar-se a bancos de dados na réplica primária

Para conexões com a réplica primária, use o ponto de extremidade `sql-server-master`. Esse ponto de extremidade também é o ouvinte para o AG. Ao usar esse ponto de extremidade, todas as conexões estão no contexto de bancos de dados dentro do grupo de disponibilidade. Por exemplo, uma conexão padrão usando esse ponto de extremidade resultará na conexão com o banco de dados `master` dentro do grupo de disponibilidade, não no banco de dados `master` da instância do SQL Server. Execute este comando para localizar o ponto de extremidade:

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

```
Description                           Endpoint             Name               Protocol
------------------------------------  -------------------  -----------------  ----------
SQL Server Master Instance Front-End  11.11.111.111,11111  sql-server-master  tds
```

> [!NOTE]
> Eventos de failover podem ocorrer durante uma execução de consulta distribuída que está acessando dados de fontes de dados remotas, como o HDFS ou o pool de dados. Como prática recomendada, os aplicativos devem ser projetados para ter lógica de repetição de conexão em caso de desconexões causadas por failover.  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>Conectar-se a bancos de dados nas réplicas secundárias

Para conexões somente leitura para bancos de dados em réplicas secundárias, use o ponto de extremidade `sql-server-master-readonly`. Esse ponto de extremidade funciona como um balanceador de carga em todas as réplicas secundárias.  Ao usar esse ponto de extremidade, todas as conexões estão no contexto de bancos de dados dentro do grupo de disponibilidade. Por exemplo, uma conexão padrão usando esse ponto de extremidade resultará na conexão com o banco de dados `master` dentro do grupo de disponibilidade, não no banco de dados `master` da instância do SQL Server. 

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

```
Description                                    Endpoint            Name                        Protocol
---------------------------------------------  ------------------  --------------------------  ----------
SQL Server Master Readable Secondary Replicas  11.11.111.11,11111  sql-server-master-readonly  tds
```

## <a name="connect-to-sql-server-instance"></a><a id="instance-connect"></a> Conectar a uma instância do SQL Server

Para determinadas operações, como definir configurações em nível de servidor ou adicionar manualmente um banco de dados ao grupo de disponibilidade, você deve se conectar à instância do SQL Server. Antes do SQL Server 2019 CU2, operações como `sp_configure`, `RESTORE DATABASE` ou qualquer DDL do grupo de disponibilidade exigirão esse tipo de conexão. Por padrão, o cluster de Big Data não inclui um ponto de extremidade que habilita a conexão de instância e você deve expor esse ponto de extremidade manualmente. 

> [!IMPORTANT]
> O ponto de extremidade exposto para conexões da instância do SQL Server tem suporte apenas para autenticação SQL, mesmo em clusters em que o Active Directory está habilitado. Por padrão, durante uma implantação de cluster de Big Data, o logon do `sa` é desabilitado e um novo logon do `sysadmin` é provisionado com base nos valores fornecidos no momento da implantação para as variáveis de ambiente `AZDATA_USERNAME` e `AZDATA_PASSWORD`.

> [!IMPORTANT]
> A DDL do grupo de disponibilidade contido é exclusivamente autogerenciada no BDC. Qualquer tentativa (de usuário externo) de descartar a disponibilidade contida ou o ponto de extremidade de espelhamento de banco de dados não tem suporte e pode resultar em um estado de BDC irrecuperável.

Aqui está um exemplo que mostra como expor esse ponto de extremidade e então adicionar o banco de dados criado com um fluxo de trabalho de restauração ao grupo de disponibilidade. Instruções semelhantes para configurar uma conexão com a instância mestra do SQL Server aplicam-se quando você deseja alterar as configurações de servidor com `sp_configure`.

> [!NOTE]
> Do SQL Server 2019 CU2 em diante os bancos de dados criados como resultado de um fluxo de trabalho de restauração são adicionados automaticamente ao grupo de disponibilidade contido.

- Determine o pod que hospeda a réplica primária conectando-se ao ponto de extremidade `sql-server-master` e execute:

    ```sql
    SELECT @@SERVERNAME
   ```

- Expor o ponto de extremidade externo criando um novo serviço do Kubernetes

    Para um cluster do `kubeadm`, execute o comando abaixo. Substitua `podName` pelo nome do servidor retornado na etapa anterior, `serviceName` pelo nome preferencial para o serviço de Kubernetes criado e `namespaceName`* pelo nome do cluster do BDC.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    Para uma execução de cluster do AKS, execute o mesmo comando, exceto que o tipo de serviço criado será `LoadBalancer`. Por exemplo: 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    Aqui está um exemplo desse comando executado no AKS, em que o pod que hospeda o primário é `master-0`:

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    Obtenha o IP do serviço de Kubernetes criado:

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> Como melhor prática, limpe excluindo o serviço de Kubernetes criado acima executando este comando:
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- Adicione um banco de dados ao grupo de disponibilidade.

    Para que o banco de dados seja adicionado ao AG, ele precisa ser executado no modo de recuperação completa e deve ser feito um backup do log. Use o IP do serviço Kubernetes criado acima e conecte-se à instância de SQL Server, então execute as instruções TSQL conforme mostrado abaixo.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    O exemplo a seguir adiciona um banco de dados chamado `sales` que foi restaurado na instância:

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>Limitações conhecidas

Esses são problemas e limitações conhecidos de grupos de disponibilidade contidos para o SQL Server mestre no cluster de Big Data:

- A configuração de alta disponibilidade deve ser criada quando o cluster de Big Data é implantado. Não é possível habilitar a configuração de alta disponibilidade com grupos de disponibilidade após a implantação. Neste momento, a única configuração habilitada é para réplicas de confirmação síncrona.

> [!WARNING]
> A atualização do modo de sincronização para confirmação assíncrona em qualquer uma das réplicas na confirmação de quorum resultará em uma configuração inválida para alta disponibilidade. A execução nessa configuração envolve um risco de perda de dados, pois, no caso de eventos de falha que afetem a réplica primária, não há um failover automático disparado e o usuário deve aceitar o risco de perda de dados ao emitir o failover manual.

- Para restaurar com êxito um banco de dados habilitado para TDE de um backup criado em outro servidor, você deve garantir que os [certificados necessários](../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md) sejam restaurados no mestre de instância do SQL Server, bem como no mestre AG contido. Confira [aqui](https://www.sqlshack.com/restoring-transparent-data-encryption-tde-enabled-databases-on-a-different-server/) para obter um exemplo de como fazer backup e restaurar os certificados.
- Determinadas operações, como a execução de definições de configuração do servidor com `sp_configure`, exigem uma conexão com o banco de dados `master` de instância do SQL Server, não com o grupo de disponibilidade `master`. Você não pode usar o ponto de extremidade primário correspondente. Siga [as instruções](#instance-connect) para expor um ponto de extremidade e conectar-se à instância do SQL Server e executar `sp_configure`. Você só pode usar a autenticação do SQL ao expor manualmente o ponto de extremidade para conectar-se ao banco de dados `master` da instância do SQL Server.
- Embora o banco de dados msdb contido esteja incluído no grupo de disponibilidade e os trabalhos do SQL Agent sejam replicados nele, os trabalhos são executados apenas por agendamento na réplica primária.
- Não há suporte para o recurso de replicação em grupos de disponibilidade contidos. As instâncias do SQL Server que fazem parte de um AG contido não podem funcionar como distribuidor ou editor, seja no nível de instância ou no AG contido.
- Não há suporte para criar grupos de arquivo ao criar o banco de dados. Como alternativa, você pode criar o banco de dados primeiro e emitir uma instrução ALTER DATABASE para adicionar qualquer grupo de arquivo.
- Antes do SQL Server 2019 CU2, os bancos de dados criados como resultado de fluxos de trabalho que não `CREATE DATABASE` e `RESTORE DATABASE` como `CREATE DATABASE FROM SNAPSHOT` não são adicionados automaticamente ao grupo de disponibilidade. [Conecte-se à instância](#instance-connect) e adicione o banco de dados ao grupo de disponibilidade manualmente.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações sobre o uso de arquivos de configuração em implantações de cluster de Big Data, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile).
- Para obter mais informações sobre o recurso de grupos de disponibilidade para SQL Server, confira [Visão geral de grupos de disponibilidade Always On (SQL Server)](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
