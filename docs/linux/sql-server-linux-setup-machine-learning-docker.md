---
title: Instalação no Docker
titleSuffix: SQL Server Machine Learning Services
description: Saiba como instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 05/11/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c07c92b65fe8ebed54ac75f3b9180bbd39534109
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882512"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Instalar os Serviços de Machine Learning do SQL Server (Python e R) no Docker

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo explica como instalar os Serviços de Machine Learning do SQL Server no Docker. Você pode usar Serviços do Machine Learning (no banco de dados) para executar scripts de Python e R no banco de dados. Não fornecemos contêineres pré-criados com os Serviços de Machine Learning. Crie um com base nos contêineres do SQL Server usando [um modelo de exemplo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Pré-requisitos

- Interface de linha de comando Git.

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, confira [Obter o Docker](https://docs.docker.com/get-docker/).

- Confira também os [requisitos do sistema para o SQL Server em Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonar o repositório mssql-docker

O comando a seguir clona o repositório git `mssql-docker` para um diretório local.

1. Abra um terminal de Bash no Linux ou Mac.

2. Crie um diretório para manter uma cópia local do repositório mssql-docker.

3. Execute o comando git clone para clonar o repositório mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Criar uma imagem de contêiner do SQL Server Linux

Conclua as seguintes etapas para criar a imagem do Docker:

1. Altere o diretório para mssql-mlservices:
    
    ```bash
    /mssql-docker/linux/preview/examples/mssql-mlservices
    ```

2. No mesmo diretório, execute o seguinte comando:

    ```bash
    docker build -t mssql-server-mlservices .
    ```

3. Execute o comando:

    ```bash
    docker run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=<password> -v <directory on the host OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```
  
    > [!NOTE]
    > Qualquer um dos seguintes valores podem ser usados para MSSQL_PID: Developer (gratuito), Express (gratuito), Enteprise (pago), Standard (pago). Se você estiver usando uma edição paga, verifique se comprou uma licença. Substitua (senha) pela sua senha real. A montagem de volume usando -v é opcional. Substitua (diretório no sistema operacional do host) por um diretório real no qual você deseja montar os dados do banco de dados e os arquivos de log.
    

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
  
   > [!NOTE]
   > O processo para executar edições de produção do SQL Server em contêineres é um pouco diferente. Para obter mais informações, confira [Configurar imagens de contêiner do SQL Server no Docker](sql-server-linux-configure-docker.md). Se você usar os mesmo nomes e portas de contêiner, o restante deste tutorial ainda funcionará com contêineres de produção.

2. Para exibir seus contêineres do Docker, execute o comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

3. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e estará escutando na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

 
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

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial do Python: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../machine-learning/tutorials/python-clustering-model.md)

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../machine-learning/tutorials/sqldev-in-database-r-for-sql-developers.md)
