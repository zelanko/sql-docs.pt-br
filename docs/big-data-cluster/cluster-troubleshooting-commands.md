---
title: Monitorar e solucionar problemas
titleSuffix: SQL Server big data clusters
description: Este artigo fornece comandos úteis para monitorar e solucionar problemas de um cluster SQL Server Big Data 2019 (versão prévia).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419481"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Monitoramento e solução de problemas SQL Server clusters de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve vários comandos kubernetes úteis que você pode usar para monitorar e solucionar problemas de um cluster SQL Server 2019 Big Data (versão prévia). Ele mostra como exibir detalhes detalhados de um pod ou outros artefatos kubernetes que estão localizados no cluster Big Data. Este artigo também aborda tarefas comuns, como copiar arquivos de ou para um contêiner que executa um dos serviços de cluster SQL Server Big Data.

> [!TIP]
> Execute os comandos **kubectl** a seguir em um computador cliente Windows (cmd ou PS) ou Linux (bash). Eles exigem a autenticação anterior no cluster e um contexto de cluster para executar. Por exemplo, para um cluster AKs criado anteriormente, você pode `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` executar para baixar o arquivo de configuração de cluster kubernetes e definir o contexto do cluster.

## <a name="get-status-of-pods"></a>Obter status de pods

Você pode usar o `kubectl get pods` comando para obter o status de pods no cluster para todos os namespaces ou para o namespace de cluster Big Data. As seções a seguir mostram exemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar status de todos os pods no cluster kubernetes

Execute o comando a seguir para obter todos os pods e seus status, incluindo os pods que fazem parte do namespace que SQL Server Big Data pods de cluster são criados em:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar o status de todos os pods no cluster de SQL Server Big Data

Use o `-n` parâmetro para especificar um namespace específico. Observe que SQL Server Big Data pods de cluster são criados em um novo namespace criado no tempo de inicialização do cluster com base no nome do cluster especificado no arquivo de configuração de implantação. O nome padrão, `mssql-cluster`, é usado aqui.

```bash
kubectl get pods -n mssql-cluster
```

Você deverá ver uma saída semelhante à lista a seguir para um cluster Big Data em execução:

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
> Durante a implantação, os pods com um **status** de **ContainerCreating** ainda estão chegando. Se a implantação parar por qualquer motivo, isso poderá lhe dar uma ideia de onde o problema pode ser. Examine também a coluna **pronto** . Isso informa quantos contêineres foram iniciados no pod. Observe que as implantações podem levar 30 minutos ou mais, dependendo da configuração e da rede. Grande parte desse tempo é gasto para baixar as imagens de contêiner para componentes diferentes.

## <a name="get-pod-details"></a>Obter detalhes do pod

Execute o comando a seguir para obter uma descrição detalhada de um pod específico na saída de formato JSON. Ele inclui detalhes, como o nó kubernetes atual no qual o pod é colocado, os contêineres em execução dentro do pod e a imagem usada para inicializar os contêineres. Ele também mostra outros detalhes, como rótulos, status e declarações de volumes persistentes associados ao Pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

O exemplo a seguir mostra os detalhes do `master-0` pod em um cluster Big data chamado `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Se ocorrerem erros, algumas vezes você poderá ver o erro nos eventos recentes do pod.

## <a name="get-pod-logs"></a>Obter logs de Pod

Você pode recuperar os logs para contêineres em execução em um pod. O comando a seguir recupera os logs de todos os contêineres em execução `master-0` no pod nomeado e os gera em `master-0-pod-logs.txt`um nome de arquivo:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>Obter status dos serviços

Execute o comando a seguir para obter detalhes para os serviços de cluster Big Data. Esses detalhes incluem o tipo e os IPs associados aos respectivos serviços e portas. Observe que SQL Server Big Data serviços de cluster são criados em um novo namespace criado no tempo de inicialização do cluster com base no nome do cluster especificado no arquivo de configuração de implantação.

```bash
kubectl get svc -n <namespace_name>
```

O exemplo a seguir mostra o status dos serviços em um cluster Big Data `mssql-cluster`chamado:

```bash
kubectl get svc -n mssql-cluster
```

Os serviços a seguir dão suporte a conexões externas com o cluster Big Data:

| Serviço | Descrição |
|---|---|
| **master-svc-external** | Fornece acesso à instância mestra.<br/>(**External-IP, 31433** e o usuário **SA** ) |
| **controller-svc-external** | Oferece suporte a ferramentas e clientes que gerenciam o cluster. |
| **gateway-svc-external** | Fornece acesso ao gateway HDFS/Spark.<br/>(**External-IP** e o usuário **raiz** ) |
| **appproxy-svc-external** | Suporte a cenários de implantação de aplicativos. |

> [!TIP]
> Essa é uma maneira de exibir os serviços com **kubectl**, mas também é possível usar `azdata bdc endpoint list` o comando para exibir esses pontos de extremidade. Para obter mais informações, consulte [obter Big data pontos de extremidade de cluster](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Obter detalhes do serviço

Execute este comando para obter uma descrição detalhada de um serviço na saída de formato JSON. Ele incluirá detalhes como rótulos, seletores, IP, External-IP (se o serviço for do tipo de balanceador de carga), porta, etc.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

O exemplo a seguir recupera detalhes para o serviço **Master-svc-external** :

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Executar comandos em um contêiner

Se as ferramentas existentes ou a infraestrutura não permitir que você execute uma determinada tarefa sem realmente estar no contexto do contêiner, você poderá fazer logon no contêiner usando `kubectl exec` o comando. Por exemplo, talvez seja necessário verificar se um arquivo específico existe ou talvez seja necessário reiniciar os serviços no contêiner. 

Para usar o `kubectl exec` comando, use a seguinte sintaxe:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

As duas seções a seguir fornecem dois exemplos de como executar um comando em um contêiner específico.

### <a id="restartsql"></a>Faça logon em um contêiner específico e reinicie SQL Server processo

O exemplo a seguir mostra como reiniciar o processo de SQL Server no `mssql-server` contêiner `master-0` no pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>Faça logon em um contêiner específico e reinicie os serviços em um contêiner
 
O exemplo a seguir mostra como reiniciar todos os serviços gerenciados pelo **supervisor**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>Copiar arquivos

Se você precisar copiar arquivos do contêiner para seu computador local, use `kubectl cp` o comando com a seguinte sintaxe:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Da mesma forma, você `kubectl cp` pode usar o para copiar arquivos do computador local para um contêiner específico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>Copiar arquivos de um contêiner

O exemplo a seguir copia os arquivos de log de SQL Server do contêiner `~/temp/sqlserverlogs` para o caminho no computador local (neste exemplo, o computador local é um cliente Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>Copiar arquivos no contêiner

O exemplo a seguir copia o arquivo **AdventureWorks2016CTP3. bak** do computador local para o SQL Server contêiner da instância mestra`mssql-server`() no `master-0` Pod. O arquivo é copiado para `/tmp` o diretório no contêiner. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>Forçar exclusão de um pod
 
Não é recomendável forçar a exclusão de um pod. Mas para testar a disponibilidade, a resiliência ou a persistência de dados, você pode excluir um pod para simular uma falha `kubectl delete pods` de Pod com o comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

O exemplo a seguir exclui o Pod `storage-0-0`do pool de armazenamento:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>Obter IP de Pod
 
Para fins de solução de problemas, talvez seja necessário obter o IP do nó em que um pod está sendo executado. Para obter o endereço IP, use o `kubectl get pods` comando com a seguinte sintaxe:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

O exemplo a seguir obtém o endereço IP do nó em que `master-0` o Pod está em execução:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Painel do kubernetes

Você pode iniciar o painel do kubernetes para obter informações adicionais sobre o cluster. As seções a seguir explicam como iniciar o painel para kubernetes no AKS e para o kubernetes bootstraped usando o kubeadm.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar o painel quando o cluster estiver em execução no AKS

Para iniciar a execução do painel do kubernetes:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se você receber o seguinte erro: *Não é possível escutar na porta 8001: Todos os ouvintes não foram criados com os seguintes erros: Não é possível criar o ouvinte: Erro escutar tcp4 127.0.0.1:8001: > associar: Normalmente, é permitido apenas um uso de cada endereço de soquete (protocolo/endereço de rede/porta). Não é possível criar o ouvinte: Erro de escuta tcp6: endereço [[:: 1]]: 8001: porta ausente em > erro de endereço: Não é possível escutar em nenhuma das portas solicitadas: [{8001 9090}* ], verifique se você não iniciou o painel já em outra janela.

Quando você inicia o painel em seu navegador, pode obter avisos de permissão devido ao RBAC habilitado por padrão em clusters AKS, e a conta de serviço usada pelo painel não tem permissões suficientes para acessar todos os recursos (por exemplo,  *Pods é proibido: User "System: USERACCOUNT: Kube-System: kubernetes-Dashboard" não é possível listar pods no namespace "* default"). Execute o seguinte comando para conceder as permissões necessárias ao `kubernetes-dashboard`e reinicie o painel:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar o painel quando o cluster kubernetes for inicializado usando kubeadm

Para obter instruções detalhadas sobre como implantar e configurar o painel em seu cluster do kubernetes, consulte [a documentação do kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar o painel do kubernetes, execute este comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são SQL Server Big data clusters](big-data-cluster-overview.md).
