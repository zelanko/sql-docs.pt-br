---
title: Execute serviços em um contêiner de aprendizado de máquina do SQL Server | Microsoft Docs
description: Este tutorial mostra como usar os serviços do SQL Server Machine Learning em um contêiner do Linux em execução no Docker.
author: uc-msft
ms.author: umajay
manager: craigg
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 3e654e29d6c49d3bf68cdfe7c4e3b479b47a973c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67840465"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Execute serviços em um contêiner de aprendizado de máquina do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial demonstra como criar um contêiner do Docker com serviços do SQL Server Machine Learning e executar Scripts de aprendizado de máquina do Transact-SQL.

> [!div class="checklist"]
> * Clone o repositório mssql-docker.
> * Crie imagem de contêiner do Linux do SQL Server com serviços de Machine Learning.
> * Execute a imagem de contêiner do Linux do SQL Server com serviços de Machine Learning.
> * Execute scripts R ou Python usando instruções Transact-SQL.
> * Parar e remover o contêiner do Linux do SQL Server. 

## <a name="prerequisites"></a>Pré-requisitos

* Interface de linha de comando do Git.
* O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
* Mínimo de 2 GB de espaço em disco.
* Mínimo de 2 GB de RAM.
* [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clone o repositório mssql-docker

1. Abra um terminal bash no Linux/Mac ou WSL terminal no Windows.

1. Crie um diretório local para armazenar uma cópia do repositório mssql-docker localmente.
1. Execute o comando de clone de git para clonar o repositório mssql-docker.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Criar imagem de contêiner do Linux do SQL Server com serviços de Machine Learning

1. Altere o diretório para o diretório mlservices mssql.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Execute o script build.sh.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Criando a imagem do docker requer a instalação de pacotes que estão vários GBs de tamanho. O script pode levar até 20 minutos para ser concluída dependendo da largura de banda de rede.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Executar a imagem de contêiner do Linux do SQL Server com serviços de Machine Learning

1. Definir variáveis de ambiente antes de executar o contêiner. Defina a variável de ambiente PATH_TO_MSSQL para um diretório do host.

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

   Este comando cria um contêiner do SQL Server com serviços de Machine Learning com a edição de desenvolvedor (padrão). Porta do SQL Server **1433** é exposta no host de porta **1401**.

   > [!NOTE]
   > O processo para executar edições do SQL Server de produção em contêineres é ligeiramente diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production). Se você usar o mesmo nomes de contêiner e portas, o restante deste passo a passo ainda funciona com contêineres de produção.

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>Executar R / Python scripts do Transact-SQL

1. Conectar-se ao SQL Server no contêiner e habilite a opção de configuração de script externo, executando a seguinte instrução T-SQL.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Verifique se os que serviços de Machine Learning está funcionando, executando o seguinte sp_execute_external_script de R/Python simples.

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
> * Clone o repositório mssql-docker.
> * Crie imagem de contêiner do Linux do SQL Server com serviços de Machine Learning.
> * Execute a imagem de contêiner do Linux do SQL Server com serviços de Machine Learning.
> * Execute scripts R ou Python usando instruções Transact-SQL.
> * Parar e remover o contêiner do Linux do SQL Server.

Em seguida, examine outras configurações do Docker e cenários de solução de problemas:

> [!div class="nextstepaction"]
>[Guia de configuração para o SQL Server no Docker](sql-server-linux-configure-docker.md)
