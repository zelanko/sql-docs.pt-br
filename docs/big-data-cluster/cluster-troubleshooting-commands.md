---
title: Usar o kubectl para solucionar problemas de monitor /
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo fornece comandos kubectl útil para monitoramento e solução de problemas de um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f6556d271426157424bbc5f5dcbf1abbb4ffdc01
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241997"
---
# <a name="kubectl-commands-for-monitoring-and-troubleshooting-sql-server-big-data-clusters"></a>Comandos Kubectl para monitoramento e solução de problemas de clusters de grandes dados do SQL Server

Este artigo descreve vários comandos úteis do Kubernetes que você pode usar para monitorar e solucionar problemas de um cluster de big data do SQL Server 2019 (visualização). Este artigo aborda as tarefas comuns, como copiar arquivos de ou para um contêiner executando um dos serviços de cluster de big data do SQL Server. Ele também mostra como exibir detalhes de um pod ou outros artefatos do Kubernetes que estão localizados no cluster de big data.

## <a name="kubectl-command-examples"></a>Exemplos de comando Kubectl

Execute o seguinte **kubectl** comandos em um computador de cliente do Linux (bash) ou Windows (cmd ou PS). Eles exigem autenticação anterior no cluster e um contexto de cluster para executar no. Por exemplo, para um cluster do AKS criado anteriormente você pode executar `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` para baixar o arquivo de configuração de cluster do Kubernetes e definir o contexto do cluster.

## <a name="get-status-of-pods"></a>Obter o status de pods

Você pode usar o `kubectl get pods` comando para obter o status de pods no cluster para todos os namespaces ou o namespace de cluster de big data. As seções a seguir mostram exemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar o status de todos os pods no cluster do Kubernetes

Execute o seguinte comando para obter todos os pods e seus status, incluindo os pods que fazem parte do namespace que o SQL Server pods de cluster de big data são criados em:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar o status de todos os pods no cluster de big data do SQL Server

Use o `-n` parâmetro para especificar um namespace específico. Observe que os pods de cluster de big data são criados em um novo namespace criado no tempo de inicialização do cluster do SQL Server com base no nome do cluster especificado no `mssqlctl create cluster <cluster_name>` comando.

```bash
kubectl get pods -n <namespace_name>
```

Por exemplo, o comando a seguir mostra o status de pods em um cluster de big data chamado `big_data_cluster`:

```bash
kubectl get pods -n big_data_cluster
```

## <a name="get-pod-details"></a>Obter detalhes de pod

Execute o seguinte comando para obter uma descrição detalhada de um pod específica na saída do formato json. Ele inclui detalhes, como o nó atual do Kubernetes que o pod é colocado no, os contêineres em execução dentro do pod e a imagem usada para inicializar os contêineres. Ele também mostra outros detalhes, como rótulos, status e persistidos declarações de volumes que estão associadas com o pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

O exemplo a seguir mostra os detalhes para o `mssql-data-pool-master-0` pod em um cluster de big data chamado `big_data_cluster`:

```bash
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="get-status-of-services"></a>Obter o status de serviços

Execute o seguinte comando para obter detalhes sobre os serviços de cluster de big data. Esses detalhes incluem o tipo e os IPs associados a portas e os respectivos serviços. Observe que os serviços de cluster de big data do SQL Server são criados em um novo namespace criado no tempo de inicialização de cluster com base no nome do cluster especificado no `mssqlctl create cluster <cluster_name>` comando.

```bash
kubectl get svc -n <namespace_name>
```

O exemplo a seguir mostra o status para os serviços em um cluster de big data chamado `big_data_cluster`:

```bash
kubectl get svc -n big_data_cluster
```

## <a name="get-service-details"></a>Obter detalhes do serviço

Execute este comando para obter uma descrição detalhada de um serviço na saída do formato json. Ele inclui detalhes como rótulos, seletor de IP, external-IP (se o serviço é do tipo de Balanceador de carga), a porta, etc.
```
kubectl describe pod  <pod_name> -n <namespace_name>
```

Exemplo:
```
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="run-commands-in-a-container"></a>Executar comandos em um contêiner

Se a infraestrutura ou ferramentas existentes não permitem que você realizar determinada tarefa sem estar no contexto do contêiner, você poderá fazer logon contêiner usando `kubectl exec` comando. Por exemplo, talvez seja necessário verificar se existe um arquivo específico, ou talvez seja necessário reiniciar os serviços no contêiner. 

Para usar o `kubectl exec` de comando, use a seguinte sintaxe:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

As seções a seguir fornecem dois exemplos de como executar um comando em um contêiner específico.

### <a id="restartsql"></a> Faça logon em um contêiner específico e reinicie o processo do SQL Server

O exemplo a seguir mostra como reiniciar o processo do SQL Server no `mssql-server` recipiente no `mssql-master-pool-0` pod:

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> Faça logon em um contêiner específico e reiniciar os serviços em um contêiner
 
O exemplo a seguir mostra como reiniciar todos os serviços gerenciados pelo **supervisord**: 

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
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
kubectl cp mssql-master-pool-0:/var/opt/mssql/log -c mssql-server -n big_data_cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> Copiar arquivos no contêiner

O exemplo a seguir copia o **AdventureWorks2016CTP3.bak** arquivo do computador local para o contêiner de instância mestre do SQL Server (`mssql-server`) na `mssql-master-pool-0` pod. O arquivo é copiado para o `/tmp` diretório no contêiner. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n big_data_cluster
```

## <a id="forcedelete"></a> Exclusão forçada um pod
 
Ele não é recomendável force a exclusão de um pod. Mas para disponibilidade, resiliência ou persistência de dados de teste, você pode excluir um pod para simular uma falha de pod com o `kubectl delete pods` comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

O exemplo a seguir exclui o pod de pool de armazenamento, `mssql-storage-pool-default-0`:

```bash
kubectl delete pods mssql-storage-pool-default-0 -n big_data_cluster --grace-period=0 --force
```

## <a id="getip"></a> Obter o pod IP
 
Para fins de solução de problemas, você precisa obter o IP do nó que um pod está sendo executado. Para obter o endereço IP, use o `kubectl get pods` comando com a seguinte sintaxe:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

O exemplo a seguir obtém o endereço IP do nó que o `mssql-master-pool-0` pod está sendo executado em:

```bash
kubectl get pods mssql-master-pool-0 -o yaml -n big_data_cluster | grep hostIP
```

## <a name="start-the-kubernetes-dashboard"></a>Iniciar o painel do Kubernetes

Você pode iniciar o painel do Kubernetes para obter mais informações sobre o cluster. As seções a seguir explicam como iniciar o painel do Kubernetes no AKS e para o Kubernetes usando kubeadm a ser inicializado.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar Painel quando o cluster está em execução no AKS

Para iniciar o painel de Kubernetes executar:
 
```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se você receber o erro a seguir: *Não é possível escutar na porta 8001: Todos os ouvintes Falha ao criar com os seguintes erros: Não é possível criar o ouvinte: Erro escutar tcp4 127.0.0.1:8001: > associar: Normalmente, o uso de apenas um de cada endereço de soquete (endereço de rede/protocolo/porta) é permitido. Não é possível criar o ouvinte: Erro escutar tcp6: endereço [[:: 1]]: 8001: faltando porta no > erro de endereço: Não é possível escutar em qualquer uma das portas solicitadas: [{8001 9090}]*, verifique se você não iniciou o painel já em outra janela.

Quando você inicia o painel do navegador, você poderá receber avisos de permissão devido a RBAC que está sendo habilitada por padrão em clusters AKS e a conta de serviço usada pelo painel não tem permissões suficientes para acessar todos os recursos (por exemplo,  *é proibido pods: Usuário "system: serviceaccount:kube-sistema: kubernetes-painel" não é possível listar os pods no namespace "default"*). Execute o seguinte comando para conceder as permissões necessárias para `kubernetes-dashboard`e, em seguida, reinicie o painel:

```
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar Painel quando o cluster Kubernetes é a ser inicializado usando kubeadm

Para instruções detalhadas de como implantar e configurar o painel em seu cluster Kubernetes, consulte [a documentação do Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar o painel do Kubernetes, execute este comando:

```
kubectl proxy
```

## <a name="next-steps"></a>Próximas etapas

Para monitorar e solucionar problemas que é específico para o SQL Server grandes dados clusters, consulte o [portal de administração de cluster](cluster-admin-portal.md).