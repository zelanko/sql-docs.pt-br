---
title: Implantação offline
titleSuffix: SQL Server big data clusters
description: Saiba como executar uma implantação offline de um cluster de Big Data do SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 061e3c39f3cbcfd7e15367bbe9b37f8fc0aebb31
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652363"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Executar uma implantação offline de um cluster de Big Data do SQL Server

Este artigo descreve como executar uma implantação offline de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Os clusters de Big Data precisam ter acesso a um repositório do Docker do qual será efetuado pull das imagens de contêiner. Uma instalação offline é aquela em que as imagens necessárias são colocadas em um repositório privado do Docker. Em seguida, esse repositório privado é usado como a origem da imagem para uma nova implantação.

## <a name="prerequisites"></a>Pré-requisitos

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Carregar imagens em um repositório privado

As etapas a seguir descrevem como efetuar pull das imagens de contêiner de cluster de Big Data do repositório da Microsoft e, em seguida, efetuar push delas para seu repositório privado.

> [!TIP]
> As etapas a seguir explicam o processo. No entanto, para simplificar a tarefa, você pode usar o [script automatizado](#automated) em vez de executar esses comandos manualmente.

1. Efetue pull das imagens de contêiner de cluster de Big Data repetindo o comando a seguir. Substitua `<SOURCE_IMAGE_NAME>` por cada [nome de imagem](#images). Substitua `<SOURCE_DOCKER_TAG>` pela tag da versão do cluster de Big Data, como **2019-CTP3.2-ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Faça logon no registro privado de destino do Docker.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Marque as imagens locais com o seguinte comando para cada imagem:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Envie por push as imagens locais ao repositório privado do Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Imagens de contêiner de cluster de Big Data

As seguintes imagens de contêiner de cluster de Big Data são necessárias para uma instalação offline:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
 - **mssql-security-support**

## <a id="automated"></a> Script automatizado

Use um script automatizado do Python que efetuará pull automaticamente de todas as imagens de contêiner necessárias e as enviará por push para um repositório privado.

> [!NOTE]
> O Python é um pré-requisito para o uso do script. Para obter mais informações sobre como instalar o Python, confira a [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. No Bash ou no PowerShell, baixe o script com o **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Em seguida, execute o script com um dos seguintes comandos:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Siga os prompts para inserir o repositório da Microsoft e suas informações de repositório privado. Após a conclusão do script, todas as imagens necessárias deverão estar localizadas no repositório privado.

## <a name="install-tools-offline"></a>Instalar ferramentas offline

As implantações de cluster de Big Data exigem várias ferramentas, incluindo **Python**, **azdata** e **kubectl**. Use as etapas a seguir para instalar essas ferramentas em um servidor offline.

### <a id="python"></a> Instalar o Python offline

1. Em um computador com acesso à Internet, baixe um dos seguintes arquivos compactados que contêm o Python:

   | Sistema operacional | Download |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado para o computador de destino e extraia-o em uma pasta de sua escolha.

1. Somente para o Windows, execute `installLocalPythonPackages.bat` nessa pasta e passe o caminho completo para a mesma pasta como um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a> Instalar o azdata offline

1. Em um computador com acesso à Internet e o [Python](https://wiki.python.org/moin/BeginnersGuide/Download), execute o comando a seguir para baixar todos os pacotes do **azdata** na pasta atual.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copie os pacotes baixados e o arquivo **requirements.txt** para o computador de destino.

1. Execute o comando a seguir no computador de destino, especificando a pasta na qual você copiou os arquivos anteriores.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Instalar o kubectl offline

Para instalar o **kubectl** em um computador offline, use as etapas a seguir.

1. Use o **curl** para baixar o **kubectl** em uma pasta de sua escolha. Para obter mais informações, confira [Instalar o binário do kubectl usando o curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copie a pasta para o computador de destino.

## <a name="deploy-from-private-repository"></a>Implantação por meio do repositório privado

Para executar a implantação por meio do repositório privado, use as etapas descritas no [guia de implantação](deployment-guidance.md), mas use um arquivo de configuração de implantação personalizado que especifique as informações do repositório privado do Docker. Os seguintes comandos do **azdata** demonstram como alterar as configurações do Docker em um arquivo de configuração de implantação personalizado chamado **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

A implantação solicita o nome de usuário e a senha do Docker ou você pode especificá-los nas variáveis de ambiente **DOCKER_USERNAME** e **DOCKER_PASSWORD**.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre implantações de cluster Big data, consulte [como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em kubernetes](deployment-guidance.md).
