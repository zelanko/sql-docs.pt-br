---
title: Conectar-se ao grupo de disponibilidade Always On do SQL Server no cluster do Kubernetes
description: Este artigo explica como conectar-se a um Grupo de Disponibilidade Always On
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952600"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Conectar-se a um grupo de disponibilidade Always On do SQL Server no Kubernetes

Para conectar-se a instâncias do SQL Server em contêineres em um cluster do Kubernetes, crie um [serviço de balanceador de carga](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). O balanceador de carga é um ponto de extremidade. Ele contém um endereço IP e encaminha as solicitações do endereço IP para o pod que executa a instância do SQL Server.

Para se conectar a uma réplica do grupo de disponibilidade, crie um serviço para diferentes tipos de réplica. É possível ver exemplos de serviços para diferentes tipos de réplicas em [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` aponta para a réplica primária.
* `ag1-secondary` aponta para a réplica secundária.

Se houver mais de uma réplica secundária, o Kubernetes roteará a conexão para as diferentes réplicas de modo Round Robin.

## <a name="create-a-load-balancer-service"></a>Criar um serviço de balanceador de carga

Para criar serviços de balanceador de carga para a réplica primária, copie [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) e atualize-o para seu grupo de disponibilidade.

O comando a seguir aplica a configuração do arquivo `.yaml` ao cluster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Obter o endereço IP para seu serviço de balanceador de carga

Para obter o endereço IP do balanceador de carga para seu serviço de balanceador de carga, execute

```kubectl
kubectl get services
```

Identifique o endereço IP do serviço ao qual você deseja se conectar.

## <a name="connect-to-primary-replica"></a>Conectar-se à réplica primária

Para conectar-se à réplica primária com a autenticação do SQL, use a conta `sa`, o valor de `sapassword` do segredo criado e esse endereço IP.

Por exemplo:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Próximas etapas

[Gerenciar grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
