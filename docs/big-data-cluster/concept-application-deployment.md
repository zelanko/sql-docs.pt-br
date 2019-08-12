---
title: O que é a Implantação de Aplicativos?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve a implantação de aplicativos em um cluster de Big Data do SQL Server 2019 (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419410"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>O que é a Implantação de Aplicativos em um cluster de Big Data do SQL Server 2019?

A Implantação de Aplicativos permite a implantação de aplicativos no cluster de Big Data fornecendo interfaces para criar, gerenciar e executar aplicativos. Os aplicativos implantados no cluster de Big Data se beneficiam do poder computacional do cluster e podem acessar os dados disponíveis no cluster. Isso aumenta a escalabilidade e o desempenho dos aplicativos, ao mesmo tempo que gerencia os aplicativos nos quais os dados residem.
As seções a seguir descrevem a arquitetura e a funcionalidade da Implantação de Aplicativos.

## <a name="application-deployment-architecture"></a>Arquitetura da Implantação de Aplicativos

A implantação de aplicativos consiste em um controlador e manipuladores de tempo de execução de aplicativo. Ao criar um aplicativo, um arquivo de especificação (`spec.yaml`) é fornecido. Esse arquivo `spec.yaml` contém tudo o que o controlador precisa saber para implantar o aplicativo com êxito. Este é um exemplo de conteúdo para `spec.yaml`:

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

O controlador inspeciona o `runtime` especificado no arquivo `spec.yaml` e chama o manipulador de tempo de execução correspondente. O manipulador de tempo de execução cria o aplicativo. Primeiro, um ReplicaSet do Kubernetes é criado contendo um ou mais pods, cada um contendo o aplicativo a ser implantado. O número de pods é definido pelo parâmetro `replicas` definido no arquivo `spec.yaml` do aplicativo. Cada pod pode ter um ou mais pools. O número de pools é definido pelo parâmetro `poolsize` definido no arquivo `spec.yaml`.

Essas configurações têm um impacto na quantidade de solicitações que a implantação pode manipular em paralelo. O número máximo de solicitações em determinado momento é igual a `replicas` vezes `poolsize`. Se você tiver cinco réplicas e dois pools por réplica, a implantação poderá manipular dez solicitações em paralelo. Confira a imagem abaixo para obter uma representação gráfica de `replicas` e `poolsize`:

![Tamanho do pool e réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Depois que o ReplicaSet for criado e os pods forem iniciados, um trabalho do Cron será criado se um `schedule` tiver sido definido no arquivo `spec.yaml`. Por fim, um serviço de Kubernetes é criado e pode ser usado para gerenciar e executar o aplicativo (veja abaixo).

Quando um aplicativo é executado, o Serviço de Kubernetes do aplicativo executa as solicitações como proxy para uma réplica e retorna os resultados.

## <a name="how-to-work-with-application-deployment"></a>Como trabalhar com a Implantação de Aplicativos

As duas interfaces principais da Implantação de Aplicativos são: 
- [Interface de linha de comando `azdata`](big-data-cluster-create-apps.md)
- [Extensão do Azure Data Studio e Visual Studio Code](app-deployment-extension.md)

Também é possível executar um aplicativo usando um serviço Web RESTful. Para obter mais informações, confira [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como criar e executar aplicativos em clusters de Big Data do SQL Server, confira o seguinte:

- [Implantar aplicativos usando o azdata](big-data-cluster-create-apps.md)
- [Implantar aplicativos usando a extensão Implantação de Aplicativos](app-deployment-extension.md)
- [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md)

Para saber mais sobre os clusters de Big Data do SQL Server, confira a seguinte visão geral:

- [O que são os clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md)
