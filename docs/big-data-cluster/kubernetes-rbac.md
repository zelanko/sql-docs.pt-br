---
title: RBAC do Kubernetes
titleSuffix: SQL Server big data clusters
description: Este artigo descreve como os Clusters de Big Data do SQL Server usam o RBAC com o Kubernetes.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d2e3f379402f16f32020f9cd34103919f13a30c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552971"
---
# <a name="kubernetes-rbac-model--impact-on-users-managing-bdc"></a>O modelo RBAC do Kubernetes e o impacto sobre os usuários que gerenciam o BDC

A seção a seguir descreve as permissões necessárias para os usuários que gerenciam Clusters de Big Data.

> [!NOTE]
> Para obter recursos adicionais sobre o modelo RBAC do Kubernetes, confira [Como usar a autorização do RBAC – Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) e [Como usar o RBAC para definir e aplicar permissões – OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

## <a name="role-required-for-deployment"></a>Função necessária para a implantação

O BDC usa contas de serviço (como `sa-mssql-controller` ou `master`) para orquestrar o provisionamento de pods de cluster, serviços, alta disponibilidade, monitoramento etc. Quando a implantação do BDC é iniciada (por exemplo, `azdata bdc create`), `azdata` faz o seguinte:

1. Verifica se o namespace fornecido existe.
2. Se o namespace não existir, ele criará um e aplicará o rótulo `MSSQL_CLUSTER`.
3. Cria a conta de serviço `sa-mssql-controller`.
4. Cria uma função `<namespaced>-admin` com permissões completas no namespace ou no projeto, mas não permissões em nível de cluster.
5. Cria uma atribuição de função dessa conta de serviço à função.

Depois que essas etapas forem concluídas, os pods do painel de controle serão provisionados e a conta de serviço implantará o restante do cluster de Big Data.  

Como consequência, o usuário que fará a implantação precisará ter permissões para:

- Listar os namespaces no cluster (1).
- Corrigir o namespace novo ou existente com o rótulo (2).
- Criar a conta de serviço `sa-mssql-controller`, a função `<namespaced>-admin` e a associação de função (3-5).

A função `admin` padrão não tem essas permissões e, portanto, o usuário que implanta o cluster de Big Data precisará ter, pelo menos, permissões de administrador no nível de namespace.

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>Função de cluster necessária para a coleta de métricas de pods e de nós

Do SQL Server 2019 CU5 em diante, o Telegraf exige uma conta de serviço com permissões de função em todo o cluster para coletar as métricas de pods e de nós. Durante a implantação (ou a atualização de implantações existentes), tentamos criar a conta de serviço e a função de cluster necessárias, mas se o usuário que está implantando o cluster ou realizando a atualização não tiver permissões suficientes, a implantação ou a atualização continuará com um aviso e terá sucesso. Nesse caso, as métricas de pods e de nós não serão coletadas. O usuário que está implantando o cluster precisará solicitar a um administrador de cluster que crie a função e a conta de serviço (antes ou depois da implantação ou da atualização). Depois que elas forem criadas, o BDC as usará. 

Este é um script que mostra como criar os artefatos necessários:

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

A conta de serviço, a função de cluster e a associação de função de cluster podem ser criadas antes ou depois da implantação do BDC. O Kubernetes atualiza automaticamente a permissão para a conta de serviço do Telegraf. Se elas forem criadas como uma implantação de pod, você verá um atraso de alguns minutos nas métricas de pods e de nós que estão sendo coletadas.

> [!NOTE]
> O SQL Server 2019 CU5 apresenta duas opções de recurso para controlar a coleta de métricas de pod e nó. Por padrão, esses parâmetros são definidos como verdadeiro em todos os destinos de ambiente, exceto no OpenShift, no qual o padrão é substituído. 

Personalize essas configurações na seção de segurança do arquivo de configuração de implantação `control.json`:

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

Se essas configurações forem definidas como `false`, o fluxo de trabalho de implantação do BDC não tentará criar a conta de serviço, a função de cluster e a associação para o Telegraf.
