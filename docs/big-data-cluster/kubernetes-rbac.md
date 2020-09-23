---
title: RBAC do Kubernetes
titleSuffix: SQL Server big data clusters
description: Este artigo descreve como os Clusters de Big Data do SQL Server usam o RBAC com o Kubernetes.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79ea97a0824d7213f0758d75f8b552372bba51c2
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879043"
---
# <a name="kubernetes-rbac-model--impact-on-users-and-service-accounts-managing-bdc"></a>O modelo RBAC do Kubernetes e o impacto sobre os usuários e as contas de serviço que gerenciam os BDC

Este artigo descreve os requisitos de permissões para usuários que gerenciam clusters de Big Data e a semântica em relação à conta de serviço padrão e ao acesso do Kubernetes de dentro do cluster de Big Data.

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

Estas são as etapas para ver como criar os artefatos necessários:

1. Crie um arquivo *metrics-role.yaml* com o conteúdo abaixo. Substitua os espaços reservados *<clusterName>* pelo nome do seu cluster de Big Data.

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: <clusterName>:cr-mssql-metricsdc-reader
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
     name: <clusterName>:crb-mssql-metricsdc-reader
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: <clusterName>:cr-mssql-metricsdc-reader
   subjects:
   - kind: ServiceAccount
     name: sa-mssql-metricsdc-reader
     namespace: <clusterName>
   ```

2. Crie a função de cluster e a associação dela:

   ```bash
   kubectl create -f metrics-role.yaml
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

## <a name="default-service-account-usage-from-within-a-bdc-pod"></a>Uso da conta de serviço padrão de dentro de um pod dos BDC

Para obter um modelo de segurança mais rígido, a CU5 do SQL Server 2019 desabilitou a montagem por credenciais padrão para a conta de serviço do Kubernetes padrão dentro do pods dos BDC. Isso se aplica a implantações novas e atualizadas na CU5 ou versões posteriores.
O token de credencial dentro dos pods pode ser usado para acessar o servidor de API do Kubernetes, e o nível de permissões depende das configurações da política de autorização do Kubernetes. Se você tiver casos de uso específicos que exijam a reversão para o comportamento anterior da CU5, apresentaremos na CU6 uma nova opção de recurso para que seja possível ativar a montagem automática no momento da implantação. Você pode fazer isso usando o arquivo de implantação de configuração control.json e definindo *automountServiceAccountToken* como *true*. Execute este comando para atualizar essa definição no arquivo de configuração personalizado *control.json* usando a CLI `azdata`: 

``` bash
azdata bdc config replace -c custom-bdc/control.json -j "$.security.automountServiceAccountToken=true"
```
