---
title: Como implantar um aplicativo no cluster de big data do SQL Server | Microsoft Docs
description: Implante um script Python ou R como um aplicativo no cluster de big data do SQL Server 2019 (visualização).
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 11/07/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: dd24b4379f50a5b974e7a0a90412d1e13bf6db22
ms.sourcegitcommit: 87fec38a515a7c524b7c99f99bc6f4d338e09846
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51272554"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>Como implantar um aplicativo no cluster de big data do SQL Server 2019 (visualização)

Este artigo descreve como implantar e gerenciar o script de R e Python como um aplicativo dentro de um cluster de big data do SQL Server 2019 (visualização).

R e Python de aplicativos são implantados e gerenciados com o **mssqlctl-pre** utilitário de linha de comando que está incluído no CTP 2.1. Este artigo fornece exemplos de como implantar esses scripts de R e Python como aplicativos da linha de comando.

## <a name="prerequisites"></a>Prerequisites

Você deve ter um cluster de big data de 2019 do SQL Server configurado. Para obter mais informações, consulte [como implantar o SQL Server, o cluster de big data no Kubernetes](deployment-guidance.md). 

## <a name="installation"></a>Instalação

O **mssqlctl-pre** utilitário de linha de comando é fornecido para visualizar o recurso de implantação de aplicativo do Python e R. Use o seguinte comando para instalar o utilitário:

```cmd
pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.1 mssqlctlpre
```

## <a name="capabilities"></a>Recursos

No CTP 2.1, que você pode criar, excluir, listar e executar um aplicativo de R ou Python. A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **mssqlctl-pre**.

| Comando | Description |
|---|---|
| `mssqlctl-pre login` | Faça logon em um cluster de big data do SQL Server |
| `mssqlctl-pre app create` | Criar um aplicativo |
| `mssqlctl-pre app list` | Lista de aplicativos implantados |
| `mssqlctl-pre app delete` | Excluir um aplicativo |
| `mssqlctl-pre app run` | Lista de aplicativos em execução |

Você pode obter ajuda com o `--help` parâmetro como no exemplo a seguir:

```bash
mssqlctl-pre app create --help
```

As seções a seguir descrevem esses comandos em mais detalhes.

## <a name="log-in"></a>Iniciar sessão

Antes de configurar aplicativos R e Python, primeiro faça logon em seu SQL Server cluster de big data com o `mssqlctl-pre login` comando. Especifique o endereço IP (externo) da `service-proxy-lb` (por exemplo: `https://ip-address:30777`) junto com o nome de usuário e senha para o cluster.

Você pode obter o endereço IP do serviço do serviço de proxy de lb executando este comando em uma janela de bash ou cmd:
```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb> -u <user-name> -p <password>
```

## <a name="create-an-app"></a>Criar um aplicativo

Para criar um aplicativo, você passa os arquivos de código Python ou R para **mssqlctl-pre** com o `app create` comando. Esses arquivos residem localmente na máquina que você está criando o aplicativo.

Use a sintaxe a seguir para criar um novo aplicativo no seu cluster de big data:

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

O comando a seguir mostra um exemplo de como pode ser este comando:

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
Para testar isso, salvar as linhas acima de código ao seu diretório local como `add.py` e execute o comando a seguir

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

Você pode verificar se o aplicativo é implantado usando o comando lista:

```bash
mssqlctl-pre app list
```

Se a implantação não for concluída você deverá ver o "estado" Mostrar "Criando": 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

Depois que a implantação for bem-sucedida, você deverá ver o "estado" alterado para "Pronto" status:

```
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
mssqlctl-pre app list
```

Se você especificar um nome e versão, ele listará esse aplicativo específico e seu estado (Criando ou pronta):

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

O exemplo a seguir demonstra esse comando:

```bash
mssqlctl-pre app list --name add-app --version v1
```

Você deve ver saídas semelhantes ao exemplo a seguir:

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Executar um aplicativo

Se o aplicativo estiver em um estado "Pronto", você pode usá-lo ao executá-lo com seus parâmetros de entrada especificados. Use a seguinte sintaxe para executar um aplicativo:

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

O comando de exemplo a seguir demonstra o comando run:

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
```

Se a execução foi bem-sucedida, você deverá ver sua saída como especificou quando criou o aplicativo. A seguir, é mostrado um exemplo.

```
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

## <a name="delete-an-app"></a>Excluir um aplicativo

Para excluir um aplicativo do seu cluster de big data, use a seguinte sintaxe:

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>Próximas etapas

Você também pode conferir exemplos adicionais no [ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster). 

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
