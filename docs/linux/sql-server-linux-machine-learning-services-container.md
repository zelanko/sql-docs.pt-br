---
title: Executar SQL Server Serviços de Machine Learning em um contêiner | Microsoft Docs
description: Este tutorial mostra como usar SQL Server Serviços de Machine Learning em um contêiner do Linux em execução no Docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f3d3774adf4bee07269b25c3359b031ca24eb99e
ms.sourcegitcommit: ef7834ed0f38c1712f45737018a0bfe892e894ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300421"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Executar SQL Server Serviços de Machine Learning em um contêiner

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial demonstra como criar um contêiner do Docker com SQL Server Serviços de Machine Learning e executar Machine Learning scripts do Transact-SQL.

> [!div class="checklist"]
> * Clone o repositório MSSQL-Docker.
> * Crie SQL Server imagem de contêiner do Linux com Serviços de Machine Learning.
> * Execute SQL Server imagem de contêiner do Linux com Serviços de Machine Learning.
> * Execute scripts R ou Python usando instruções Transact-SQL.
> * Pare e remova o SQL Server contêiner do Linux. 

## <a name="prerequisites"></a>Pré-requisitos

* Interface de linha de comando git.
* O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
* Mínimo de 2 GB de espaço em disco.
* Mínimo de 2 GB de RAM.
* [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonar o repositório MSSQL-Docker

1. Abra um terminal Bash no terminal Linux/Mac ou WSL no Windows.

1. Crie um diretório local para manter uma cópia do repositório MSSQL-Docker localmente.
1. Execute o comando git clone para clonar o repositório MSSQL-Docker.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Criar SQL Server imagem de contêiner do Linux com Serviços de Machine Learning

1. Altere o diretório para o diretório MSSQL-mlservices.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Execute o script build.sh.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > A criação da imagem do Docker requer a instalação de pacotes com vários GBs de tamanho. O script pode levar até 20 minutos para ser concluído, dependendo da largura de banda da rede.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Executar SQL Server imagem de contêiner do Linux com Serviços de Machine Learning

1. Defina variáveis de ambiente antes de executar o contêiner. Defina a variável de ambiente PATH_TO_MSSQL para um diretório de host.

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Execute o script run.sh.

   ```bash
   ./run.sh
   ```

   Este comando cria um contêiner SQL Server com Serviços de Machine Learning com a Developer Edition (padrão). SQL Server porta **1433** é exposta no host como a porta **1401**.

   > [!NOTE]
   > O processo para executar as edições de SQL Server de produção em contêineres é um pouco diferente. Para obter mais informações, consulte [Configure SQL Server contêiner images on Docker](sql-server-linux-configure-docker.md). Se você usar os mesmos nomes de contêiner e portas, o restante deste passo a passo ainda funciona com contêineres de produção.

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>Executar scripts de R/Python do Transact-SQL

1. Conecte-se a SQL Server no contêiner e habilite a opção de configuração de script externo executando a seguinte instrução T-SQL.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Verifique se Serviços de Machine Learning está funcionando executando o seguinte sp_execute_external_script R/Python simples.

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
> * Clone o repositório MSSQL-Docker.
> * Crie SQL Server imagem de contêiner do Linux com Serviços de Machine Learning.
> * Execute SQL Server imagem de contêiner do Linux com Serviços de Machine Learning.
> * Execute scripts R ou Python usando instruções Transact-SQL.
> * Pare e remova o SQL Server contêiner do Linux.

Em seguida, examine outros cenários de configuração e solução de problemas do Docker:

> [!div class="nextstepaction"]
>[Guia de configuração para SQL Server no Docker](sql-server-linux-configure-docker.md)
