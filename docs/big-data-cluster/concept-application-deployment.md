---
title: O que é a implantação de aplicativo?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve a implantação de aplicativos em um cluster de big data do SQL Server 2019 (visualização).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7e103acdcfd11b3693e6b1ba343258ee00c16572
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729188"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>O que é a implantação de aplicativos em um cluster de big data do SQL Server 2019?

Implantação de aplicativo permite a implantação de aplicativos no cluster de big data, fornecendo interfaces para criar, gerenciar e executar aplicativos. Aplicativos implantados no cluster de big data se beneficiar do poder computacional do cluster e podem acessar os dados que está disponíveis no cluster. Isso aumenta a escalabilidade e desempenho de aplicativos, ao gerenciar os aplicativos onde os dados residem.
As seções a seguir descrevem a arquitetura e a funcionalidade de implantação de aplicativo.

## <a name="application-deployment-architecture"></a>Arquitetura de implantação do aplicativo

Implantação de aplicativo consiste em um controlador e manipuladores de tempo de execução do aplicativo. Ao criar um aplicativo, um arquivo de especificação (`spec.yaml`) é fornecido. Isso `spec.yaml` arquivo contém tudo o que o controlador precisa saber para implantar o aplicativo com êxito. A seguir está um exemplo do conteúdo para `spec.yaml`:

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

Inspeciona o controlador a `runtime` especificado no `spec.yaml` de arquivo e chama o manipulador de tempo de execução correspondente. O manipulador de tempo de execução cria o aplicativo. Primeiro, um Kubernetes ReplicaSet é criado que contém um ou mais pods, cada uma delas contém o aplicativo a ser implantado. O número de pods é definido pela `replicas` parâmetro definido `spec.yaml` arquivo para o aplicativo. Cada pod pode ter um dos mais pools. O número de pools é definido pela `poolsize` parâmetro definido `spec.yaml` arquivo.

Essas configurações têm um impacto na quantidade de solicitações para que a implantação pode manipular em paralelo. O número máximo de solicitações em um determinado momento é igual a `replicas` vezes `poolsize`. Se você tiver 5 réplicas e 2 pools por réplica a implantação pode lidar com 10 solicitações em paralelo. Consulte a imagem abaixo, para uma representação gráfica dos `replicas` e `poolsize`:

![Tamanho_do_pool e réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Depois ReplicaSet tiver sido criado e os pods tem iniciado, um trabalho de cron é criado se um `schedule` foi definido no `spec.yaml` arquivo. Por fim, um Kubernetes Service é criado, o que pode ser usado para gerenciar e executar o aplicativo (veja abaixo).

Quando um aplicativo é executado, o serviço de Kubernetes para os proxies de aplicativo, as solicitações para uma réplica e retorna os resultados.

## <a name="how-to-work-with-application-deployment"></a>Como trabalhar com a implantação de aplicativos

As duas interfaces principais para implantação de aplicativo são: 
- [Interface de linha de comando `mssqlctl`](big-data-cluster-create-apps.md)
- [Extensão do Visual Studio Code e o estúdio de dados do Azure](app-deployment-extension.md)

Também é possível que um aplicativo a ser executada usando um serviço web RESTful. Para obter mais informações, consulte [consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como criar e executar aplicativos em clusters de grandes dados do SQL Server, consulte o seguinte:

- [Implantar aplicativos usando mssqlctl](big-data-cluster-create-apps.md)
- [Implantar aplicativos usando a extensão de implantar o aplicativo](app-deployment-extension.md)
- [Consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md)

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
