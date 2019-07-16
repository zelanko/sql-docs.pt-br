---
title: Implantar aplicativos usando mssqlctl
titleSuffix: SQL Server big data clusters
description: Implante um script Python ou R como um aplicativo no cluster de big data do SQL Server 2019 (visualização).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e3768ff5bfc01f2068b10ebd8afc18d12fa808c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958860"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Como implantar um aplicativo no cluster de big data do SQL Server (versão prévia)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar e gerenciar o script de R e Python como um aplicativo dentro de um cluster de big data do SQL Server 2019 (visualização).

## <a name="whats-new-and-improved"></a>O que é novo e aprimorado

- Um único utilitário de linha de comando para gerenciar o cluster e aplicativo.
- Simplifica a implantação de aplicativo, fornecendo um controle granular por meio de arquivos de especificações.
- Suporte à hospedagem de tipos de aplicativos adicionais - SSIS e MLeap (novo no CTP 2.3)
- [Extensão do VS Code](app-deployment-extension.md) para gerenciar a implantação de aplicativo

Aplicativos são implantados e gerenciados usando `mssqlctl` utilitário de linha de comando. Este artigo fornece exemplos de como implantar aplicativos da linha de comando. Para saber como usar isso no Visual Studio Code, confira [extensão do VS Code](app-deployment-extension.md).

Há suporte para os seguintes tipos de aplicativos:
- Aplicativos de R e Python (funções, modelos e aplicativos)
- Fornecimento de MLeap
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de big data do SQL Server de 2019](deployment-guidance.md)
- [Utilitário de linha de comando mssqlctl](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Capacidades

No SQL Server de 2019 (visualização) você pode criar, excluir, descrevem, inicializar, lista executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **mssqlctl**.

|Comando |Descrição |
|:---|:---|
|`mssqlctl login` | Entrar em um cluster de big data do SQL Server |
|`mssqlctl app create` | Crie aplicativo. |
|`mssqlctl app delete` | Exclua o aplicativo. |
|`mssqlctl app describe` | Descreva o aplicativo. |
|`mssqlctl app init` | Início rápido novo esqueleto do aplicativo. |
|`mssqlctl app list` | Lista de aplicativos. |
|`mssqlctl app run` | Execute o aplicativo. |
|`mssqlctl app update`| Atualize o aplicativo. |

Você pode obter ajuda com o `--help` parâmetro como no exemplo a seguir:

```bash
mssqlctl app create --help
```

As seções a seguir descrevem esses comandos em mais detalhes.

## <a name="sign-in"></a>Entrar

Antes de implantar ou interagir com aplicativos, primeiro entre no seu SQL Server cluster de big data com o `mssqlctl login` comando. Especifique o endereço IP externo do `controller-svc-external` serviço (por exemplo: `https://ip-address:30080`) junto com o nome de usuário e senha para o cluster.

```bash
mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Se você estiver usando o AKS, você precisará executar o comando a seguir para obter o endereço IP do `mgmtproxy-svc-external` serviço executando este comando em uma janela de bash ou cmd:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm ou Minikube

Se você estiver usando Kubeadm ou Minikube para executar o comando a seguir para obter o endereço IP para fazer logon no cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Criar um aplicativo

Para criar um aplicativo, use `mssqlctl` com o `app create` comando. Esses arquivos residem localmente na máquina que você está criando o aplicativo.

Use a sintaxe a seguir para criar um novo aplicativo no cluster de big data:

```bash
mssqlctl app create --spec <directory containing spec file>
```

O comando a seguir mostra um exemplo de como pode ser este comando:

```bash
mssqlctl app create --spec ./addpy
```

Isso pressupõe que você tenha seu aplicativo armazenado em do `addpy` pasta. Essa pasta também deve conter um arquivo de especificação para o aplicativo, chamado `spec.yaml`. Consulte [a página de implantação do aplicativo](concept-application-deployment.md) para obter mais informações sobre o `spec.yaml` arquivo.

Para implantar esse aplicativo de exemplo de aplicativo, crie os seguintes arquivos em um diretório chamado `addpy`:

- `add.py`. Copie o seguinte código Python para esse arquivo:
   ```py
   #add.py
   def add(x,y):
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

Em seguida, execute o comando a seguir:

```bash
mssqlctl app create --spec ./addpy
```

Você pode verificar se o aplicativo é implantado usando o comando lista:

```bash
mssqlctl app list
```

Se a implantação não está completa você deve ver a `state` Mostrar `WaitingforCreate` como o exemplo a seguir:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Após a implantação for bem-sucedida, você deverá ver a `state` alterar para `Ready` status:

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

Você pode listar todos os aplicativos que foram criados com êxito com o `app list` comando.

O comando a seguir lista todos os aplicativos disponíveis no seu cluster de big data:

```bash
mssqlctl app list
```

Se você especificar um nome e versão, ele lista esse aplicativo específico e seu estado (Criando ou pronta):

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

O exemplo a seguir demonstra esse comando:

```bash
mssqlctl app list --name add-app --version v1
```

Você deve ver saídas semelhantes ao exemplo a seguir:

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

Se o aplicativo está em um `Ready` de estado, você pode usá-lo ao executá-lo com seus parâmetros de entrada especificados. Use a seguinte sintaxe para executar um aplicativo:

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

O comando de exemplo a seguir demonstra o comando run:

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

Se a execução foi bem-sucedida, você deverá ver sua saída como especificou quando criou o aplicativo. Confira o exemplo abaixo.

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

## <a name="create-an-app-skeleton"></a>Criar um esqueleto do aplicativo

O comando init fornece um andaime com os artefatos relevantes que é necessário para implantar um aplicativo. O exemplo a seguir cria hello, você pode fazer isso executando o comando a seguir.

```bash
mssqlctl app init --name hello --version v1 --template python
```

Isso criará uma pasta chamada hello.  Você pode `cd` no diretório e inspecione os arquivos gerados na pasta. Spec.YAML define o aplicativo, como nome, versão e código-fonte. Você pode editar a especificação para alterar o nome, versão, entrada e saídas.

Aqui está um exemplo de saída do comando de inicialização que você verá na pasta

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Descrever um aplicativo

O comando descrição fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade em seu cluster. Isso normalmente é usado por um desenvolvedor de aplicativo para compilar um aplicativo usando o cliente do swagger e usando o serviço Web para interagir com o aplicativo de maneira RESTful. Ver [consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md) para obter mais informações.

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

Para excluir um aplicativo do seu cluster de big data, use a seguinte sintaxe:

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>Próximas etapas

Explore como integrar aplicativos implantados no SQL Server em seus próprios aplicativos em clusters do big data [consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md) para obter mais informações. Você também pode conferir exemplos adicionais no [exemplos de implantar o aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
