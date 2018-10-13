---
title: Como implantar um cluster do SQL Server Big Data no Kubernetes | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/08/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 02a1aa7299173315e4f4d6a60eae5f166e8fcdfe
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877889"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>Como implantar um cluster de Big Data do SQL Server no Kubernetes

Cluster de Big Data do SQL Server pode ser implantado como contêineres do docker em um cluster Kubernetes. Isso é uma visão geral das etapas de instalação e configuração:

- Configurar o cluster Kubernetes em uma única VM, o cluster de VMs ou no serviço de contêiner do Azure
- Instalar a ferramenta de configuração de cluster `mssqlctl` no computador cliente
- Implantar um cluster de Big Data do SQL Server em um cluster Kubernetes

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Pré-requisitos de cluster de Kubernetes

Cluster de Big Data do SQL Server requer uma versão de v 1.10 mínimo para o Kubernetes, para o servidor e cliente. Para instalar uma versão específica no cliente kubectl, consulte [instalar kubectl binário por meio de rotação](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl).  Versões mais recentes do minikube e AKS são pelo menos 1.10. Para o AKS, será necessário usar `--kubernetes-version` parâmetro para especificar uma versão diferente do padrão.

> [!NOTE]
> Observe que as versões de servidor e cliente Kubernetes devem ser + 1 ou -1, versão secundária. Para obter mais informações, consulte [Kubernetes suporte para versões e componente distorção](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Instalação de cluster do Kubernetes

Se você já tiver um cluster do Kubernetes que atenda aos acima pré-requisitos, você poderá pular diretamente para o [etapa de implantação](#deploy). Esta seção pressupõe uma compreensão básica dos conceitos de Kubernetes.  Para obter informações detalhadas sobre Kubernetes, consulte o [documentação do Kubernetes](https://kubernetes.io/docs/home).

Você pode optar por implantar Kubernetes em qualquer uma das três maneiras:

| Implante Kubernetes em: | Description |
|---|---|
| **Minikube** | Um cluster do Kubernetes de nó único em uma VM. |
| **Serviços de Kubernetes do Azure (AKS)** | Um serviço gerenciado de contêiner do Kubernetes no Azure. |
| **Várias VMs** | Um cluster Kubernetes implantado em suas VMs usando kubeadm |

Para obter orientação sobre como configurar uma destas opções de cluster do Kubernetes para o cluster de Big Data do SQL Server, consulte um dos seguintes artigos:

   - [Configurar o Minikube](deploy-on-minikube.md)
   - [Configurar o Kubernetes no serviço de Kubernetes do Azure](deploy-on-aks.md)

## <a id="deploy"></a> Implantar um cluster de Big Data do SQL Server

Depois de configurar o cluster Kubernetes, você pode prosseguir com a implantação de cluster de Big Data do SQL Server. Para implantar um cluster de big data com todas as configurações padrão para um ambiente de desenvolvimento/teste, siga as instruções neste artigo:

[Guia de início rápido: Implantar o SQL Server, o Cluster de Big Data no Kubernetes](quickstart-big-data-cluster-deploy.md)

Se você quiser personalizar a configuração de cluster de big data, de acordo com suas necessidades de carga de trabalho, siga o próximo conjunto de instruções.

## <a name="verify-kubernetes-configuration"></a>Verifique se a configuração do kubernetes

Execute o comando kubectl para exibir a configuração de cluster abaixo. Certifique-se de que kubectl está apontada para o contexto do cluster correto.

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool-for-sql-server-big-data-cluster"></a>Instalar a ferramenta de gerenciamento de CLI mssqlctl para cluster de Big Data do SQL Server
`mssqlctl` um utilitário de linha de comando é escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de big data por meio de APIs REST. A versão do Python mínima necessária é v 3.5. Você também deve ter `pip` que é usado para baixar e instalar `mssqlctl` ferramenta. Em um cliente Windows, você pode baixar o pacote do Python necessário da [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Para python3.5.3 e posterior, pip3 também é instalado quando você instala o Python. Quando você o instala não é possível selecionar a adicionar ao caminho. Em seguida, você pode encontrar onde o pip3 é localizado e adicioná-lo manualmente ao caminho.
No Linux (WSL ou Ubuntu cliente por exemplo), esses comandos instalará a última versão 3.5 do Python e pip:

```bash
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
sudo pip3 install --upgrade pip
```

> [!NOTE]
Se a instalação do Python está falta a `requests` pacote, você deve instalar `requests` usando `python -m pip install requests`. Se você já tiver um `requests` pacote instalado, verifique se você tem a versão mais recente, executando `python -m pip install requests --upgrade`.

Execute o comando para instalar o msqlctl abaixo:

```bash
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
```

## <a name="define-environment-variables"></a>Definir variáveis de ambiente

A configuração do cluster pode ser personalizada usando um conjunto de variáveis de ambiente que são passados para o `mssqlctl create cluster` comando. A maioria das variáveis de ambiente é opcional com avalues padrão, conforme descrito abaixo. Observe que há variáveis de ambiente, como as credenciais que exigem entrada do usuário.

| Variável de ambiente | Obrigatório | Valor padrão | Description |
|---|---|---|---|
| **ACCEPT_EULA** | Sim | N/A | Aceite o contrato de licença do SQL Server (por exemplo, ' Y').  |
| **CLUSTER_NAME** | Sim | N/A | O nome do namespace para implantar o cluster de Big Data do SQL Server em Kubernetes. |
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
| **USE_PERSISTENT_VOLUME** | não | true | `true` Para usar declarações de Volume persistente Kubernetes para o armazenamento de pod.  `false` Para usar o armazenamento efêmero host para o armazenamento de pod. Consulte a [persistência de dados](concept-data-persistence.md) tópico para obter mais detalhes. |
| **STORAGE_CLASS_NAME** | não | padrão | Se `USE_PERSISTENT_VOLUME` é `true` isso indica o nome de classe de armazenamento Kubernetes para usar. Consulte a [persistência de dados](concept-data-persistence.md) tópico para obter mais detalhes. |
| **MASTER_SQL_PORT** | não | 31433 | A porta de TCP/IP que a instância mestre do SQL escuta na rede pública. |
| **KNOX_PORT** | não | 30443 | A porta de TCP/IP Knox Apache ouve na rede pública. |
| **GRAFANA_PORT** | não | 30888 | A porta de TCP/IP que o aplicativo de monitoramento de Grafana escuta na rede pública. |
| **KIBANA_PORT** | não | 30999 | A porta de TCP/IP que o aplicativo de pesquisa de log do Kibana escuta na rede pública. |



> [!IMPORTANT]
>1. Durante o período da visualização privada limitada, as credenciais para o registro privado do Docker serão fornecidas para você após a separação sua [registro EAP](https://aka.ms/eapsignup).
>1. Para um cluster local criado com kubeadm, o valor da variável de ambiente `CLUSTER_PLATFORM` é `kubernetes`. Além disso, quando USE_PERSISTENT_STORAGE = true, você deve provisionar previamente uma classe de armazenamento do Kubernetes e passá-lo por meio do usando o STORAGE_CLASS_NAME.
>1. Certifique-se de que encapsular as senhas entre aspas duplas se ele contiver caracteres especiais. Você pode definir o MSSQL_SA_PASSWORD para que você quiser, mas certifique-se de que eles são suficientemente complexos e não usam o `!`, `&` ou `‘` caracteres. Observe que os delimitadores de aspas duplas funcionam somente em comandos de bash.
>1. O nome do cluster deve ser caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o cluster do nome especificado.
>1. O **SA** conta é um administrador do sistema na instância do SQL Server Master que é criada durante a instalação. Após a criação de seu contêiner do SQL Server, a variável de ambiente MSSQL_SA_PASSWORD especificada é detectável executando echo MSSQL_SA_PASSWORD $ no contêiner. Para fins de segurança, altere sua senha de SA, de acordo com práticas recomendadas documentadas [aqui](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Definir variáveis de ambiente necessárias para implantar Aris cluster difere dependendo se você estiver usando o cliente Windows ou Linux.  Escolha as etapas a seguir dependendo de qual sistema operacional você está usando.

Inicializar as variáveis de ambiente a seguir, eles são necessários para implantar o cluster:

### <a name="windows"></a>Windows

Usando uma janela CMD (não PowerShell), configure as seguintes variáveis de ambiente:

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username>
SET DOCKER_PASSWORD=<your password>
SET DOCKER_EMAIL=<your Docker email, use same as username provided>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

Inicialize as variáveis de ambiente a seguir:

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME=<controller_admin_name – can be anything>
export CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
export KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
export MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

export DOCKER_REGISTRY=private-repo.microsoft.com
export DOCKER_REPOSITORY=mssql-private-preview
export DOCKER_USERNAME=<your username>
export DOCKER_PASSWORD=<your password>
export DOCKER_EMAIL=<your Docker email, use same as username provided>
export DOCKER_PRIVATE_REGISTRY="1"
```

## <a name="deploy-sql-server-big-data-cluster"></a>Implantar um cluster de Big Data do SQL Server

A API de criação do cluster é usada para inicializar o namespace do Kubernetes e implantar os pods de aplicativo para o namespace. Para implantar o cluster de Big Data do SQL Server no cluster do Kubernetes, execute o seguinte comando:

```bash
mssqlctl create cluster <name of your cluster>
```

Durante a inicialização do cluster, a janela de comando do cliente será a saída o status da implantação. Você também pode verificar o status da implantação executando estes comandos em uma janela cmd diferentes:

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

## <a id="masterip"></a> Obter a instância mestre do SQL Server e os endereços IP do cluster de Big Data do SQL Server

Depois que o script de implantação foi concluída com êxito, você pode obter o endereço IP da instância mestre do SQL Server usando as etapas descritas abaixo. Você usará esse endereço IP e porta número 31433 para se conectar a instância mestre do SQL Server (por exemplo:  **\<endereço ip\>, 31433**). Da mesma forma, para o IP de cluster de Big Data do SQL Server. Todos os pontos de extremidade do cluster são descritos no guia pontos de extremidade de serviço no Portal de administração do Cluster. Você pode usar o Portal de administração de Cluster para monitorar a implantação. Você pode acessar o portal usando o IP endereço e porta número externa para o `service-proxy-lb` (por exemplo: **https://\<endereço ip\>: 30777**). As credenciais para acessar o portal de administração é os valores de `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variáveis de ambiente fornecidas acima.

### <a name="aks"></a>AKS

Se você estiver usando o AKS, o Azure fornece o serviço de Balanceador de carga do Azure. Execute o seguinte comando:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

Procure os **External-IP** valor atribuído ao serviço. Em seguida, conecte-se à instância mestre do SQL Server usando o endereço IP na porta 31433 (Ex:  **\<endereço ip\>, 31433**) e para Big Data do SQL Server do ponto de extremidade usando o external-IP para cluster `service-security-lb` service. 

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

Depois de implantar com êxito os dados do SQL Server grande cluster Kubernetes, [instalar as ferramentas de dados grandes](deploy-big-data-tools.md) e experimentar alguns dos novos recursos e saiba [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).
