---
title: Implantação no OpenShift
titleSuffix: SQL Server Big Data Cluster
description: Saiba como atualizar Clusters de Big Data do SQL Server no OpenShift.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 91c491facec15ea50ee93641ff9482b20e5bbf1a
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "96123986"
---
# <a name="deploy-big-data-clusters-2019-on-openshift-on-premises-and-azure-red-hat-openshift"></a>Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no OpenShift local e no Red Hat OpenShift no Azure

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo explica como implantar um BDC (cluster de Big Data) do SQL Server em ambientes do OpenShift, no local ou no ARO (Red Hat OpenShift no Azure).

> [!TIP]
> Para encontrar uma forma rápida de inicializar um ambiente de exemplo usando o ARO e o BDC implantado nessa plataforma, use o script Python disponível [aqui](quickstart-big-data-cluster-deploy-aro.md).


O SQL Server 2019 CU5 introduz o suporte para Clusters de Big Data do SQL Server no OpenShift. Você pode implantar Clusters de Big Data no OpenShift local ou no ARO (Red Hat OpenShift no Azure). A implantação exige a versão mínima 4.3 do cluster OpenShift. Embora o fluxo de trabalho de implantação seja semelhante à implantação em outras plataformas baseadas no Kubernetes ([kubeadm](deploy-with-kubeadm.md) e [AKS](deploy-on-aks.md)), há algumas diferenças. A diferença está principalmente na execução de aplicativos como o usuário não raiz e o contexto de segurança usado para namespace no qual o BDC é implantado.

Para implantar o cluster OpenShift no local, confira a [documentação do Red Hat OpenShift](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-installation-and-upgrade). Para implantações do ARO, confira o [Red Hat OpenShift no Azure](/azure/openshift/intro-openshift).

Este artigo descreve as etapas de implantação específicas da plataforma OpenShift, destaca as opções existentes para acessar o ambiente de destino e o namespace que você está usando para implantar o cluster de Big Data.

## <a name="pre-requisites"></a>Pré-requisitos

> [!IMPORTANT]
> Os pré-requisitos abaixo precisam ser executados por um administrador de cluster OpenShift (função de cluster de administrador de cluster) que tenha permissões suficientes para criar esses objetos no nível de cluster. Para obter mais informações sobre as funções de cluster do OpenShift, confira [Como usar o RBAC para definir e aplicar permissões](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

1. Verifique se a configuração de `pidsLimit` do OpenShift está atualizada para acomodar cargas de trabalho do SQL Server. O valor padrão no OpenShift é muito baixo para cargas de trabalho semelhantes a de produção. Comece com pelo menos `4096`, mas o valor ideal depende da configuração de `max worker threads` no SQL Server e do número de processadores da CPU no nó do host do OpenShift. 
    - Para descobrir como atualizar o `pidsLimit` para o cluster do OpenShift, use [estas instruções]( https://github.com/openshift/machine-config-operator/blob/master/docs/ContainerRuntimeConfigDesign.md). Observe que as versões do OpenShift anteriores a `4.3.5` apresentavam um defeito que fazia com que o valor atualizado não entrasse em vigor. Lembre-se de atualizar o OpenShift para a última versão. 
    - Para ajudar você a calcular o valor ideal dependendo do ambiente e das cargas de trabalho planejadas do SQL Server, use a estimativa e os exemplos abaixo:

    |Número de processadores|Número máximo de threads de trabalho padrão|Trabalhos padrão por processador|Valor mínimo de pidsLimit|
    |--------------------|--------------------------|-----------------------------|-----------------------|
    |          64        |           512            |             16              | 512 + (64 *16) = 1.536 |
    |         128        |           512            |             32              | 512 + (128*32) = 4.608 |

    > [!NOTE]
    > Outros processos (por exemplo, backups, CLR, texto completo, SQLAgent) também adicionam uma sobrecarga; portanto, adicione um buffer ao valor estimado.

1. Baixe a SCC (restrição de contexto de segurança) personalizada [`bdc-scc.yaml`](#bdc-sccyaml-file):

    ```console
    curl https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml -o bdc-scc.yaml
    ```

1. Aplique a SCC ao cluster.

    ```console
    oc apply -f bdc-scc.yaml
    ```

    > [!NOTE]
    > A SCC personalizada para o BDC é baseada na SCC `nonroot` interno no OpenShift, com permissões adicionais. Para saber mais sobre as restrições de contexto de segurança do OpenShift, confira [Como gerenciar restrições de contexto de segurança](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html). Para obter informações detalhadas sobre quais permissões adicionais são necessárias para Clusters de Big Data na SCC `nonroot`, baixe o white paper [aqui](https://aka.ms/sql-bdc-openshift-security).

3. Crie um namespace/um projeto:

   ```console
   oc new-project <namespaceName>
   ```

4. Atribua a SCC personalizada às contas de serviços dos usuários no namespace em que o BDC foi implantado:

   ```console
   oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:<namespaceName>
   ```

5. Atribua a permissão apropriada ao usuário que está implantando o BDC. Execute uma delas. 

   - Se o usuário que está implantando o BDC tiver a função de administrador de cluster, prossiga para [Implantar cluster de Big Data](#deploy-big-data-cluster).

   - Se o usuário que está implantando o BDC for um administrador de namespace, atribua a ele a função local de administrador de cluster no namespace criado. A opção preferencial é que o usuário que implanta e gerencia o cluster de Big Data tenha permissões de administrador no nível do namespace.

   ```console
   oc adm policy add-role-to-user cluster-admin <deployingUser> -n <namespaceName>
   ```

   O usuário que está implantando o cluster de Big Data precisará fazer logon no console do OpenShift:

   ```console
   oc login -u <deployingUser> -p <password>
   ```

## <a name="deploy-big-data-cluster"></a>Implantar um cluster de Big Data

1. Instale o [azdata](../azdata/install/deploy-install-azdata.md) mais recente.

1. Clone um dos arquivos de configuração internos do OpenShift, dependendo do ambiente de destino (OpenShift local ou ARO) e do cenário de implantação. Confira a seção *Configurações específicas do OpenShift nos arquivos de configuração de implantação* abaixo para obter as configurações específicas do OpenShift nos arquivos de configuração internos. Para obter mais detalhes sobre os arquivos de configuração disponíveis, confira as [diretrizes de implantação](deployment-guidance.md).

   Liste todos os arquivos de configuração internos disponíveis.

   ```console
   azdata bdc config list
   ```

   Para clonar um dos arquivos de configuração internos, execute o comando abaixo (opcionalmente, você pode substituir o perfil com base na plataforma/no cenário de destino):

   ```console
   azdata bdc config init --source openshift-dev-test --target custom-openshift
   ```

   Para uma implantação no ARO, comece com um dos perfis `aro-`, que inclui valores padrão para `serviceType` e `storageClass` apropriados para esse ambiente. Por exemplo:

   ```console
   azdata bdc config init --source aro-dev-test --target custom-openshift
   ```

1. Personalize os arquivos de configuração control.json e bdc.json. Estes são alguns recursos adicionais que orientarão você nas personalizações compatíveis com vários casos de uso:

   - [Storage](concept-data-persistence.md)
   - [Configurações relacionadas ao AD](active-directory-deploy.md)
   - [Outras personalizações](deployment-custom-configuration.md)

   > [!NOTE]
   > Não há suporte para a integração ao Azure Active Directory no BDC e, portanto, você não pode usar esse método de autenticação para a implantação no ARO.

1. Definir [variáveis de ambiente](deployment-guidance.md#env)

1. Implantar um cluster de Big Data

   ```console
   azdata bdc create --config custom-openshift --accept-eula yes
   ```

1. Após a implantação bem-sucedida, você poderá fazer logon e listar os pontos de extremidade do cluster externo:

   ```console
      azdata login -n mssql-cluster
      azdata bdc endpoint list
   ```

## <a name="openshift-specific-settings-in-the-deployment-configuration-files"></a>Configurações específicas do OpenShift nos arquivos de configuração de implantação

O SQL Server 2019 CU5 apresenta duas opções de recurso para controlar a coleta de métricas de pod e nó. Esses parâmetros são definidos como `false` por padrão nos perfis internos do OpenShift, já que os contêineres de monitoramento exigem um [contexto de segurança com privilégios](https://www.openshift.com/blog/managing-sccs-in-openshift), o que flexibilizará algumas das restrições de segurança para o namespace no qual BDC foi implantado.

```json
    "security": {
      "allowNodeMetricsCollection": false,
      "allowPodMetricsCollection": false
}
```

O nome da classe de armazenamento padrão do ARO é managed-premium (em oposição ao AKS, em que a classe de armazenamento padrão é chamada default). Você encontrará isso no `control.json` correspondente a `aro-dev-test` e `aro-dev-test-ha`:

```json
    },
    "storage": {
      "data": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
      }
```

## <a name="bdc-sccyaml-file"></a>Arquivo `bdc-scc.yaml`

O arquivo SCC para essa implantação é:

:::code language="yaml" source="../../sql-server-samples/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml":::

## <a name="next-steps"></a>Próximas etapas

[Tutorial: Carregar dados de exemplo em um cluster de Big Data do SQL Server](tutorial-load-sample-data.md)
