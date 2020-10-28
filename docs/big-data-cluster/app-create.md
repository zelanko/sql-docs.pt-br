---
title: Implantar aplicativos usando o azdata
titleSuffix: SQL Server Big Data Clusters
description: Implante um script do Python ou R como um aplicativo no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e91315b5ec79c136b4d84a7fbc36a707cc3d82f
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257296"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-clusters"></a>Como implantar um aplicativo nos Clusters de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Os aplicativos implantados nos BDC (Clusters de Big Data) do SQL Server se beneficiam de muitas vantagens, como a capacidade de computação do cluster, e acessam um grande volume de dados disponíveis no cluster. Ele aprimoram consideravelmente o desempenho, pois o aplicativo reside no mesmo cluster dos dados.

Este artigo descreve como implantar e gerenciar o script R e Python como um aplicativo em um cluster de Big Data do SQL Server.

## <a name="whats-new-and-improved"></a>Novidades e melhorias

- Um único utilitário de linha de comando para gerenciar o cluster e o aplicativo.
- Implantação de aplicativos simplificada, fornecendo controle granular por meio de arquivos de especificação.
- Suporte à hospedagem de tipos de aplicativo adicionais: SSIS (SQL Server Integration Services) e MLeap.
- [Extensão do Visual Studio Code](app-deployment-extension.md) para gerenciar a implantação de aplicativos.

Os aplicativos são implantados e gerenciados usando a [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]. Este artigo fornece exemplos de como implantar aplicativos por meio da linha de comando. Para saber como usar isso no Visual Studio Code, veja a [Extensão do Visual Studio Code](app-deployment-extension.md).

Há suporte para os seguintes tipos de aplicativos:

- **Python** : uma das linguagens de programação gerais mais populares para várias pessoas, como engenheiros de dados, cientistas de dados ou engenheiros de DevOps, dá suporte a inúmeros cenários, como estruturação de dados, automação e criação de protótipo. Até certo ponto, também é cada vez mais usado para programar aplicativos de nível empresarial trabalhando em conjunto com estruturas de desenvolvimento da Web, como o Flask e o Django, para atender a diferentes requisitos de negócios.  
- **R** : outra linguagem de programação popular para a engenharia de dados e os cientistas de dados. Comparado ao Python, o R é uma linguagem de programação com foco mais específico em computação e elementos gráficos estatísticos.  
- **SSIS (SQL Server Integration Services)** : soluções de integração de dados de alto desempenho para criação e depuração de pacotes ETL; ele usa o DTSX (formato de arquivo do pacote do Data Transformation Services), um formato de arquivo baseado em XML que armazena as instruções para o processamento da migração de dados entre bancos de dados e a integração de fontes externas.   
- **MLeap** : é um formato de serialização comum e fornece tudo o que é necessário para executar e serializar pipelines do SparkML e outros que podem ser carregados em runtime para processar tarefas de pontuação de ML quase em tempo real e próximo aos dados.  

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019, você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata** .

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

## <a name="azure-kubernetes-service-aks"></a>AKS (Serviço de Kubernetes do Azure)

Se estiver usando o AKS, execute o seguinte comando para obter o endereço IP do serviço `controller-svc-external` executando esse comando em uma janela de cmd ou Bash:


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>Clusters do Kubernetes criados com o kubeadm

Execute o comando a seguir para obter o endereço IP e entrar no cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app-skeleton"></a>Criar um esqueleto de aplicativo

O comando **azdata app init** fornece um scaffold com os artefatos relevantes que são necessários para implantar um aplicativo. O exemplo abaixo cria add-app. Execute isso com o comando a seguir.

```bash
azdata app init --name add-app --version v1 --template python
```

Isso criará uma pasta chamada hello.  Use o comando `cd` no diretório e inspecione os arquivos gerados na pasta. spec.yaml define o aplicativo, como nome, versão e código-fonte. Edite a especificação para alterar o nome, a versão, a entrada e as saídas.

Esta é uma saída de exemplo do comando init que você verá na pasta

```
add-app.py
run-spec.yaml
spec.yaml
```

## <a name="create-an-app"></a>Criar um aplicativo

Para criar um aplicativo, use [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] com o comando `app create`. Esses arquivos residem localmente no computador usado para criar o aplicativo.

Use a seguinte sintaxe para criar um aplicativo no cluster de Big Data:

```bash
azdata app create --spec <directory containing spec file>
```

O seguinte comando mostra um exemplo da aparência desse comando:

```bash
azdata app create --spec ./addpy
```

Isso pressupõe que o aplicativo esteja armazenado na pasta `addpy`. Essa pasta também deverá conter um arquivo de especificação para o aplicativo, chamado `spec.yaml`. Confira [a página Implantação de Aplicativos](concept-application-deployment.md) para obter mais informações sobre o arquivo `spec.yaml`.

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

Se a implantação não for concluída, você verá o `state` mostrar `WaitingforCreate` como o seguinte exemplo:

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

## <a name="delete-an-app"></a>Excluir um aplicativo

Para excluir um aplicativo do cluster de Big Data, use a seguinte sintaxe:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Próximas etapas

Explore como integrar os aplicativos implantados nos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em seus aplicativos em [Executar aplicativos em clusters de Big Data](app-run.md) e [Consumir aplicativos em clusters de Big Data](app-consume.md) para obter mais informações. Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).