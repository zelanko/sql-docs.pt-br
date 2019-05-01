---
title: Implantar offline
titleSuffix: SQL Server big data clusters
description: Saiba como executar uma implantação offline de um cluster de big data do SQL Server.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: afd7c0e3b8fcf92721e95231175cb33d81c6775e
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759143"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Executar uma implantação offline de um cluster de big data do SQL Server

Este artigo descreve como executar uma implantação offline de um cluster de big data do SQL Server 2019 (visualização). Clusters de big data devem ter acesso a um repositório do Docker do qual a imagens de contêiner de pull. Uma instalação offline é-um em que as imagens necessárias são colocadas em um repositório privado do Docker. Esse repositório privado, em seguida, é usado como a origem da imagem para uma nova implantação.

## <a name="prerequisites"></a>Prerequisites

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Carregar imagens em um repositório privado

As etapas a seguir descrevem como efetuar pull de cluster de big data imagens de contêiner do repositório Microsoft e, em seguida, enviá-los ao seu repositório particular.

> [!TIP]
> As etapas a seguir explicam o processo. No entanto, para simplificar a tarefa, você pode usar o [script automatizado](#automated) em vez de executar manualmente esses comandos.

1. Primeiro, faça logon registro do Docker de Microsoft com o **logon do docker** comando. Use o nome de usuário e a senha que a Microsoft fornecida como parte do programa de adoção antecipada.

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > Esses comandos usam o PowerShell como um exemplo, mas você pode executá-los de cmd, bash ou qualquer shell de comando que pode executar o docker. No Linux, adicionar `sudo` para cada comando.

1. O cluster de big data de pull imagens de contêiner, repetindo o comando a seguir. Substitua `<SOURCE_IMAGE_NAME>` com cada [nome da imagem](#images). Substitua `<SOURCE_DOCKER_TAG>` com a marca para big data de cluster versão, como **ctp2.5**.  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Faça logon no destino particular do registro do Docker.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. As imagens locais com o seguinte comando para cada imagem de marca:

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Envie por push as imagens do locais para o repositório privado do Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Imagens de contêiner do cluster de big data

As seguintes imagens de contêiner de cluster de big data são necessárias para uma instalação offline:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-portal**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**

## <a id="automated"></a> Script automatizado

Você pode usar um script de python automatizados que automaticamente extrairá todas as imagens de contêiner necessárias e enviá-las em um repositório privado.

> [!NOTE]
> Python é um pré-requisito para usar o script. Para obter mais informações sobre como instalar o Python, consulte o [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. No bash ou PowerShell, baixe o script com **curl**:

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

1. Siga os prompts para inserir o repositório da Microsoft e suas informações de repositório privado. Depois que o script for concluído, todos os necessários imagens devem estar localizadas em seu repositório privado.

## <a name="install-tools-offline"></a>Instalar as ferramentas offline

Implantações de cluster de big data requerem várias ferramentas, inclusive **Python**, **mssqlctl**, e **kubectl**. Use as etapas a seguir para instalar essas ferramentas em um servidor offline.

### <a id="python"></a> Instalar o python offline

1. Em um computador com acesso à internet, baixe um dos seguintes arquivos compactados contendo o Python:

   | Sistema Operacional | Download |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado para o computador de destino e extraia-os em uma pasta de sua escolha.

1. Para Windows, execute `installLocalPythonPackages.bat` essa pasta e passe o caminho completo para a mesma pasta como um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> Instalar mssqlctl off-line

1. Em um computador com acesso à internet e [Python](https://wiki.python.org/moin/BeginnersGuide/Download), execute o seguinte comando para baixar todos os desativar o **mssqlctl** pacotes na pasta atual.

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. Baixe o **Requirements. txt** arquivo.

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. Copie os pacotes baixados e o **Requirements. txt** arquivo para o computador de destino.

1. Execute o seguinte comando no computador de destino, especificando a pasta que você copiou os arquivos anteriores.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Instalar kubectl off-line

Para instalar **kubectl** para um computador offline, use as etapas a seguir.

1. Use **curl** para baixar **kubectl** para uma pasta de sua escolha. Para obter mais informações, consulte [instalar binário kubectl usando curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copie a pasta para a máquina de destino.

## <a name="deploy-with-from-repository"></a>Implantar com do repositório

Para implantar a partir do repositório privado, use as etapas descritas na [guia de implantação](deployment-guidance.md), mas personalizar as seguintes variáveis de ambiente para corresponder ao seu repositório particular do Docker.

- **DOCKER_REGISTRY**  
- **DOCKER_REPOSITORY**
- **DOCKER_USERNAME**
- **DOCKER_PASSWORD**  
- **DOCKER_EMAIL**
- **DOCKER_IMAGE_TAG**

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre implantações de cluster de big data, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md).
