---
title: Implantar aplicativos usando o azdata
titleSuffix: SQL Server big data clusters
description: Implante um script Python ou R como um aplicativo no cluster SQL Server 2019 Big Data (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06b76e7eb8eec8db1993ca558a1f57355457c4ad
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419484"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Como implantar um aplicativo no cluster SQL Server Big Data (versão prévia)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar e gerenciar o script R e Python como um aplicativo dentro de um cluster SQL Server 2019 Big Data (versão prévia).

## <a name="whats-new-and-improved"></a>O que há de novo e aprimorado

- Um único utilitário de linha de comando para gerenciar cluster e aplicativo.
- Implantação de aplicativo simplificada ao fornecer controle granular por meio de arquivos de especificação.
- Suporte à Hospedagem de tipos de aplicativos adicionais-SSIS e MLeap (novidade no CTP 2,3)
- [Extensão de vs Code](app-deployment-extension.md) para gerenciar a implantação de aplicativos

Os aplicativos são implantados `azdata` e gerenciados usando o utilitário de linha de comando. Este artigo fornece exemplos de como implantar aplicativos da linha de comando. Para saber como usá-lo em Visual Studio Code consulte [vs Code extensão](app-deployment-extension.md).

Há suporte para os seguintes tipos de aplicativos:
- Aplicativos R e Python (funções, modelos e aplicativos)
- Serviço de MLeap
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster SQL Server 2019 Big Data](deployment-guidance.md)
- [utilitário de linha de comando azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Capacidades

No SQL Server 2019 (versão prévia), você pode criar, excluir, descrever, inicializar, listar executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativo que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata login` | Entrar em um cluster SQL Server Big Data |
|`azdata app create` | Criar aplicativo. |
|`azdata app delete` | Excluir aplicativo. |
|`azdata app describe` | Descreva o aplicativo. |
|`azdata app init` | Início rápido novo esqueleto do aplicativo. |
|`azdata app list` | Listar aplicativo (s). |
|`azdata app run` | Execute o aplicativo. |
|`azdata app update`| Atualizar aplicativo. |

Você pode obter ajuda com o `--help` parâmetro como no exemplo a seguir:

```bash
azdata app create --help
```

As seções a seguir descrevem esses comandos mais detalhadamente.

## <a name="sign-in"></a>Entrar

Antes de implantar ou interagir com aplicativos, primeiro entre no cluster do SQL Server Big data com o `azdata login` comando. Especifique o endereço IP externo do `controller-svc-external` serviço (por exemplo: `https://ip-address:30080`) junto com o nome de usuário e a senha para o cluster.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Se você estiver usando o AKs, precisará executar o comando a seguir para obter o endereço IP do `mgmtproxy-svc-external` serviço executando esse comando em uma janela bash ou cmd:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm ou Minikube

Se você estiver usando Kubeadm ou Minikube, execute o seguinte comando para obter o endereço IP para fazer logon no cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Criar um aplicativo

Para criar um aplicativo, use `azdata` com o `app create` comando. Esses arquivos residem localmente no computador do qual você está criando o aplicativo.

Use a sintaxe a seguir para criar um novo aplicativo no cluster Big Data:

```bash
azdata app create --spec <directory containing spec file>
```

O comando a seguir mostra um exemplo de como esse comando pode ser:

```bash
azdata app create --spec ./addpy
```

Isso pressupõe que você tenha seu aplicativo armazenado na `addpy` pasta. Essa pasta também deve conter um arquivo de especificação para o aplicativo, `spec.yaml`chamado. Consulte [a página de implantação do aplicativo](concept-application-deployment.md) para obter mais informações `spec.yaml` sobre o arquivo.

Para implantar este aplicativo de exemplo de aplicativo, crie os seguintes arquivos em um `addpy`diretório chamado:

- `add.py`. Copie o seguinte código Python para este arquivo:
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml`. Copie o seguinte código para este arquivo:
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

Em seguida, execute o comando a seguir:

```bash
azdata app create --spec ./addpy
```

Você pode verificar se o aplicativo é implantado usando o comando de lista:

```bash
azdata app list
```

Se a implantação não for concluída, você verá a `state` exibição `WaitingforCreate` como o exemplo a seguir:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Depois que a implantação for bem-sucedida, você deverá ver `state` a alteração `Ready` para o status:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Listar um aplicativo

Você pode listar todos os aplicativos que foram criados com êxito `app list` com o comando.

O comando a seguir lista todos os aplicativos disponíveis no cluster Big Data:

```bash
azdata app list
```

Se você especificar um nome e uma versão, ele listará esse aplicativo específico e seu estado (criando ou pronto):

```bash
azdata app list --name <app_name> --version <app_version>
```

O exemplo a seguir demonstra esse comando:

```bash
azdata app list --name add-app --version v1
```

Você deverá ver uma saída semelhante ao exemplo a seguir:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Executar um aplicativo

Se o aplicativo estiver em um `Ready` estado, você poderá usá-lo executando-o com os parâmetros de entrada especificados. Use a sintaxe a seguir para executar um aplicativo:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

O comando de exemplo a seguir demonstra o comando executar:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Se a execução tiver sido bem-sucedida, você deverá ver a saída conforme especificado quando criou o aplicativo. Confira o exemplo abaixo.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>Criar um esqueleto de aplicativo

O comando init fornece um Scaffold com os artefatos relevantes que são necessários para implantar um aplicativo. O exemplo a seguir cria Olá, você pode fazer isso executando o comando a seguir.

```bash
azdata app init --name hello --version v1 --template python
```

Isso criará uma pasta chamada Hello.  Você pode `cd` no diretório e inspecionar os arquivos gerados na pasta. spec. YAML define o aplicativo, como nome, versão e código-fonte. Você pode editar a especificação para alterar nome, versão, entrada e saídas.

Aqui está um exemplo de saída do comando init que você verá na pasta

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Descrever um aplicativo

O comando de descrição fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade no cluster. Normalmente, isso é usado por um desenvolvedor de aplicativo para criar um aplicativo usando o cliente do Swagger e usando o WebService para interagir com o aplicativo de maneira RESTful. Consulte [consumir aplicativos em clusters Big data](big-data-cluster-consume-apps.md) para obter mais informações.

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>Excluir um aplicativo

Para excluir um aplicativo do cluster Big Data, use a seguinte sintaxe:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Próximas etapas

Explore como integrar aplicativos implantados em clusters SQL Server Big Data em seus próprios aplicativos em [aplicativos de consumo em Big data clusters](big-data-cluster-consume-apps.md) para obter mais informações. Você também pode conferir exemplos adicionais em [exemplos de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre clusters de Big Data SQL Server, consulte [o que são SQL Server 2019 Big data clusters?](big-data-cluster-overview.md).
