---
title: Monitorar e solucionar problemas
titleSuffix: SQL Server big data clusters
description: Este artigo fornece comandos úteis para monitorar e solucionar problemas de um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 0548176a191d5c2b16b113b5a931a1ed0435741c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472299"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Monitorar e solucionar problemas de clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve vários comandos úteis do Kubernetes que você pode usar para monitorar e solucionar problemas de um cluster de big data do SQL Server 2019 (visualização). Ele mostra como exibir detalhes de um pod ou outros artefatos do Kubernetes que estão localizados no cluster de big data. Este artigo também aborda tarefas comuns, como copiar arquivos de ou para um contêiner executando um dos serviços de cluster de big data do SQL Server.

> [!TIP]
> Execute o seguinte **kubectl** comandos em um computador de cliente do Linux (bash) ou Windows (cmd ou PS). Eles exigem autenticação anterior no cluster e um contexto de cluster para executar no. Por exemplo, para um cluster do AKS criado anteriormente você pode executar `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` para baixar o arquivo de configuração de cluster do Kubernetes e definir o contexto do cluster.

## <a name="get-status-of-pods"></a>Obter o status de pods

Você pode usar o `kubectl get pods` comando para obter o status de pods no cluster para todos os namespaces ou o namespace de cluster de big data. As seções a seguir mostram exemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar o status de todos os pods no cluster do Kubernetes

Execute o seguinte comando para obter todos os pods e seus status, incluindo os pods que fazem parte do namespace que o SQL Server pods de cluster de big data são criados em:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar o status de todos os pods no cluster de big data do SQL Server

Use o `-n` parâmetro para especificar um namespace específico. Observe que os pods de cluster de big data do SQL Server são criados em um novo namespace criado no tempo de inicialização do cluster com base no nome do cluster especificado no arquivo de configuração de implantação. O nome padrão, `mssql-cluster`, é usado aqui.

```bash
kubectl get pods -n mssql-cluster
```

Você deve ver a saída semelhante à lista a seguir para um cluster de execução big data:

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
> Durante a implantação, pods com um **STATUS** dos **ContainerCreating** ainda estão surgindo. Se a implantação trava por qualquer motivo, isso pode dar uma ideia em que o problema pode ser. Examine também os **pronto** coluna. Isso informa quantos contêineres começaram no pod. Observe que as implantações podem levar 30 minutos ou mais dependendo da sua configuração e a rede. Grande parte desse tempo é gasto baixando as imagens de contêiner para diferentes componentes.

## <a name="get-pod-details"></a>Obter detalhes de pod

Execute o seguinte comando para obter uma descrição detalhada de um pod específica na saída do formato JSON. Ele inclui detalhes, como o nó atual do Kubernetes que o pod é colocado no, os contêineres em execução dentro do pod e a imagem usada para inicializar os contêineres. Ele também mostra outros detalhes, como rótulos, status e persistidos declarações de volumes que estão associadas com o pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

O exemplo a seguir mostra os detalhes para o `master-0` pod em um cluster de big data chamado `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Se ocorreu algum erro, às vezes você pode ver o erro nos eventos recentes para o pod.

## <a name="get-pod-logs"></a>Obter logs de pod

Você pode recuperar os logs para contêineres em execução em um pod. O comando a seguir recupera os logs para todos os contêineres em execução no pod denominado `master-0` e gera como saída para um nome de arquivo `master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> Obter o status de serviços

Execute o seguinte comando para obter detalhes sobre os serviços de cluster de big data. Esses detalhes incluem o tipo e os IPs associados a portas e os respectivos serviços. Observe que os serviços de cluster de big data do SQL Server são criados em um novo namespace criado no tempo de inicialização de cluster com base no nome do cluster especificado no arquivo de configuração de implantação.

```bash
kubectl get svc -n <namespace_name>
```

O exemplo a seguir mostra o status para os serviços em um cluster de big data chamado `mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

Os seguintes serviços dão suporte a conexões externas para o cluster de big data:

| Serviço | Descrição |
|---|---|
| **master-svc-external** | Fornece acesso para a instância mestre.<br/>(**EXTERNAL-IP, 31433** e o **SA** usuário) |
| **controller-svc-external** | Dá suporte a ferramentas e clientes que gerenciam o cluster. |
| **mgmtproxy-svc-external** | Fornece acesso para o [Portal de administração de Cluster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**:30777/portal) |
| **gateway-svc-external** | Fornece acesso para o gateway HDFS/Spark.<br/>(**EXTERNAL-IP** e o **raiz** usuário) |
| **appproxy-svc-external** | Suporte a cenários de implantação do aplicativo. |

> [!TIP]
> Essa é uma maneira de exibir os serviços com **kubectl**, mas também é possível usar `mssqlctl cluster endpoints list` comando para exibir esses pontos de extremidade. Para obter mais informações, consulte [obter pontos de extremidade de cluster de big data](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Obter detalhes do serviço

Execute este comando para obter uma descrição detalhada de um serviço na saída do formato JSON. Ele inclui detalhes como rótulos, seletor de IP, external-IP (se o serviço é do tipo de Balanceador de carga), a porta, etc.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

O exemplo a seguir recupera os detalhes para o **master-svc-externo** serviço:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Executar comandos em um contêiner

Se a infraestrutura ou ferramentas existentes não permitem que você realizar determinada tarefa sem estar no contexto do contêiner, você poderá fazer logon contêiner usando `kubectl exec` comando. Por exemplo, talvez seja necessário verificar se existe um arquivo específico, ou talvez seja necessário reiniciar os serviços no contêiner. 

Para usar o `kubectl exec` de comando, use a seguinte sintaxe:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

As seções a seguir fornecem dois exemplos de como executar um comando em um contêiner específico.

### <a id="restartsql"></a> Faça logon em um contêiner específico e reinicie o processo do SQL Server

O exemplo a seguir mostra como reiniciar o processo do SQL Server no `mssql-server` recipiente no `master-0` pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> Faça logon em um contêiner específico e reiniciar os serviços em um contêiner
 
O exemplo a seguir mostra como reiniciar todos os serviços gerenciados pelo **supervisord**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> Copiar arquivos

Se você precisa copiar os arquivos do contêiner em seu computador local, use `kubectl cp` comando com a seguinte sintaxe:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Da mesma forma, você pode usar `kubectl cp` para copiar arquivos do computador local para um contêiner específico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> Copiar arquivos de um contêiner

O exemplo a seguir copia os arquivos de log do SQL Server do contêiner para o `~/temp/sqlserverlogs` caminho no computador local (no exemplo o computador local é um cliente Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> Copiar arquivos no contêiner

O exemplo a seguir copia o **AdventureWorks2016CTP3.bak** arquivo do computador local para o contêiner de instância mestre do SQL Server (`mssql-server`) na `master-0` pod. O arquivo é copiado para o `/tmp` diretório no contêiner. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> Exclusão forçada um pod
 
Ele não é recomendável force a exclusão de um pod. Mas para disponibilidade, resiliência ou persistência de dados de teste, você pode excluir um pod para simular uma falha de pod com o `kubectl delete pods` comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

O exemplo a seguir exclui o pod de pool de armazenamento, `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> Obter o pod IP
 
Para fins de solução de problemas, você precisa obter o IP do nó que um pod está sendo executado. Para obter o endereço IP, use o `kubectl get pods` comando com a seguinte sintaxe:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

O exemplo a seguir obtém o endereço IP do nó que o `master-0` pod está sendo executado em:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>Portal de administração de cluster

Use o [portal de administração de cluster](cluster-admin-portal.md) para monitorar o status do seu cluster de big data. Por exemplo, durante as implantações, você pode usar o **implantação** guia. Você precisa esperar para o **mgmtproxy-svc-externo** início antes de acessar esse portal, portanto, ele não estará disponível no início de uma implantação do serviço.

## <a name="kubernetes-dashboard"></a>Painel do Kubernetes

Você pode iniciar o painel do Kubernetes para obter mais informações sobre o cluster. As seções a seguir explicam como iniciar o painel do Kubernetes no AKS e para o Kubernetes usando kubeadm a ser inicializado.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar Painel quando o cluster está em execução no AKS

Para iniciar o painel de Kubernetes executar:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se você receber o erro a seguir: *Não é possível escutar na porta 8001: Todos os ouvintes Falha ao criar com os seguintes erros: Não é possível criar o ouvinte: Erro escutar tcp4 127.0.0.1:8001: > associar: Normalmente, o uso de apenas um de cada endereço de soquete (endereço de rede/protocolo/porta) é permitido. Não é possível criar o ouvinte: Erro escutar tcp6: endereço [[:: 1]]: 8001: faltando porta no > erro de endereço: Não é possível escutar em qualquer uma das portas solicitadas: [{8001 9090}]*, verifique se você não iniciou o painel já em outra janela.

Quando você inicia o painel do navegador, você poderá receber avisos de permissão devido a RBAC que está sendo habilitada por padrão em clusters AKS e a conta de serviço usada pelo painel não tem permissões suficientes para acessar todos os recursos (por exemplo,  *é proibido pods: Usuário "system: serviceaccount:kube-sistema: kubernetes-painel" não é possível listar os pods no namespace "default"*). Execute o seguinte comando para conceder as permissões necessárias para `kubernetes-dashboard`e, em seguida, reinicie o painel:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar Painel quando o cluster Kubernetes é a ser inicializado usando kubeadm

Para instruções detalhadas de como implantar e configurar o painel em seu cluster Kubernetes, consulte [a documentação do Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar o painel do Kubernetes, execute este comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters de grandes dados do SQL Server](big-data-cluster-overview.md).