---
title: Implantar offline
titleSuffix: SQL Server big data clusters
description: Saiba como executar uma implantação offline de um cluster SQL Server Big Data.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419371"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Executar uma implantação offline de um cluster SQL Server Big Data

Este artigo descreve como executar uma implantação offline de um cluster SQL Server 2019 Big Data (versão prévia). Os clusters de Big data devem ter acesso a um repositório do Docker do qual efetuar pull de imagens de contêiner. Uma instalação offline é aquela em que as imagens necessárias são colocadas em um repositório do Docker privado. Esse repositório privado é usado como a origem da imagem para uma nova implantação.

## <a name="prerequisites"></a>Pré-requisitos

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Carregar imagens em um repositório privado

As etapas a seguir descrevem como efetuar pull da Big Data imagens de contêiner de cluster do repositório da Microsoft e, em seguida, enviá-las por push para seu repositório privado.

> [!TIP]
> As etapas a seguir explicam o processo. No entanto, para simplificar a tarefa, você pode usar o [script automatizado](#automated) em vez de executar manualmente esses comandos.

1. Receba as imagens de contêiner de cluster Big Data repetindo o comando a seguir. Substituir `<SOURCE_IMAGE_NAME>` por cada [nome de imagem](#images). Substitua `<SOURCE_DOCKER_TAG>` pela marca da versão do cluster Big data, como **2019-CTP 3.2-Ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Faça logon no registro do Docker privado de destino.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Marque as imagens locais com o seguinte comando para cada imagem:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Envie por push as imagens locais para o repositório privado do Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>Imagens de contêiner de cluster de Big data

As seguintes Big Data imagens de contêiner de cluster são necessárias para uma instalação offline:

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
 - **MSSQL-segurança-suporte**

## <a id="automated"></a>Script automatizado

Você pode usar um script Python automatizado que extrairá automaticamente todas as imagens de contêiner necessárias e as enviará por push para um repositório privado.

> [!NOTE]
> O Python é um pré-requisito para o uso do script. Para obter mais informações sobre como instalar o Python, consulte a [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Do bash ou do PowerShell, baixe o script com ondulação:

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

1. Siga os prompts para inserir o repositório da Microsoft e suas informações de repositório privado. Após a conclusão do script, todas as imagens necessárias devem estar localizadas em seu repositório privado.

## <a name="install-tools-offline"></a>Instalar ferramentas offline

As implantações de cluster de Big data exigem várias ferramentas, incluindo **Python**, **azdata**e **kubectl**. Use as etapas a seguir para instalar essas ferramentas em um servidor offline.

### <a id="python"></a>Instalar Python offline

1. Em um computador com acesso à Internet, baixe um dos seguintes arquivos compactados que contêm Python:

   | Sistema Operacional | Download |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado no computador de destino e extraia-o para uma pasta de sua escolha.

1. Somente para Windows, execute `installLocalPythonPackages.bat` a partir dessa pasta e passe o caminho completo para a mesma pasta que um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a>Instalar o azdata offline

1. Em um computador com acesso à Internet e [Python](https://wiki.python.org/moin/BeginnersGuide/Download), execute o seguinte comando para baixar todos os pacotes **azdata** para a pasta atual.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copie os pacotes baixados e o arquivo **requirements. txt** para o computador de destino.

1. Execute o comando a seguir no computador de destino, especificando a pasta na qual você copiou os arquivos anteriores.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>Instalar o kubectl offline

Para instalar o **kubectl** em um computador offline, use as etapas a seguir.

1. Use a **rotação** para baixar o **kubectl** para uma pasta de sua escolha. Para obter mais informações, consulte [instalar o binário kubectl usando](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)a ondulação.

1. Copie a pasta para o computador de destino.

## <a name="deploy-from-private-repository"></a>Implantar do repositório privado

Para implantar do repositório privado, use as etapas descritas no [Guia de implantação](deployment-guidance.md), mas use um arquivo de configuração de implantação personalizada que especifique as informações particulares do repositório do Docker. Os comandos **azdata** a seguir demonstram como alterar as configurações do Docker em um arquivo de configuração de implantação personalizado chamado **Control. JSON**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

A implantação solicita o nome de usuário e a senha do Docker, ou você pode especificá-los nas variáveis de ambiente **DOCKER_USERNAME** e **DOCKER_PASSWORD** .

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre implantações de cluster Big Data, consulte [como implantar SQL Server Big data clusters no kubernetes](deployment-guidance.md).
