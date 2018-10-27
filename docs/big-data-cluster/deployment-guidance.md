---
title: Como implantar grandes de dados do SQL Server clusters no Kubernetes | Microsoft Docs
description: Aprenda a implantar clusters de big data de 2019 do SQL Server (versão prévia) no Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/08/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: de19577b4a83bc10875bf56f4c0f2924828a00ea
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051178"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>Como implantar o SQL Server, o cluster de big data no Kubernetes

Cluster de big data do SQL Server pode ser implantado como contêineres do docker em um cluster Kubernetes. Isso é uma visão geral das etapas de instalação e configuração:

- Configure o cluster Kubernetes em uma única VM, o cluster de VMs ou no serviço de Kubernetes do Azure (AKS).
- Instalar a ferramenta de configuração de cluster **mssqlctl** no computador cliente.
- Implante um cluster de big data do SQL Server em um cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Pré-requisitos de cluster de Kubernetes

Cluster de big data do SQL Server requer uma versão de v 1.10 mínimo para o Kubernetes, para o servidor e cliente. Para instalar uma versão específica no cliente kubectl, consulte [instalar kubectl binário por meio de rotação](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl).  Versões mais recentes do minikube e AKS são pelo menos 1.10. Para o AKS, você precisará usar `--kubernetes-version` parâmetro para especificar uma versão diferente do padrão.

> [!NOTE]
> Observe que as versões de servidor e cliente Kubernetes devem ser + 1 ou -1, versão secundária. Para obter mais informações, consulte [Kubernetes suporte para versões e componente distorção](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Instalação de cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atenda aos acima pré-requisitos, você poderá pular diretamente para o [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos de Kubernetes.  Para obter informações detalhadas sobre Kubernetes, consulte o [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar Kubernetes em qualquer uma das três maneiras:

| Implante Kubernetes em: | Description |
|---|---|
| **Minikube** | Um cluster do Kubernetes de nó único em uma VM. |
| **Serviços de Kubernetes do Azure (AKS)** | Um serviço gerenciado de contêiner do Kubernetes no Azure. |
| **Vários computadores** | Um cluster Kubernetes implantado em máquinas físicas ou virtuais usando **kubeadm** |

Para obter orientação sobre como configurar uma destas opções de cluster do Kubernetes para um cluster de big data do SQL Server, consulte um dos seguintes artigos:

   - [Configurar o Minikube](deploy-on-minikube.md)
   - [Configurar o Kubernetes no serviço de Kubernetes do Azure](deploy-on-aks.md)
   - [Configurar o Kubernetes em várias máquinas com kubeadm](deploy-with-kubeadm.md)
   
> [!TIP]
> Para um script de python de exemplo que implanta o cluster de big data do AKS e o SQL Server, consulte [implantar um cluster de big data no serviço de Kubernetes do Azure (AKS) do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a id="deploy"></a> Implantar um cluster de big data do SQL Server

Depois de configurar o cluster Kubernetes, você pode prosseguir com a implantação de cluster de big data do SQL Server. Para implantar um cluster de big data no Azure com todas as configurações padrão para um ambiente de desenvolvimento/teste, siga as instruções neste artigo:

[Início rápido: Implantar um cluster de big data do SQL Server no Kubernetes](quickstart-big-data-cluster-deploy.md)

Se você quiser personalizar a configuração de cluster de big data acordo com suas necessidades de carga de trabalho, siga o próximo conjunto de instruções.

## <a name="verify-kubernetes-configuration"></a>Verifique se a configuração do kubernetes

Execute o **kubectl** comando para exibir a configuração do cluster. Certifique-se de que kubectl está apontada para o contexto do cluster correto.

```bash
kubectl config view
```

## <a id="mssqlctl"></a> Instalar mssqlctl

**mssqlctl** é um utilitário de linha de comando escrito em Python que permite que os administradores para inicializar e gerenciar o cluster de big data por meio de APIs REST de cluster. A versão do Python mínima necessária é v 3.5. Você também deve ter `pip` que é usado para baixar e instalar **mssqlctl** ferramenta. 

### <a name="windows-mssqlctl-installation"></a>Instalação do Windows mssqlctl

1. Em um cliente Windows, baixe o pacote Python necessário [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Para python3.5.3 e posterior, pip3 também é instalado quando você instala o Python. 

   > [!TIP] 
   > Ao instalar o Python3, selecione Adicionar Python ao seu caminho. Se você não fizer isso, você pode posteriormente localizar onde se encontra pip3 e adicioná-lo manualmente ao seu caminho.

1. Certifique-se de que você tenha a versão mais recente **solicitações** pacote.

   ```cmd
   python -m pip install requests
   python -m pip install requests --upgrade
   ```

1. Instale **mssqlctl** com o seguinte comando:

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

### <a name="linux-mssqlctl-installation"></a>Instalação do Linux mssqlctl

No Linux, você deve instalar o **python3** e **pip python3** pacotes e, em seguida, execute `sudo pip3 install --upgrade pip`. Isso instala a versão 3.5 mais recente do Python e pip. O exemplo a seguir mostra como esses comandos funcionaria para Ubuntu (se você estiver usando outra plataforma, modifique os comandos para o Gerenciador de pacotes):

1. Instale os pacotes Python necessários:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip && /
   sudo -H pip3 install --upgrade pip
   ```

1. Certifique-se de que você tenha a versão mais recente **solicitações** pacote.

   ```bash
   sudo -H python3 -m pip install requests
   sudo -H python3 -m pip install requests --upgrade
   ```

1. Instale **mssqlctl** com o seguinte comando:

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

## <a name="define-environment-variables"></a>Definir variáveis de ambiente

A configuração do cluster pode ser personalizada usando um conjunto de variáveis de ambiente que são passados para o `mssqlctl create cluster` comando. A maioria das variáveis de ambiente é opcional com valores padrão, conforme descrito abaixo. Observe que há variáveis de ambiente, como as credenciais que exigem entrada do usuário.

| Variável de ambiente | Obrigatório | Valor padrão | Description |
|---|---|---|---|
| **ACCEPT_EULA** | Sim | N/A | Aceite o contrato de licença do SQL Server (por exemplo, ' Y').  |
| **CLUSTER_NAME** | Sim | N/A | O nome do namespace para implantar o SQLServer cluster de big data em Kubernetes. |
| **CLUSTER_PLATFORM** | Sim | N/A | A plataforma em que o cluster Kubernetes é implantado. Pode ser `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | não | 1 | O número de réplicas de pool de computação para criar. No CTP 2.0 apenas com o valor permitido é 1. |
| **CLUSTER_DATA_POOL_REPLICAS** | não | 2 | O número de dados do pool réplicas para criar. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | não | 2 | O número de réplicas de pool de armazenamento para criar. |
| **DOCKER_REGISTRY** | Sim | TBD | O registro privado onde as imagens usadas para implantar o cluster são armazenadas. |
| **DOCKER_REPOSITORY** | Sim | TBD | O repositório privado dentro do registro acima, onde as imagens são armazenadas.  É necessário durante a versão prévia pública controlada. |
| **DOCKER_USERNAME** | Sim | N/A | O nome de usuário para acessar as imagens de contêiner, caso eles são armazenados em um repositório privado. É necessário durante a versão prévia pública controlada. |
| **DOCKER_PASSWORD** | Sim | N/A | A senha para acessar o repositório privado acima. É necessário durante a versão prévia pública controlada.|
| **DOCKER_EMAIL** | Sim | N/A | O email associado com o repositório privado acima. É necessário para a duração da visualização privada restrita. |
| **DOCKER_IMAGE_TAG** | não | mais recente | O rótulo usado para marcar as imagens. |
| **DOCKER_IMAGE_POLICY** | não | Always | Sempre force um pull das imagens.  |
| **DOCKER_PRIVATE_REGISTRY** | Sim | 1 | Para o período de tempo da visualização pública restringido, esse valor deve ser definido como 1. |
| **CONTROLLER_USERNAME** | Sim | N/A | O nome de usuário para o administrador de cluster. |
| **CONTROLLER_PASSWORD** | Sim | N/A | A senha para o administrador de cluster. |
| **KNOX_PASSWORD** | Sim | N/A | A senha do usuário do Knox. |
| **MSSQL_SA_PASSWORD** | Sim | N/A | A senha do usuário de SA para a instância mestre do SQL. |
| **USE_PERSISTENT_VOLUME** | não | true | `true` Para usar declarações de Volume persistente Kubernetes para o armazenamento de pod.  `false` Para usar o armazenamento efêmero host para o armazenamento de pod. Consulte a [persistência de dados](concept-data-persistence.md) artigo para obter mais detalhes. Se você implantar o cluster de big data no minikube do SQL Server e USE_PERSISTENT_VOLUME = true, você deve definir o valor para `STORAGE_CLASS_NAME=standard`. |
| **STORAGE_CLASS_NAME** | não | padrão | Se `USE_PERSISTENT_VOLUME` é `true` isso indica o nome de classe de armazenamento Kubernetes para usar. Consulte a [persistência de dados](concept-data-persistence.md) artigo para obter mais detalhes. Se você implantar o cluster de big data no minikube do SQL Server, o nome de classe de armazenamento padrão é diferente e você deve substituí-la definindo `STORAGE_CLASS_NAME=standard`. |
| **MASTER_SQL_PORT** | não | 31433 | A porta de TCP/IP que a instância mestre do SQL escuta na rede pública. |
| **KNOX_PORT** | não | 30443 | A porta de TCP/IP Knox Apache ouve na rede pública. |
| **GRAFANA_PORT** | não | 30888 | A porta de TCP/IP que o aplicativo de monitoramento de Grafana escuta na rede pública. |
| **KIBANA_PORT** | não | 30999 | A porta de TCP/IP que o aplicativo de pesquisa de log do Kibana escuta na rede pública. |

> [!IMPORTANT]
>1. Durante o período da visualização privada limitada, as credenciais para o registro privado do Docker serão fornecidas para você após a separação sua [registro EAP](https://aka.ms/eapsignup).
>1. Para um cluster local criada com **kubeadm**, o valor da variável de ambiente `CLUSTER_PLATFORM` é `kubernetes`. Além disso, quando `USE_PERSISTENT_VOLUME=true`, você deve pré-provisionar uma classe de armazenamento do Kubernetes e passá-lo por meio do usando o `STORAGE_CLASS_NAME`.
>1. Certifique-se de que encapsular as senhas entre aspas duplas se ele contiver caracteres especiais. Você pode definir o MSSQL_SA_PASSWORD para que você quiser, mas certifique-se de que eles são suficientemente complexos e não usam o `!`, `&` ou `‘` caracteres. Observe que os delimitadores de aspas duplas funcionam somente em comandos de bash.
>1. O nome do cluster deve ser caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o cluster do nome especificado.
>1. O **SA** conta é um administrador do sistema na instância do SQL Server Master que é criada durante a instalação. Após a criação de seu contêiner do SQL Server, a variável de ambiente MSSQL_SA_PASSWORD especificada é detectável executando echo MSSQL_SA_PASSWORD $ no contêiner. Para fins de segurança, altere sua senha de SA, de acordo com práticas recomendadas documentadas [aqui](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Definir variáveis de ambiente necessárias para implantar um cluster de big data é diferente dependendo se você estiver usando o cliente Windows ou Linux.  Escolha as etapas a seguir dependendo de qual sistema operacional você está usando.

Inicializar as variáveis de ambiente a seguir, eles são necessários para implantar o cluster:

### <a name="windows"></a>Windows

Usando uma janela CMD (não PowerShell), configure as seguintes variáveis de ambiente. Não use aspas ao redor dos valores.

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
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

export CONTROLLER_USERNAME="<controller_admin_name – can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password – can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password – can be anything, password complexity compliant>"
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
mssqlctl create cluster <name of your cluster>
```

Durante a inicialização do cluster, a janela de comando do cliente produzirá o status da implantação. Você também pode verificar o status da implantação executando estes comandos em uma janela cmd diferentes:

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

Você pode ver um status mais granular e a configuração para cada pod, executando:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

Quando o pod de controlador estiver em execução, você pode aproveitar a guia de implantação no Portal de administração do Cluster para monitorar a implantação.

## <a id="masterip"></a> Obter a instância mestre do SQL Server e os endereços IP do cluster de big data do SQL Server

Depois que o script de implantação foi concluída com êxito, você pode obter o endereço IP da instância mestre do SQL Server usando as etapas descritas abaixo. Você usará esse endereço IP e porta número 31433 para se conectar a instância mestre do SQL Server (por exemplo:  **\<endereço ip\>, 31433**). Da mesma forma, para o IP de cluster de big data do SQL Server. Todos os pontos de extremidade do cluster são descritos no guia pontos de extremidade de serviço no Portal de administração do Cluster. Você pode usar o Portal de administração de Cluster para monitorar a implantação. Você pode acessar o portal usando o IP endereço e porta número externa para o `service-proxy-lb` (por exemplo: **https://\<endereço ip\>: 30777**). As credenciais para acessar o portal de administração é os valores de `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variáveis de ambiente fornecidas acima.

### <a name="aks"></a>AKS

Se você estiver usando o AKS, o Azure fornece o serviço de Balanceador de carga do Azure. Execute o seguinte comando:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

Procure os **External-IP** valor atribuído ao serviço. Em seguida, conecte-se à instância mestre do SQL Server usando o endereço IP na porta 31433 (Ex:  **\<endereço ip\>, 31433**) e para o SQL Server grandes dados cluster ponto de extremidade usando o external-IP para `service-security-lb` service. 

### <a name="minikube"></a>Minikube

Se você estiver usando o Minikube, você precisa executar o seguinte comando para obter o endereço IP que você precisa para se conectar ao. Além de IP, especifique a porta para o ponto de extremidade que você precisa para se conectar ao. Para obter todos os pontos de extremidade serviço para 

```bash
minikube ip
```

Independentemente da plataforma você está executando o cluster Kubernetes, para obter todos os pontos de serviço implantados para o cluster, execute o comando a seguir:
```bash
kubectl get svc -n <name of your cluster>
```

## <a name="next-steps"></a>Próximas etapas

Depois de implantar com êxito o cluster de big data para Kubernetes, do SQL Server [instalar as ferramentas de dados grandes](deploy-big-data-tools.md) e experimentar alguns dos novos recursos e saiba [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).
