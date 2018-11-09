---
title: Implantar um cluster de big data do SQL Server | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: efa3d06feb138445c3e55e5d2ea3da7e60f3da20
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269551"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Início rápido: Implantar um cluster de big data do SQL Server no serviço de Kubernetes do Azure (AKS)

Instale o cluster de big data do SQL Server no AKS em uma configuração padrão adequada para ambientes de desenvolvimento/teste. Além de uma instância do SQL Master, o cluster inclui duas instâncias de pool de armazenamento, uma instância de pool de dados e computação de uma instância de pool. Os dados persistem usando volumes persistentes Kubernetes que usam classes de armazenamento de padrão do AKS. Para personalizar ainda mais a sua configuração, consulte as variáveis de ambiente na [diretrizes de implantação](deployment-guidance.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisites

Este início rápido exige que você já tenha configurado um cluster do AKS com a versão mínima de v 1.10. Para obter mais informações, consulte o [implantar no AKS](deploy-on-aks.md) guia.

No computador em que você está usando para executar os comandos para instalar o cluster de big data do SQL Server, instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). Cluster de big data do SQL Server requer uma versão mínima de 1,10 para Kubernetes, para o servidor e cliente (kubectl). Para instalar o kubectl, consulte [instalar kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl). 

Para instalar o **mssqlctl** ferramenta de CLI para gerenciar o big data do SQL Server do cluster no computador cliente, você deve instalar primeiro [Python](https://www.python.org/downloads/) v3.0 versão mínima e [pip3](https://pip.pypa.io/en/stable/installing/). `pip` já está instalado, se você estiver usando uma versão do Python pelo menos 3.4 obtido por download [python.org](https://www.python.org/).

## <a name="verify-aks-configuration"></a>Verificar a configuração do AKS

Quando você tiver implantado o cluster do AKS, você poderá executar o comando kubectl para exibir a configuração de cluster abaixo. Certifique-se de que kubectl está apontada para o contexto do cluster correto.

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool"></a>Instalar a ferramenta de gerenciamento de CLI mssqlctl

Execute o comando abaixo para instalar **mssqlctl** ferramenta no computador cliente. O comando funciona em um Windows e um cliente Linux, mas certifique-se de que esteja executando-o em uma janela cmd que é executado com privilégios administrativos no Windows ou um prefixo com `sudo` no Linux:

```
pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.1 mssqlctl  
```

> [!IMPORTANT]
> Se você instalou uma versão anterior, você deve excluir o cluster *antes de* Atualizando **mssqlctl** e instalar a nova versão. Para obter mais informações, consulte [atualizar para uma nova versão](deployment-guidance.md#upgrade).

> [!TIP]
> Se **mssqlctl** não instalado corretamente, examine as etapas de pré-requisito no artigo [instalar mssqlctl](deployment-guidance.md#mssqlctl).

## <a name="define-environment-variables"></a>Definir variáveis de ambiente

Definir variáveis de ambiente necessárias para a implantação de cluster de big data ligeiramente difere dependendo se você estiver usando o cliente Windows ou Linux/macOS.  Escolha as etapas a seguir dependendo de qual sistema operacional você está usando.

Antes de continuar, observe as seguintes diretrizes importantes:

- No [janela de comando](http://docs.microsoft.com/visualstudio/ide/reference/command-window), aspas são incluídas nas variáveis de ambiente. Se você usar aspas para encapsular uma senha, as aspas são incluídas na senha.
- No bash, aspas não são incluídas na variável. Nossos exemplos usam aspas duplas `"`.
- Você pode definir a senha de variáveis de ambiente para que você quiser, mas certifique-se de que eles são suficientemente complexos e não usam o `!`, `&`, ou `'` caracteres.
- Na versão CTP 2.1, não altere as portas padrão.
- O `sa` conta é um administrador do sistema na instância do SQL Server Master que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente `MSSQL_SA_PASSWORD` especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua `sa` senha, de acordo com práticas recomendadas documentadas [aqui](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Inicialize as variáveis de ambiente a seguir.  Eles são necessários para implantar um cluster de big data:

### <a name="windows"></a>Windows

Usando uma janela de comando (não PowerShell), configure as seguintes variáveis de ambiente:

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

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

### <a name="linuxmacos"></a>Linux/macOS

Inicialize as variáveis de ambiente a seguir:

```bash
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

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

> [!NOTE]
> Durante a visualização pública limitada, credenciais do Docker para baixar as imagens de cluster de big data do SQL Server são fornecidas para cada cliente pela Microsoft. Para solicitar acesso, registre [aqui](https://aka.ms/eapsignup)e especifique seu interesse para tentar a clusters de grandes dados do SQL Server.

## <a name="deploy-a-big-data-cluster"></a>Implantar um cluster de big data

Para implantar um cluster de big data 2019 CTP 2.1 do SQL Server no cluster do Kubernetes, execute o seguinte comando:

```bash
mssqlctl create cluster <name of your cluster>
```

> [!NOTE]
> O nome do seu cluster precisa ter caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes para o cluster de big data serão criados em um namespace com o mesmo nome que o cluster do nome especificado.


A janela de comando ou shell retorna o status da implantação. Você também pode verificar o status da implantação executando estes comandos em uma janela cmd diferentes:

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

Você pode ver um status mais granular e a configuração para cada pod, executando:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

Quando o pod de controlador estiver em execução, você pode usar o Portal de administração de Cluster para monitorar a implantação. Você pode acessar o portal usando o IP endereço e porta número externa para o `service-proxy-lb` (por exemplo: **https://\<endereço ip\>: 30777**). As credenciais para acessar o portal de administração é os valores de `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variáveis de ambiente fornecidas acima.

Você pode obter o endereço IP do serviço do serviço de proxy de lb executando este comando em uma janela de bash ou cmd:

```bash
kubectl get svc service-proxy-lb -n <name of your cluster>
```

> [!NOTE]
> Você verá um aviso de segurança ao acessar a página da web, como estamos usando certificados gerados automaticamente SSL. Em futuras versões, fornecemos a capacidade de fornecer seus próprios certificados autoassinados.
 

## <a name="connect-to-the-big-data-cluster"></a>Conectar-se para o cluster de big data

Depois que o script de implantação foi concluída com êxito, você pode obter o endereço IP da instância mestre do SQL Server e os pontos de extremidade HDFS/Spark usando as etapas descritas abaixo. Todos os pontos de extremidade do cluster são exibidos na seção de pontos de extremidade de serviço no Portal de administração do Cluster também para facilitar a referência.

O Azure fornece o serviço de Balanceador de carga do Azure no AKS. Execute o seguinte comando em um cmd ou janela de bash:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
```

Procure os **External-IP** valor que é atribuído aos serviços. Conectar-se à instância mestre do SQL Server usando o endereço IP para o `service-master-pool-lb` na porta 31433 (Ex:  **\<endereço ip\>, 31433**) e para o SQL Server grandes dados cluster ponto de extremidade usando o external-IP para o `service-security-lb` serviço.   Que dados grandes ponto de extremidade de cluster é onde você pode interagir com o HDFS e enviar trabalhos do Spark por meio do Knox.

## <a name="sample-deployment-script"></a>Exemplo de script de implantação

Para um script de python de exemplo que implanta o cluster de big data do AKS e o SQL Server, consulte [implantar um cluster de big data no serviço de Kubernetes do Azure (AKS) do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="next-steps"></a>Próximas etapas

Agora que o cluster de big data do SQL Server é implantado, experimente alguns dos novos recursos:

> [!div class="nextstepaction"]
> [Como usar blocos de anotações na visualização do SQL Server de 2019](notebooks-guidance.md)
