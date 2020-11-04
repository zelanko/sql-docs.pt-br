---
title: O que é a implantação de aplicativos?
titleSuffix: SQL Server Big Data Clusters
description: Saiba como a implantação de aplicativo fornece interfaces para criar, gerenciar e executar aplicativos em um cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ac26973c4d1ff8b2a9e689f3aa372d3888f939d6
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914289"
---
# <a name="what-is-application-deployment-on-a-sql-server-big-data-cluster"></a>O que é a implantação de aplicativos em um cluster de Big Data do SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

A implantação de aplicativos permite que esse tipo de implantação ocorra no cluster de Big Data do SQL Server, fornecendo interfaces para criar, gerenciar e executar aplicativos. Os aplicativos implantados no cluster de Big Data do SQL Server se beneficiam do poder computacional do cluster e podem acessar os dados disponíveis nele. Isso aumenta a escalabilidade e o desempenho dos aplicativos, ao mesmo tempo que gerencia os aplicativos nos quais os dados residem. Os runtimes de aplicativos compatíveis com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] são o R, Python, SSIS e MLeap.

As seções a seguir descrevem a arquitetura e a funcionalidade da implantação de aplicativos.

## <a name="application-deployment-architecture"></a>Arquitetura da implantação de aplicativos

A implantação de aplicativos consiste em um controlador e manipuladores de runtime de aplicativo. Ao criar um aplicativo, um arquivo de especificação (`spec.yaml`) é fornecido. Esse arquivo `spec.yaml` contém tudo o que o controlador precisa saber para implantar o aplicativo com êxito. Este é um exemplo de conteúdo para `spec.yaml`:

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

O controlador inspeciona o `runtime` especificado no arquivo `spec.yaml` e chama o manipulador de runtime correspondente. O manipulador de runtime cria o aplicativo. Primeiro, um ReplicaSet do Kubernetes é criado contendo um ou mais pods, cada um contendo o aplicativo a ser implantado. O número de pods é definido pelo parâmetro `replicas` definido no arquivo `spec.yaml` do aplicativo. Cada pod pode ter um ou mais pools. O número de pools é definido pelo parâmetro `poolsize` definido no arquivo `spec.yaml`.

Essas configurações têm um impacto na quantidade de solicitações que a implantação pode manipular em paralelo. O número máximo de solicitações em determinado momento é igual a `replicas` vezes `poolsize`. Se você tiver cinco réplicas e dois pools por réplica, a implantação poderá manipular dez solicitações em paralelo. Confira a imagem abaixo para obter uma representação gráfica de `replicas` e `poolsize`:

![Tamanho do pool e réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Depois que o ReplicaSet for criado e os pods forem iniciados, um trabalho do Cron será criado se um `schedule` tiver sido definido no arquivo `spec.yaml`. Por fim, um serviço de Kubernetes é criado e pode ser usado para gerenciar e executar o aplicativo (veja abaixo).

Quando um aplicativo é executado, o Serviço de Kubernetes do aplicativo executa as solicitações como proxy para uma réplica e retorna os resultados.

## <a name="security-considerations-for-applications-deployments-on-openshift"></a><a id="app-deploy-security"></a> Considerações de segurança para implantações de aplicativos no OpenShift

O SQL Server 2019 CU5 habilita o suporte para a implantação de Clusters de Big Data no Red Hat OpenShift, bem como um modelo de segurança atualizado para o BDC, para que contêineres com privilégios não sejam mais necessários. Além de não privilegiados, os contêineres são executados como um usuário não raiz por padrão em todas as novas implantações usando o SQL Server 2019 CU5.

No momento do lançamento do CU5, a etapa de configuração dos aplicativos implantados com interfaces de [implantação de aplicativo]() ainda será executada como usuário *raiz*. Isso é necessário porque, durante a instalação, são instalados mais pacotes que o aplicativo usará. Outro código de usuário implantado como parte do aplicativo será executado como usuário de baixo privilégio. 

Além disso, a funcionalidade **CAP_AUDIT_WRITE** é uma funcionalidade opcional necessária para permitir o agendamento de aplicativos SSIS que usam trabalhos cron. Quando o arquivo de especificação YAML do aplicativo especifica uma agenda, o aplicativo será disparado por meio de um trabalho cron, que requer a funcionalidade adicional.  Como alternativa, o aplicativo pode ser disparado sob demanda com *azdata app run* por meio de uma chamada do serviço Web, que não requer a funcionalidade CAP_AUDIT_WRITE. 

> [!NOTE]
> O SCC personalizado no [artigo de implantação do OpenShift](deploy-openshift.md) não inclui essa funcionalidade pois ela não é exigida por uma implantação padrão do cluster de Big Data. Para habilitar essa funcionalidade, você precisa primeiro atualizar o arquivo YAML do SCC personalizado para incluir CAP_AUDIT_WRITE no 

```yml
...
allowedCapabilities:
- SETUID
- SETGID
- CHOWN
- SYS_PTRACE
- AUDIT_WRITE
...
```

## <a name="how-to-work-with-application-deployment"></a>Como trabalhar com a Implantação de Aplicativos

As duas interfaces principais da implantação de aplicativos são: 
- [Interface de linha de comando [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](app-create.md)
- [Extensão do Azure Data Studio e Visual Studio Code](app-deployment-extension.md)

Também é possível executar um aplicativo usando um serviço Web RESTful. Para obter mais informações, confira [Consumir aplicativos em clusters de Big Data](app-consume.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como criar e executar aplicativos em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira o seguinte:

- [Implantar aplicativos usando o azdata](app-create.md)
- [Implantar aplicativos usando a extensão Implantação de Aplicativos](app-deployment-extension.md)
- [Consumir aplicativos em clusters de Big Data](app-consume.md)

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira a visão geral a seguir:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)