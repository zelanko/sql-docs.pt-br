---
title: Serviços de Machine Learning (Python, R)
titleSuffix: SQL Server Big Data Clusters
description: Saiba como executar scripts do Python e do R na instância mestra de Clusters de Big Data do SQL Server com Serviços de Machine Learning.
author: dphansen
ms.author: davidph
ms.date: 04/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: a14258c15ac1af1445b201f7b999dbec1682555d
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196908"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>Executar scripts do Python e do R com Serviços de Machine Learning em Clusters de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Você pode executar scripts do Python e do R na instância mestra de [Clusters de Big Data do SQL Server](big-data-cluster-overview.md) com [Serviços de Machine Learning](../machine-learning/index.yml).

> [!NOTE]
> Você também pode executar o código Java na instância mestra com as [Extensões de Linguagem do SQL Server](../language-extensions/language-extensions-overview.md). A conclusão das etapas abaixo habilitará também as Extensões de Linguagem.

## <a name="enable-machine-learning-services"></a>Habilitar Serviços de Machine Learning

O Serviços de Machine Learning são instalados por padrão em Clusters de Big Data e não exigem instalação separada.

Para habilitar Serviços de Machine Learning, execute esta instrução na instância mestra:

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

Agora você está pronto para executar scripts do Python e do R na instância mestra de Clusters de Big Data. Confira os guias de início rápido nas [Próximas etapas](#next-steps) para executar seu primeiro script.

>[!NOTE]
>A definição de configuração não pode ser definida em uma conexão de ouvinte do grupo de disponibilidade. Se os Clusters de Big Data forem implantados com alta disponibilidade, então defina `external scripts enabled` em cada réplica. Confira [Habilitar o cluster com alta disponibilidade](#enable-on-cluster-with-high-availability).

## <a name="enable-on-cluster-with-high-availability"></a>Habilitar o cluster com alta disponibilidade

Quando você [Implanta o Cluster de Big Data do SQL Server com alta disponibilidade](deployment-high-availability.md), a implantação cria um grupo de disponibilidade para a instância mestra. Para habilitar os Serviços de Machine Learning, defina `external scripts enabled` em cada instância do grupo de disponibilidade. Para um Cluster de Big data, você precisa executar `sp_configure` em cada réplica da instância mestra do SQL Server

A seção a seguir descreve como habilitar scripts externos em cada instância.

### <a name="create-an-external-load-balancer-for-each-instance"></a>Criar um balanceador de carga externo para cada instância

Para cada réplica no grupo de disponibilidade, crie um balanceador de carga para permitir que você se conecte à instância. 

`kubectl expose pod <pod-name> --port=<connection port number> --name=<load-balancer-name> --type=LoadBalancer -n <kubernetes namespace>`

Os exemplos neste artigo usam os seguintes valores:

- `<pod-name>`: `master-#`
- `<connection port number>`: `1533`
- `<load-balancer-name>`: `mymaster-#`
- `<kubernetes namespace>`: `mssql-cluster`

Atualize o seguinte script para o seu ambiente e execute os comandos:

```bash
kubectl expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer -n mssql-cluster 
kubectl expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer -n mssql-cluster
kubectl expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer -n mssql-cluster 
```

`kubectl` retorna a seguinte saída.

```bash
service/mymaster-0 exposed
service/mymaster-1 exposed
service/mymaster-2 exposed
```

Cada balanceador de carga é um ponto de extremidade de réplica mestre.

### <a name="enable-script-execution-on-each-replica"></a>Habilitar a execução de script em cada réplica

1. Obtenha o endereço IP do ponto de extremidade da réplica mestre.

   O comando a seguir retorna o endereço IP externo do ponto de extremidade da réplica. 

   `kubectl get services <load-balancer-name> -n <kubernetes namespace>`

   Para obter o endereço IP externo para cada réplica neste cenário, execute os seguintes comandos:

   ```bash
   kubectl get services mymaster-0 -n mssql-cluster
   kubectl get services mymaster-1 -n mssql-cluster
   kubectl get services mymaster-2 -n mssql-cluster
   ```

   >[!NOTE]
   > Pode levar algum tempo para que o endereço IP externo esteja disponível. Execute o script anterior periodicamente até que cada ponto de extremidade retorne um endereço IP externo.

1. Conecte-se ao ponto de extremidade de réplica mestre e habilite a execução de script.

    Execute esta instrução:

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

   Por exemplo, você pode executar o comando anterior com `sqlcmd`. O exemplo a seguir conecta-se ao ponto de extremidade da réplica mestre e habilita a execução do script. Atualize os valores no script para seu ambiente.

   ```bash
   sqlcmd -S <IP address>,1533 -U <user name> -P <password> -Q "EXEC sp_configure 'external scripts enabled', 1; RECONFIGURE WITH OVERRIDE;"
   ```

   Repita a etapa para cada réplica.

### <a name="demonstration"></a>Demonstração

A imagem a seguir demonstra esse processo.

[![Demonstração](media/machine-learning-services/example-kube-enable-scripts.png "Demonstrar o recurso de habilitação no Kubernetes")](media/machine-learning-services/example-kube-enable-scripts.png#lightbox)

Agora você está pronto para executar scripts do Python e do R na instância mestra de Clusters de Big Data. Confira os guias de início rápido nas [Próximas etapas](#next-steps) para executar seu primeiro script.

### <a name="delete-the-master-replica-endpoints"></a>Excluir os pontos de extremidade de réplica mestre

No cluster do Kubernetes, exclua o ponto de extremidade de cada réplica. O ponto de extremidade é exposto no Kubernetes como um serviço de balanceamento de carga.

O comando a seguir exclui o serviço de balanceamento de carga.

`kubectl delete svc <load-balancer-name> -n mssql-cluster`

Para os exemplos neste artigo, execute os seguintes comandos.

```bash
kubectl delete svc mymaster-0 -n mssql-cluster
kubectl delete svc mymaster-1 -n mssql-cluster
kubectl delete svc mymaster-2 -n mssql-cluster
```

## <a name="next-steps"></a>Próximas etapas

+ [Executar scripts simples do Python](../machine-learning/tutorials/quickstart-python-create-script.md?toc=/sql/toc.json)
+ [Treinar e pontuar um modelo preditivo no Python](../machine-learning/tutorials/quickstart-python-train-score-model.md?toc=/sql/toc.json)
+ [Executar scripts simples do R](../machine-learning/tutorials/quickstart-r-create-script.md?toc=/sql/toc.json)
+ [Treinar e pontuar um modelo preditivo no R](../machine-learning/tutorials/quickstart-r-train-score-model.md?toc=/sql/toc.json)
