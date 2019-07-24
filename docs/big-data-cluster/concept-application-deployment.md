---
title: O que é a implantação de aplicativos?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve a implantação de aplicativos em um cluster SQL Server 2019 Big Data (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419410"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>O que é a implantação de aplicativos em um cluster SQL Server 2019 Big Data?

A implantação de aplicativos permite a implantação de aplicativos no cluster Big Data fornecendo interfaces para criar, gerenciar e executar aplicativos. Os aplicativos implantados no cluster de Big Data se beneficiam do poder computacional do cluster e podem acessar os dados que estão disponíveis no cluster. Isso aumenta a escalabilidade e o desempenho dos aplicativos, ao mesmo tempo em que gerencia os aplicativos nos quais os dados residem.
As seções a seguir descrevem a arquitetura e a funcionalidade da implantação do aplicativo.

## <a name="application-deployment-architecture"></a>Arquitetura de implantação de aplicativos

A implantação de aplicativos consiste em um controlador e manipuladores de tempo de execução de aplicativo. Ao criar um aplicativo, um arquivo de especificação`spec.yaml`() é fornecido. Esse `spec.yaml` arquivo contém tudo o que o controlador precisa saber para implantar o aplicativo com êxito. Veja a seguir um exemplo de conteúdo para `spec.yaml`:

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

O controlador inspeciona o `runtime` especificado `spec.yaml` no arquivo e chama o manipulador de tempo de execução correspondente. O manipulador de tempo de execução cria o aplicativo. Primeiro, um kubernetes Réplicaset é criado contendo um ou mais pods, cada um contendo o aplicativo a ser implantado. O número de pods é definido pelo `replicas` parâmetro definido `spec.yaml` no arquivo para o aplicativo. Cada pod pode ter um ou mais pools. O número de pools é definido pelo `poolsize` parâmetro definido `spec.yaml` no arquivo.

Essas configurações têm um impacto na quantidade de solicitações que a implantação pode manipular em paralelo. O número máximo de solicitações em um determinado momento é igual a `replicas` Times `poolsize`. Se você tiver 5 réplicas e 2 pools por réplica, a implantação poderá lidar com 10 solicitações em paralelo. Consulte a imagem abaixo para obter uma representação gráfica `replicas` de `poolsize`e:

![Pools e réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Depois que o conjunto de réplicas tiver sido criado e os pods tiverem começado, um trabalho cron será `schedule` criado se um tiver `spec.yaml` sido definido no arquivo. Por fim, um serviço kubernetes é criado e pode ser usado para gerenciar e executar o aplicativo (veja abaixo).

Quando um aplicativo é executado, o serviço kubernetes para o aplicativo executa as solicitações para uma réplica e retorna os resultados.

## <a name="how-to-work-with-application-deployment"></a>Como trabalhar com a implantação de aplicativos

As duas interfaces principais para a implantação de aplicativos são: 
- [Interface de linha de comando`azdata`](big-data-cluster-create-apps.md)
- [Extensão de Visual Studio Code e Azure Data Studio](app-deployment-extension.md)

Também é possível que um aplicativo seja executado usando um serviço Web RESTful. Para obter mais informações, consulte [consumir aplicativos em clusters de Big data](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como criar e executar aplicativos em clusters SQL Server Big Data, consulte o seguinte:

- [Implantar aplicativos usando o azdata](big-data-cluster-create-apps.md)
- [Implantar aplicativos usando a extensão de implantação de aplicativo](app-deployment-extension.md)
- [Consumir aplicativos em clusters Big Data](big-data-cluster-consume-apps.md)

Para saber mais sobre os clusters de Big Data SQL Server, consulte a seguinte visão geral:

- [O que são SQL Server clusters de Big Data 2019?](big-data-cluster-overview.md)
