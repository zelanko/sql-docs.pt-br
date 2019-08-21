---
title: Implantar aplicativos usando o azdata
titleSuffix: SQL Server big data clusters
description: Implante um script Python ou R como um aplicativo no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 18e97a3567b50982bd2be11dcc3493951dfe8fa9
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653153"
---
# <a name="how-to-deploy-an-app-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Como implantar um aplicativo em[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar e gerenciar o script R e Python como um aplicativo dentro de um cluster SQL Server 2019 Big Data.

## <a name="whats-new-and-improved"></a>Novidades e melhorias

- Um único utilitário de linha de comando para gerenciar o cluster e o aplicativo.
- Implantação de aplicativos simplificada, fornecendo controle granular por meio de arquivos de especificação.
- Suporte à Hospedagem de tipos de aplicativos adicionais-SSIS e MLeap (novidade no CTP 2,3).
- [Visual Studio Code extensão](app-deployment-extension.md) para gerenciar a implantação de aplicativos.

Os aplicativos são implantados e gerenciados por meio do utilitário de linha de comando `azdata`. Este artigo fornece exemplos de como implantar aplicativos por meio da linha de comando. Para saber como usá-lo em Visual Studio Code consulte [Visual Studio Code extensão](app-deployment-extension.md).

Há suporte para os seguintes tipos de aplicativos:
- Aplicativos R e Python (funções, modelos e aplicativos)
- MLeap Serving
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019 (versão prévia), você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata login` | Entrar em um cluster de Big Data do SQL Server |
|`azdata app create` | Criar aplicativo. |
|`azdata app delete` | Excluir o aplicativo. |
|`azdata app describe` | Descrever o aplicativo. |
|`azdata app init` | Iniciar rapidamente um novo esqueleto de aplicativo. |
|`azdata app list` | Listar os aplicativos. |
|`azdata app run` | Executar o aplicativo. |
|`azdata app update`| Atualizar o aplicativo. |

Obtenha ajuda com o parâmetro `--help` como no seguinte exemplo:

```bash
azdata app create --help
```

As seções a seguir descrevem esses comandos mais detalhadamente.

## <a name="sign-in"></a>Entrar

Antes de implantar aplicativos ou interagir com eles, primeiro, entre no cluster de Big Data do SQL Server com o comando `azdata login`. Especifique o endereço IP externo do serviço `controller-svc-external` (por exemplo: `https://ip-address:30080`) junto com o nome de usuário e a senha do cluster.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Caso você esteja usando o AKS, execute o seguinte comando a seguir para obter o endereço IP do serviço `controller-svc-external` executando esse comando em uma janela de cmd ou Bash:


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm ou Minikube

Se você estiver usando Kubeadm ou Minikube, execute o seguinte comando para obter o endereço IP para entrar no cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Criar um aplicativo

Para criar um aplicativo, use `azdata` com o comando `app create`. Esses arquivos residem localmente no computador usado para criar o aplicativo.

Use a seguinte sintaxe para criar um aplicativo no cluster de Big Data:

```bash
azdata app create --spec <directory containing spec file>
```

O seguinte comando mostra um exemplo da aparência desse comando:

```bash
azdata app create --spec ./addpy
```

Isso pressupõe que o aplicativo esteja armazenado na pasta `addpy`. Essa pasta também deverá conter um arquivo de especificação para o aplicativo, chamado `spec.yaml`. Consulte [a página de implantação do aplicativo](concept-application-deployment.md) para obter mais `spec.yaml` informações sobre o arquivo.

Para implantar esse aplicativo de exemplo de aplicativo, crie os seguintes arquivos em um diretório chamado `addpy`:

- `add.py`. Copie o seguinte código Python para esse arquivo:
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml`. Copie o seguinte código para esse arquivo:
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

Em seguida, execute o seguinte comando:

```bash
azdata app create --spec ./addpy
```

Verifique se o aplicativo foi implantado usando o comando list:

```bash
azdata app list
```

Se a implantação não for concluída, você deverá ver o `state` mostrar `WaitingforCreate` como o seguinte exemplo:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Depois que a implantação for bem-sucedida, você deverá ver o `state` ser alterado para o status `Ready`:

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

Liste todos os aplicativos que foram criados com êxito com o comando `app list`.

O seguinte comando lista todos os aplicativos disponíveis no cluster de Big Data:

```bash
azdata app list
```

Se você especificar um nome e uma versão, ele listará esse aplicativo específico e o estado (Criando ou Pronto):

```bash
azdata app list --name <app_name> --version <app_version>
```

O seguinte exemplo demonstra esse comando:

```bash
azdata app list --name add-app --version v1
```

Você deverá ver uma saída semelhante ao seguinte exemplo:

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

Se o aplicativo estiver em um estado `Ready`, use-o executando-o com os parâmetros de entrada especificados. Use a seguinte sintaxe para executar um aplicativo:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

O seguinte comando de exemplo demonstra o comando de execução:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Se a execução for bem-sucedida, você deverá ver a saída especificada quando o aplicativo foi criado. Confira o exemplo abaixo.

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

O comando init fornece um scaffold com os artefatos relevantes que são necessários para implantar um aplicativo. O exemplo abaixo cria hello. Execute isso com o comando a seguir.

```bash
azdata app init --name hello --version v1 --template python
```

Isso criará uma pasta chamada hello.  Você pode executar `cd` no diretório e inspecionar os arquivos gerados na pasta. spec. YAML define o aplicativo, como nome, versão e código-fonte. Você pode editar a especificação para alterar o nome, a versão, a entrada e as saídas.

Esta é uma saída de exemplo do comando init que você verá na pasta

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Descrever um aplicativo

O comando describe fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade no cluster. Normalmente, isso é usado por um desenvolvedor de aplicativos para criar um aplicativo usando o cliente do Swagger e usando o serviço Web para interagir com o aplicativo de maneira semelhante ao RESTful. Confira [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md) para obter mais informações.

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
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
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

Para excluir um aplicativo do cluster de Big Data, use a seguinte sintaxe:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Próximas etapas

Explore como integrar aplicativos implantados [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em seus próprios aplicativos em [aplicativos de consumo em Big data clusters](big-data-cluster-consume-apps.md) para obter mais informações. Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]sobre o, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
