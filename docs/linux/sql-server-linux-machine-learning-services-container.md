---
title: Executar os Serviços de Machine Learning do SQL Server em um contêiner | Microsoft Docs
description: Este tutorial como usar os Serviços de Machine Learning do SQL Server em um contêiner Linux em execução no Docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 28bdf20b51769e15a887b4f9ec227f7aaf6afc95
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923819"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Executar os Serviços de Machine Learning do SQL Server em um contêiner

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial demonstra como criar um contêiner do Docker usando os Serviços de Machine Learning do SQL Server e como executar scripts de Machine Learning usando Transact-SQL. A cobertura inclui as seguintes tarefas:

> [!div class="checklist"]
> * Clonar o repositório mssql-docker.
> * Criar uma imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning.
> * Executar a imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning.
> * Executar scripts de R ou Python usando instruções Transact-SQL.
> * Interromper e remover o contêiner Linux do SQL Server.

## <a name="prerequisites"></a>Prerequisites

* Interface de linha de comando Git.
* O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
* Mínimo de 2 gigabytes (GB) de espaço em disco.
* Mínimo de 2 GB de RAM.
* [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonar o repositório mssql-docker

1. Abra um terminal Bash no Linux ou Mac ou abra um terminal WSL no Windows.

1. Crie um diretório local para conter uma cópia local do repositório mssql-docker.
1. Execute o comando git clone para clonar o repositório mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>Criar uma imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning

1. Altere o diretório para mssql-mlservices:

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Execute o script build.sh:

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Para compilar a imagem do Docker, você deve instalar pacotes com vários GBs de tamanho. O script pode levar até 20 minutos para ser terminar a execução dependendo da largura de banda da rede.

## <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>Executar a imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning

1. Defina suas variáveis de ambiente antes de executar o contêiner. Defina a variável de ambiente PATH_TO_MSSQL como um diretório de host:

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Execute o script run.sh:

   ```bash
   ./run.sh
   ```

   Este comando cria um contêiner do SQL Server com Serviços de Machine Learning usando a edição de Desenvolvedor (padrão). A porta do SQL Server **1433** é exposta no host como a porta **1401**.

   > [!NOTE]
   > O processo para executar edições de produção do SQL Server em contêineres é um pouco diferente. Para obter mais informações, confira [Configurar imagens de contêiner do SQL Server no Docker](sql-server-linux-configure-docker.md). Se você usar os mesmo nomes e portas de contêiner, o restante deste tutorial ainda funcionará com contêineres de produção.

1. Para exibir seus contêineres do Docker, execute o comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Saída: 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>Alterar a senha SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>Executar scripts de R / Python de Transact-SQL

1. Conecte-se ao SQL Server no contêiner e habilite a opção de configuração de script externo executando a seguinte instrução T-SQL:

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Verifique se os Serviços de Machine Learning estão funcionando seguindo o script simples de R/Python sp_execute_external_script:

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a fazer o seguinte:

> [!div class="checklist"]
> * Clonar o repositório mssql-docker
> * Criar a imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning
> * Executar a imagem de contêiner Linux do SQL Server com os Serviços de Machine Learning
> * Executar scripts de R ou Python usando instruções Transact-SQL
> * Interromper e remover o contêiner Linux do SQL Server

A seguir, examine outros cenários de configuração e solução de problemas do Docker:

> [!div class="nextstepaction"]
>[Guia de configuração do SQL Server no Docker](sql-server-linux-configure-docker.md)
