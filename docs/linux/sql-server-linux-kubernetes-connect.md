---
title: Conectar-se ao SQL Server sempre no grupo de disponibilidade no cluster do Kubernetes
description: Este artigo explica como se conectar a um grupo de disponibilidade AlwaysOn
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7fcad17522f4372e696a26a99d4ce1a4af92ea15
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356097"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Conectar-se a um SQL Server sempre no grupo de disponibilidade no Kubernetes

Para se conectar às instâncias do SQL Server em contêineres em um cluster Kubernetes, crie uma [serviço de Balanceador de carga](http://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). O balanceador de carga é um ponto de extremidade. Ele contém um endereço IP e encaminha as solicitações para o endereço IP para o pod executando a instância do SQL Server.

Para se conectar a uma réplica do grupo de disponibilidade, crie um serviço para tipos diferentes de réplica. Você pode ver exemplos de serviços para diferentes tipos de réplicas em [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` aponta para a réplica primária.
* `ag1-secondary` aponta para qualquer réplica secundária.

Se mais de uma réplica secundária, Kubernetes roteia a conexão para as diferentes réplicas em um estilo round-robin.

## <a name="create-a-load-balancer-service"></a>Criar um serviço de Balanceador de carga

Para criar serviços de Balanceador de carga para o primário e as réplicas, copie [ `ag1-services.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) partir [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) e atualizá-lo para seu grupo de disponibilidade.

O comando a seguir aplica-se a configuração do `.yaml` arquivo em cluster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Obtenha o endereço IP para seu serviço de Balanceador de carga

Para obter o endereço IP do balanceador de carga para seu serviço de Balanceador de carga, execute

```kubectl
kubectl get services
```

Identificar o endereço IP do serviço que você deseja se conectar.

## <a name="connect-to-primary-replica"></a>Conectar-se à réplica primária

Para se conectar à réplica primária com a autenticação do SQL, use o `sa` conta, o valor de `sapassword` do segredo que você criou e esse endereço IP.

Por exemplo:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Próximas etapas

[Gerenciar grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
