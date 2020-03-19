---
title: Instalação no Docker
titleSuffix: SQL Server Machine Learning Services
description: Saiba como instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 02/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 767df0ec19f0749eab78a757db5bc92eb66cab49
ms.sourcegitcommit: 39d8d2d504d0ab70bac5ae3e981657e15dfb7bee
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2020
ms.locfileid: "78964514"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker

Este artigo explica como instalar os Serviços de Machine Learning do SQL Server no Docker. Você pode usar Serviços do Machine Learning (no banco de dados) para executar scripts de Python e R no banco de dados. Não fornecemos contêineres pré-criados com os Serviços de Machine Learning. Crie um com base nos contêineres do SQL Server usando [um modelo de exemplo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Pré-requisitos

- Interface de linha de comando Git.
- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/install/) (Instalar o Docker).
- [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonar o repositório mssql-docker

1. Abra um terminal Bash no Linux ou no Mac ou abra um terminal do Subsistema do Windows para Linux no Windows.

2. Crie um diretório local para conter uma cópia local do repositório mssql-docker.

3. Execute o comando git clone para clonar o repositório mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Criar uma imagem de contêiner do SQL Server Linux

1. Altere o diretório para mssql-mlservices:

2. No mesmo diretório, execute o seguinte comando:

    ```bash
       docker builds -t mssql-server-mlservices
    ```

3. Execute o comando:

    ```bash
       docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=  -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    Modifique-o para adicionar SA_PASSWORD e o caminho -v. 

4. Confirme-o executando o seguinte comando:

    ```bash
       docker ps -a
    ```

   > [!NOTE]
   > Para compilar a imagem do Docker, você deve instalar pacotes com vários GBs de tamanho. O script pode levar até 20 minutos para ser terminar a execução dependendo da largura de banda da rede.

## <a name="run-the-sql-server-linux-container-image"></a>Executar a imagem de contêiner do SQL Server Linux

1. Defina suas variáveis de ambiente antes de executar o contêiner. Defina a variável de ambiente PATH_TO_MSSQL como um diretório de host:

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

2. Execute o script run.sh:

   ```bash
   ./run.sh
   ```

   Este comando cria um contêiner do SQL Server com Serviços de Machine Learning usando a edição de Desenvolvedor (padrão). A porta do SQL Server **1433** é exposta no host como a porta **1401**.

   > [!NOTE]
   > O processo para executar edições de produção do SQL Server em contêineres é um pouco diferente. Para obter mais informações, confira [Configurar imagens de contêiner do SQL Server no Docker](sql-server-linux-configure-docker.md). Se você usar os mesmo nomes e portas de contêiner, o restante deste tutorial ainda funcionará com contêineres de produção.

3. Para exibir seus contêineres do Docker, execute o comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

4. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```
    Saída:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="run-in-a-container"></a>Executar em um contêiner

[Executar imagens de contêiner do SQL Server com o Docker](quickstart-install-connect-docker.md).

## <a name="connect-to-linux-sql-server-in-the-container"></a>Conectar-se ao Linux SQL Server no contêiner

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)
