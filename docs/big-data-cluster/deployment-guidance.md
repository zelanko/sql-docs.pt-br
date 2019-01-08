---
title: Como implantar
titleSuffix: SQL Server 2019 big data clusters
description: Aprenda a implantar clusters de big data de 2019 do SQL Server (versão prévia) no Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 9c1f2fbb750dcdf8e5d78ddcfd5004a32c0cc209
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246745"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Como implantar clusters de grandes dados do SQL Server no Kubernetes

Cluster de big data do SQL Server pode ser implantado como contêineres do docker em um cluster Kubernetes. Isso é uma visão geral das etapas de instalação e configuração:

- Configure o cluster Kubernetes em uma única VM, o cluster de VMs ou no serviço de Kubernetes do Azure (AKS).
- Instalar a ferramenta de configuração de cluster **mssqlctl** no computador cliente.
- Implante um cluster de big data do SQL Server em um cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Pré-requisitos de cluster de Kubernetes

Clusters de grandes dados do SQL Server requerem uma versão mínima do Kubernetes de pelo menos v 1.10 para servidor e cliente (kubectl).

> [!NOTE]
> Observe que as versões de servidor e cliente Kubernetes devem ser + 1 ou -1, versão secundária. Para obter mais informações, consulte [Kubernetes suporte para versões e componente distorção](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Instalação de cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atenda aos acima pré-requisitos, você poderá pular diretamente para o [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos de Kubernetes.  Para obter informações detalhadas sobre Kubernetes, consulte o [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar Kubernetes em qualquer uma das três maneiras:

| Implante Kubernetes em: | Descrição | Link |
|---|---|---|
| **Minikube** | Um cluster do Kubernetes de nó único em uma VM. | [Instruções](deploy-on-minikube.md) |
| **Serviços de Kubernetes do Azure (AKS)** | Um serviço gerenciado de contêiner do Kubernetes no Azure. | [Instruções](deploy-on-aks.md) |
| **Vários computadores** | Um cluster Kubernetes implantado em máquinas físicas ou virtuais usando **kubeadm** | [Instruções](deploy-with-kubeadm.md) |
  
> [!TIP]
> Para um script de python de exemplo que implanta o cluster de big data do AKS e o SQL Server, consulte [implantar um cluster de big data no serviço de Kubernetes do Azure (AKS) do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="deploy-sql-server-2019-big-data-tools"></a>Implantar ferramentas de big data do SQL Server de 2019

Antes de implantar o cluster de big data do SQL Server 2019, primeiramente [instalar as ferramentas de big data](deploy-big-data-tools.md):
- **mssqlctl**
- **Kubectl**
- **Azure Data Studio**
- **Extensão do SQL Server de 2019**

## <a id="deploy"></a> Implantar um cluster de big data do SQL Server

Depois de configurar o cluster Kubernetes, você pode prosseguir com a implantação de cluster de big data do SQL Server. 

> [!NOTE]
> Se você estiver atualizando de uma versão anterior, consulte o [atualizar a seção deste artigo](#upgrade).

Para implantar um cluster de big data no Azure com todas as configurações padrão para um ambiente de desenvolvimento/teste, siga as instruções neste artigo:

[Guia de início rápido: Implantar um cluster de big data do SQL Server no Kubernetes](quickstart-big-data-cluster-deploy.md)

Se você quiser personalizar sua implantação de cluster de big data de acordo com sua carga de trabalho necessidades de, siga as instruções no restante deste artigo.

## <a name="verify-kubernetes-configuration"></a>Verifique se a configuração do kubernetes

Execute o **kubectl** comando para exibir a configuração do cluster. Certifique-se de que kubectl está apontada para o contexto do cluster correto.

```bash
kubectl config view
```

## <a name="define-environment-variables"></a>Definir variáveis de ambiente

A configuração do cluster pode ser personalizada usando um conjunto de variáveis de ambiente que são passados para o `mssqlctl create cluster` comando. A maioria das variáveis de ambiente é opcional com valores padrão, conforme descrito abaixo. Observe que há variáveis de ambiente, como as credenciais que exigem entrada do usuário.

| Variável de ambiente | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|
| **ACCEPT_EULA** | Sim | N/D | Aceite o contrato de licença do SQL Server (por exemplo, ' Y').  |
| **CLUSTER_NAME** | Sim | N/D | O nome do namespace para implantar o SQLServer cluster de big data em Kubernetes. |
| **CLUSTER_PLATFORM** | Sim | N/D | A plataforma em que o cluster Kubernetes é implantado. Pode ser `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | Não | 1 | O número de réplicas de pool de computação para criar. No CTP 2.2 somente com o valor permitido é 1. |
| **CLUSTER_DATA_POOL_REPLICAS** | Não | 2 | O número de dados do pool réplicas para criar. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | Não | 2 | O número de réplicas de pool de armazenamento para criar. |
| **DOCKER_REGISTRY** | Sim | TBD | O registro privado onde as imagens usadas para implantar o cluster são armazenadas. |
| **DOCKER_REPOSITORY** | Sim | TBD | O repositório privado dentro do registro acima, onde as imagens são armazenadas.  É necessário durante a versão prévia pública controlada. |
| **DOCKER_USERNAME** | Sim | N/D | O nome de usuário para acessar as imagens de contêiner, caso eles são armazenados em um repositório privado. É necessário durante a versão prévia pública controlada. |
| **DOCKER_PASSWORD** | Sim | N/D | A senha para acessar o repositório privado acima. É necessário durante a versão prévia pública controlada.|
| **DOCKER_EMAIL** | Sim | N/D | O email associado com o repositório privado acima. É necessário para a duração da visualização privada restrita. |
| **DOCKER_IMAGE_TAG** | Não | mais recente | O rótulo usado para marcar as imagens. |
| **DOCKER_IMAGE_POLICY** | Não | Always | Sempre force um pull das imagens.  |
| **DOCKER_PRIVATE_REGISTRY** | Sim | 1 | Para o período de tempo da visualização pública restringido, esse valor deve ser definido como 1. |
| **CONTROLLER_USERNAME** | Sim | N/D | O nome de usuário para o administrador de cluster. |
| **CONTROLLER_PASSWORD** | Sim | N/D | A senha para o administrador de cluster. |
| **KNOX_PASSWORD** | Sim | N/D | A senha do usuário do Knox. |
| **MSSQL_SA_PASSWORD** | Sim | N/D | A senha do usuário de SA para a instância mestre do SQL. |
| **USE_PERSISTENT_VOLUME** | Não | true | `true` Para usar declarações de Volume persistente Kubernetes para o armazenamento de pod.  `false` Para usar o armazenamento efêmero host para o armazenamento de pod. Consulte a [persistência de dados](concept-data-persistence.md) artigo para obter mais detalhes. Se você implantar o cluster de big data no minikube do SQL Server e USE_PERSISTENT_VOLUME = true, você deve definir o valor para `STORAGE_CLASS_NAME=standard`. |
| **STORAGE_CLASS_NAME** | Não | padrão | Se `USE_PERSISTENT_VOLUME` é `true` isso indica o nome de classe de armazenamento Kubernetes para usar. Consulte a [persistência de dados](concept-data-persistence.md) artigo para obter mais detalhes. Se você implantar o cluster de big data no minikube do SQL Server, o nome de classe de armazenamento padrão é diferente e você deve substituí-la definindo `STORAGE_CLASS_NAME=standard`. |
| **MASTER_SQL_PORT** | Não | 31433 | A porta de TCP/IP que a instância mestre do SQL escuta na rede pública. |
| **KNOX_PORT** | Não | 30443 | A porta de TCP/IP Knox Apache ouve na rede pública. |
| **GRAFANA_PORT** | Não | 30888 | A porta de TCP/IP que o aplicativo de monitoramento de Grafana escuta na rede pública. |
| **KIBANA_PORT** | Não | 30999 | A porta de TCP/IP que o aplicativo de pesquisa de log do Kibana escuta na rede pública. |

> [!IMPORTANT]
>1. Durante o período da visualização privada limitada, as credenciais para o registro privado do Docker serão fornecidas para você após a separação sua [registro EAP](https://aka.ms/eapsignup).
>1. Para um cluster local criada com **kubeadm**, o valor da variável de ambiente `CLUSTER_PLATFORM` é `kubernetes`. Além disso, quando `USE_PERSISTENT_VOLUME=true`, você deve pré-provisionar uma classe de armazenamento do Kubernetes e passá-lo por meio do usando o `STORAGE_CLASS_NAME`.
>1. Certifique-se de que encapsular as senhas entre aspas duplas se ele contiver caracteres especiais. Você pode definir o MSSQL_SA_PASSWORD para que você quiser, mas certifique-se de que eles são suficientemente complexos e não usam o `!`, `&` ou `'` caracteres. Observe que os delimitadores de aspas duplas funcionam somente em comandos de bash.
>1. O nome do cluster deve ser caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o cluster do nome especificado.
>1. O **SA** conta é um administrador do sistema na instância do SQL Server Master que é criada durante a instalação. Após a criação de seu contêiner do SQL Server, a variável de ambiente MSSQL_SA_PASSWORD especificada é detectável executando echo MSSQL_SA_PASSWORD $ no contêiner. Para fins de segurança, altere sua senha de SA, de acordo com práticas recomendadas documentadas [aqui](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Definir variáveis de ambiente necessárias para implantar um cluster de big data é diferente dependendo se você estiver usando o cliente Windows ou Linux.  Escolha as etapas a seguir dependendo de qual sistema operacional você está usando.

Inicializar as variáveis de ambiente a seguir, eles são necessários para implantar o cluster:

### <a name="windows"></a>Windows

Usando uma janela CMD (não PowerShell), configure as seguintes variáveis de ambiente. Não use aspas ao redor dos valores.

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

Inicialize as variáveis de ambiente a seguir. No bash, você pode usar aspas em torno de cada valor.

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Configurações do Minikube

Se você estiver implantando em minikube e `USE_PERSISTENT_VOLUME=true` (padrão), você também deve substituir o valor padrão para `STORAGE_CLASS_NAME` variável de ambiente.

Use o seguinte comando no Windows para implantações do minikube:

```cmd
SET STORAGE_CLASS_NAME=standard
```

Use o seguinte comando no Linux para implantações do minikube:

```bash
export STORAGE_CLASS_NAME=standard
```

Como alternativa, você pode suprimir usando volumes persistentes em minikube definindo `USE_PERSISTENT_VOLUME=false`.

### <a name="kubadm-settings"></a>Configurações de Kubadm

Se você estiver implantando com kubeadm em seu próprio máquinas físicas ou virtuais, você deve pré-provisionar uma classe de armazenamento do Kubernetes e passá-lo por meio do usando o `STORAGE_CLASS_NAME`. Como alternativa, você pode suprimir usando volumes persistentes definindo `USE_PERSISTENT_VOLUME=false`. Para obter mais informações sobre o armazenamento persistente, consulte [persistência de dados com o SQL Server, o cluster de big data no Kubernetes](concept-data-persistence.md).

## <a name="deploy-sql-server-big-data-cluster"></a>Implantar o cluster de Big Data do SQL Server

A API de criação do cluster é usada para inicializar o namespace do Kubernetes e implantar os pods de aplicativo para o namespace. Para implantar o cluster de big data do SQL Server no cluster do Kubernetes, execute o seguinte comando:

```bash
mssqlctl create cluster <your-cluster-name>
```

Durante a inicialização do cluster, a janela de comando do cliente produzirá o status da implantação. Durante o processo de implantação, você deverá ver uma série de mensagens em que ele está aguardando o pod do controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Depois de 10 a 20 minutos, você deve ser notificado se o pod de controlador está em execução:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.222.222.222:30080
```

> [!IMPORTANT]
> Toda a implantação pode levar muito tempo devido ao tempo necessário para baixar as imagens de contêiner para os componentes do cluster de big data. No entanto, ele não deve levar várias horas. Se você estiver tendo problemas com sua implantação, consulte o [solução de problemas](#troubleshoot) seção deste artigo para saber como monitorar e inspecionar a implantação.

Quando a implantação for concluída, a saída notifica você de sucesso:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> Obter a instância mestre do SQL Server e os endereços IP do cluster de big data do SQL Server

Depois que o script de implantação foi concluída com êxito, você pode obter o endereço IP da instância mestre do SQL Server usando as etapas descritas abaixo. Você usará esse endereço IP e porta número 31433 para se conectar a instância mestre do SQL Server (por exemplo:  **\<endereço ip\>, 31433**). Da mesma forma, para o IP de cluster de big data do SQL Server. Todos os pontos de extremidade do cluster são descritos no guia pontos de extremidade de serviço no Portal de administração do Cluster. Você pode usar o Portal de administração de Cluster para monitorar a implantação. Você pode acessar o portal usando o IP endereço e porta número externa para o `service-proxy-lb` (por exemplo: **https://\<endereço ip\>: 30777/portal**). As credenciais para acessar o portal de administração é os valores de `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variáveis de ambiente fornecidas acima.

### <a name="aks"></a>AKS

Se você estiver usando o AKS, o Azure fornece o serviço de Balanceador de carga do Azure. Execute o seguinte comando:

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc service-security-lb -n <your-cluster-name>
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

Procure os **External-IP** valor atribuído ao serviço. Em seguida, conecte-se à instância mestre do SQL Server usando o endereço IP na porta 31433 (Ex:  **\<endereço ip\>, 31433**) e para o SQL Server grandes dados cluster ponto de extremidade usando o external-IP para `service-security-lb` service. 

### <a name="minikube"></a>Minikube

Se você estiver usando o Minikube, você precisa executar o seguinte comando para obter o endereço IP que você precisa para se conectar ao. Além de IP, especifique a porta para o ponto de extremidade que você precisa para se conectar ao. Para obter todos os pontos de extremidade serviço para 

```bash
minikube ip
```

Independentemente da plataforma você está executando o cluster Kubernetes, para obter todos os pontos de serviço implantados para o cluster, execute o comando a seguir:
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> Atualizar para uma nova versão

Atualmente, a única maneira de atualizar um cluster de big data para uma nova versão é remover e recriar o cluster manualmente. Cada versão tem uma versão exclusiva do **mssqlctl** que não é compatível com a versão anterior. Além disso, se tiver um cluster mais antigo baixar uma imagem em um novo nó, a imagem mais recente não ficará compatível com as imagens mais antigas no cluster. Para atualizar para a versão mais recente, use as seguintes etapas:

1. Antes de excluir o cluster antigo, fazer backup dos dados na instância mestre do SQL Server e no HDFS. Para a instância mestre do SQL Server, você pode usar [SQL Server backup e restauração](data-ingestion-restore-databse.md). Para o HDFS, você [pode copiar os dados com **curl**](data-ingestion-curl.md).

1. Excluir o cluster antigo com o `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl delete cluster <old-cluster-name>
   ```

1. Instale a versão mais recente do **mssqlctl**.
   
   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para **mssqlctl** alterações. Mesmo se você instalou anteriormente **mssqlctl**, você deverá reinstalar do caminho mais recente antes de criar o novo cluster.

1. Instalar a versão mais recente usando as instruções na [implantar seção](#deploy) deste artigo. 

## <a id="troubleshoot"></a> Monitorando e Solucionando problemas

Para monitorar ou solucionar problemas de uma implantação, use **kubectl** para inspecionar o status do cluster e para detectar possíveis problemas. A qualquer momento durante a implantação, você pode abrir uma janela de comando diferente para executar os testes a seguir.

1. Inspecione o status dos pods no cluster.

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   Durante a implantação, pods com um **STATUS** dos **ContainerCreating** ainda estão surgindo. Se a implantação trava por qualquer motivo, isso pode dar uma ideia em que o problema pode ser. Examine também os **pronto** coluna. Isso informa quantos contêineres começaram no pod. Observe que as implantações podem levar trinta minutos ou mais dependendo da sua rede e configuração. Grande parte desse tempo é gasto baixando as imagens de contêiner para diferentes componentes. A tabela a seguir mostra a saída de exemplo editado de dois contêineres durante a implantação:

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. Descreva um pod individual para obter mais detalhes. O comando a seguir inspeciona o `mssql-storage-pool-default-0` pod.

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   Isso gera informações detalhadas sobre o pod, incluindo eventos recentes. Se tiver ocorrido um erro, você pode encontrar, às vezes, o erro aqui.

1. Recupere os logs para contêineres em execução em um pod. O comando a seguir recupera os logs para todos os contêineres em execução no pod denominado `mssql-storage-pool-default-0` e gera como saída para um nome de arquivo `pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. Examine os serviços de cluster durante e após uma implantação com o seguinte comando:

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   Esses serviços oferecem suporte a conexões internas e externas para o cluster de big data. Conexões externas, são usados os seguintes serviços:

   | Serviço | Descrição |
   |---|---|
   | **ponto de extremidade de mestre de pool** | Fornece acesso para a instância mestre.<br/>(**EXTERNAL-IP, 31433** e o **SA** usuário) |
   | **serviço mssql-controlador lb**<br/>**serviço mssql-controlador nodeport** | Dá suporte a ferramentas e clientes que gerenciam o cluster. |
   | **serviço de proxy de lb**<br/>**serviço de proxy de nodeport** | Fornece acesso para o [Portal de administração de Cluster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**: 30777/portal)|
   | **serviço de segurança de lb**<br/>**serviço de segurança de nodeport** | Fornece acesso para o gateway HDFS/Spark.<br/>(**EXTERNAL-IP** e o **raiz** usuário) |

   > [!NOTE]
   > Os nomes de serviço podem variar dependendo do seu ambiente de Kubernetes. Ao implantar no serviço de Kubernetes do Azure (AKS), os nomes de serviço terminam com **-lb**. Para implantações minikube e kubeadm, os nomes de serviço terminam com **nodeport -**.

1. Use o [Portal de administração de Cluster](cluster-admin-portal.md) para monitorar a implantação na **implantação** guia. Você precisa esperar para o **serviço de proxy de lb** início antes de acessar esse portal, portanto, ele não estará disponível no início de uma implantação do serviço.

> [!TIP]
> Para obter mais informações sobre como solucionar problemas do cluster, consulte [comandos Kubectl para monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

## <a name="next-steps"></a>Próximas etapas

Experimente alguns dos novos recursos e Aprenda [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).
