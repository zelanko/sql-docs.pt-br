---
title: Instalação no Docker
titleSuffix: SQL Server Machine Learning Services
description: Saiba como instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 03/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53419aba5515a9a60817ec0cc2a9de5a648d2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80228337"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como instalar os Serviços de Machine Learning do SQL Server no Docker. Você pode usar Serviços do Machine Learning (no banco de dados) para executar scripts de Python e R no banco de dados. Não fornecemos contêineres pré-criados com os Serviços de Machine Learning. Crie um com base nos contêineres do SQL Server usando [um modelo de exemplo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Pré-requisitos

- Interface de linha de comando Git.

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, confira [Obter o Docker](https://docs.docker.com/get-docker/).

- Confira também os [requisitos do sistema para o SQL Server em Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonar o repositório mssql-docker

O comando a seguir clona o repositório git `mssql-docker` para um diretório local.

1. Abra um terminal Bash no Linux ou no Mac ou abra um terminal do Subsistema do Windows para Linux no Windows.

2. Crie um diretório para manter uma cópia local do repositório mssql-docker.

3. Execute o comando git clone para clonar o repositório mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Criar uma imagem de contêiner do SQL Server Linux

Conclua as seguintes etapas para criar a imagem do Docker:

1. Altere o diretório para mssql-mlservices:

2. No mesmo diretório, execute o seguinte comando:

    ```bash
    docker builds -t mssql-server-mlservices
    ```

3. Execute o comando:

    ```bash
    docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=<your_sa_password> -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    Altere `<your_sa_password>` em `SA_PASSWORD=<your_sa_password>` e altere o caminho de `-v`. 

4. Confirme-o executando o seguinte comando:

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > Para compilar a imagem do Docker, você deve instalar pacotes com vários GBs de tamanho. A execução do script pode levar algum tempo para ser concluída dependendo da largura de banda da rede.

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

4. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e estará escutando na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Saída:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>Habilitar Serviços de Machine Learning

Para habilitar os Serviços de Machine Learning, conecte-se à sua instância do SQL Server e execute a seguinte instrução T-SQL:

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/python-ski-rental-linear-regression.md)
+ [Tutorial: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/python-clustering-model.md)

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)
