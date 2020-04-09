---
title: Solucionar problemas do Kubernetes
titleSuffix: SQL Server big data clusters
description: Este artigo fornece comandos úteis para monitorar e solucionar problemas de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9ab57972b9ba0d758ff692887fa8d93d7f731d0a
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664180"
---
# <a name="troubleshoot-big-data-clusters-2019-kubernetes"></a>Solucionar problemas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]do Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve vários comandos úteis do Kubernetes que você pode usar para monitorar e solucionar problemas de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Ele mostra como exibir detalhes de um pod ou outros artefatos do Kubernetes que estão localizados no cluster de Big Data. Este artigo também aborda tarefas comuns, como copiar arquivos bidirecionalmente em um contêiner que executa um dos serviços de cluster de Big Data do SQL Server.

> [!TIP]
> Para monitorar o status de componentes de Clusters de Big Data, você pode usar comandos [**azdata bdc status**](deployment-guidance.md#status) ou [notebooks de solução de problemas](notebooks-manage-bdc.md) internos fornecidos com o Azure Data Studio.

> [!TIP]
> Execute os comandos **kubectl** a seguir em um computador cliente Windows (cmd ou PS) ou Linux (Bash). Eles exigem a autenticação anterior no cluster e um contexto de cluster para execução. Por exemplo, para um cluster do AKS criado anteriormente, você pode executar `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` para baixar o arquivo de configuração de cluster do Kubernetes e definir o contexto do cluster.

## <a name="get-status-of-pods"></a>Obter o status de pods

Use o comando `kubectl get pods` para obter o status de pods no cluster para todos os namespaces ou o namespace do cluster de Big Data. As seções a seguir mostram exemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar o status de todos os pods no cluster do Kubernetes

Execute o comando a seguir para obter todos os pods e os status, incluindo os pods que fazem parte do namespace no qual os pods de clusters de Big Data do SQL Server são criados:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar o status de todos os pods no cluster de Big Data do SQL Server

Use o parâmetro `-n` para especificar um namespace específico. Observe que os pods de clusters de Big Data do SQL Server são criados em um namespace criado no momento de inicialização do cluster com base no nome do cluster especificado no arquivo de configuração de implantação. O nome padrão, `mssql-cluster`, é usado aqui.

```bash
kubectl get pods -n mssql-cluster
```

Você deverá ver uma saída semelhante à seguinte lista para um cluster de Big Data em execução:

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> Durante a implantação, os pods com um **STATUS** igual a **ContainerCreating** ainda estão sendo recebidos. Se a implantação travar por qualquer motivo, isso poderá dar uma ideia da possível causa do problema. Examine também a coluna **PRONTO**. Isso informa quantos contêineres foram iniciados no pod. Observe que as implantações podem levar 30 minutos ou mais, dependendo da configuração e da rede. Grande parte desse tempo é gasto no download das imagens de contêiner para componentes diferentes.

## <a name="get-pod-details"></a>Obter detalhes do pod

Execute o comando a seguir para obter uma descrição detalhada de um pod específico na saída de formato JSON. Ele inclui detalhes, como o nó atual do Kubernetes no qual o pod é colocado, os contêineres em execução no pod e a imagem usada para inicializar os contêineres. Ele também mostra outros detalhes, como rótulos, status e declarações de volumes persistentes associados ao pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

O seguinte exemplo mostra os detalhes do pod `master-0` em um cluster de Big Data chamado `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Caso ocorram erros, às vezes, você poderá ver o erro nos eventos recentes do pod.

## <a name="get-pod-logs"></a>Obter os logs do pod

Você poderá recuperar os logs para contêineres em execução em um pod. O seguinte comando recupera os logs de todos os contêineres em execução no pod chamado `master-0` e os gera em um arquivo chamado `master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluster > master-0-pod-logs.txt
```

## <a name="get-status-of-services"></a><a id="services"></a> Obter o status de serviços

Execute o comando a seguir para obter detalhes dos serviços de clusters de Big Data. Esses detalhes incluem o tipo e os IPs associados aos respectivos serviços e às respectivas portas. Observe que os serviços de clusters de Big Data do SQL Server são criados em um namespace criado no momento de inicialização do cluster com base no nome do cluster especificado no arquivo de configuração de implantação.

```bash
kubectl get svc -n <namespace_name>
```

O seguinte exemplo mostra o status dos serviços em um cluster de Big Data chamado `mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

Os seguintes serviços dão suporte a conexões externas com o cluster de Big Data:

| Serviço | Descrição |
|---|---|
| **master-svc-external** | Fornece acesso à instância mestra.<br/>(**EXTERNAL-IP,31433** e o usuário **SA**) |
| **controller-svc-external** | Dá suporte a ferramentas e clientes que gerenciam o cluster. |
| **gateway-svc-external** | Fornece acesso ao gateway do HDFS/Spark.<br/>(**EXTERNAL-IP** e o usuário **raiz**) |
| **appproxy-svc-external** | Dá suporte a cenários de implantação de aplicativos. |

> [!TIP]
> Essa é uma maneira de exibir os serviços com **kubectl**, mas também é possível usar o comando `azdata bdc endpoint list` para exibir esses pontos de extremidade. Para obter mais informações, confira [Obter pontos de extremidade de cluster de Big Data](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Obter detalhes do serviço

Execute este comando para obter uma descrição detalhada de um serviço na saída de formato JSON. Ele incluirá detalhes como rótulos, seletores, IP, IP externo (se o serviço for do tipo LoadBalancer), porta etc.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

O seguinte exemplo recupera detalhes do serviço **master-svc-external**:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="copy-files"></a><a id="copy"></a> Copiar arquivos

Caso precise copiar arquivos do contêiner para o computador local, use o comando `kubectl cp` com a seguinte sintaxe:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Da mesma forma, use `kubectl cp` para copiar arquivos do computador local para um contêiner específico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a name="copy-files-from-a-container"></a><a id="copyfrom"></a> Copiar arquivos de um contêiner

O seguinte exemplo copia os arquivos de log de SQL Server do contêiner para o caminho `~/temp/sqlserverlogs` no computador local (neste exemplo, o computador local é um cliente Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a name="copy-files-into-container"></a><a id="copyinto"></a> Copiar arquivos para o contêiner

O exemplo a seguir copia o arquivo **AdventureWorks2016CTP3.bak** do computador local para o contêiner da instância mestra do SQL Server (`mssql-server`) no pod `master-0`. O arquivo é copiado para o diretório `/tmp` no contêiner. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a name="force-delete-a-pod"></a><a id="forcedelete"></a> Forçar a exclusão de um pod
 
Não é recomendável forçar a exclusão de um pod. Porém, para testar a disponibilidade, a resiliência ou a persistência de dados, você pode excluir um pod para simular uma falha de pod com o comando `kubectl delete pods`.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

O seguinte exemplo exclui o pod do pool de armazenamento, `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a name="get-pod-ip"></a><a id="getip"></a> Obter o IP do pod
 
Para fins de solução de problemas, talvez seja necessário obter o IP do nó em que um pod está sendo executado. Para obter o endereço IP, use o comando `kubectl get pods` com a seguinte sintaxe:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

O seguinte exemplo obtém o endereço IP do nó em que o pod `master-0` está em execução:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Painel do Kubernetes

Inicie o painel do Kubernetes para obter mais informações sobre o cluster. As seções a seguir explicam como iniciar o painel do Kubernetes no AKS e do Kubernetes inicializado usando o kubeadm.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar o painel quando o cluster estiver em execução no AKS

Para iniciar a execução do painel do Kubernetes:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se você receber o seguinte erro: *Não é possível escutar a porta 8001: Falha na criação de todos os ouvintes com os seguintes erros: Não é possível criar o ouvinte: Erro ao escutar tcp4 127.0.0.1:8001: >associação: Normalmente, apenas um tipo de uso de cada endereço de soquete (endereço de rede/protocolo/porta) é permitido. Não é possível criar o ouvinte: Erro ao escutar tcp6: endereço [[::1]]:8001: porta ausente em >erro de endereço: Não é possível escutar nenhuma das portas solicitadas: [{8001 9090}]* . Verifique se o painel já não foi iniciado em outra janela.

Ao iniciar o painel no navegador, você poderá obter avisos de permissão devido ao RBAC estar habilitado por padrão em clusters do AKS. Além disso, a conta de serviço usada pelo painel não tem permissões suficientes para acessar todos os recursos (por exemplo, *pods são proibidos: O usuário "system:serviceaccount:kube-system:kubernetes-dashboard" não pode listar os pods no namespace "padrão"* ). Execute o seguinte comando para conceder as permissões necessárias ao `kubernetes-dashboard` e, em seguida, reinicie o painel:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar o painel quando o cluster do Kubernetes for inicializado usando o kubeadm

Para obter instruções detalhadas sobre como implantar e configurar o painel no cluster do Kubernetes, confira [a documentação do Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar o painel do Kubernetes, execute este comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).
