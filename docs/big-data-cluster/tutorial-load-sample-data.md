---
title: Carregar dados de exemplo
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como carregar dados de exemplo em um cluster SQL Server Big Data. Os dados de exemplo incluem dados relacionais na instância mestra de SQL Server. Ele também inclui dados do HDFS no pool de armazenamento. Esses dados dão suporte a outros tutoriais nesta seção.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419279"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Tutorial: Carregar dados de exemplo em um cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial explica como usar um script para carregar dados de exemplo em um cluster SQL Server Big Data 2019 (versão prévia). Muitos dos outros tutoriais da documentação usam esses dados de exemplo.

> [!TIP]
> Você pode encontrar exemplos adicionais para SQL Server Cluster de Big Data 2019 (versão prévia) no repositório GitHub [SQL-Server-Samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) . Eles estão localizados no **SQL-Server-Samples/Samples/Features/SQL-Big-data-cluster/** Path.

## <a name="prerequisites"></a>Pré-requisitos

- [Um cluster Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big data](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>Carregar dados de exemplo

As etapas a seguir usam um script de inicialização para baixar um SQL Server backup de banco de dados e carregar os mesmos em seu cluster Big Data. Para facilitar o uso, essas etapas foram divididas em seções do [Windows](#windows) e do [Linux](#linux) .

## <a id="windows"></a> Windows

As etapas a seguir descrevem como usar um cliente Windows para carregar os dados de exemplo em seu cluster Big Data.

1. Abra um novo prompt de comando do Windows.

   > [!IMPORTANT]
   > Não use o Windows PowerShell para essas etapas. No PowerShell, o script falhará, pois usará a versão do PowerShell da ondulação.

1. Use a **rotação** para baixar o script de Bootstrap para os dados de exemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Baixe o script Transact-SQL **Bootstrap-Sample-DB. SQL** . Esse script é chamado pelo script de inicialização.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para o cluster Big Data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome que você atribuiu ao cluster Big Data. |
   | <SQL_MASTER_IP> | O endereço IP da instância mestra. |
   | <SQL_MASTER_SA_PASSWORD> | A senha SA para a instância mestra. |
   | <KNOX_IP> | O endereço IP do gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | A senha para o gateway HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP para a instância mestra do SQL Server e o Knox. Execute `kubectl get svc -n <your-big-data-cluster-name>` e examine os endereços IP externos para a instância mestra (**Master-svc-external**) e Knox (**Gateway-svc-external**). O nome padrão de um cluster é **MSSQL-cluster**.

1. Execute o script de inicialização.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

As etapas a seguir descrevem como usar um cliente Linux para carregar os dados de exemplo em seu cluster Big Data.

1. Baixe o script de inicialização e atribua permissões de executável a ele.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Baixe o script Transact-SQL **Bootstrap-Sample-DB. SQL** . Esse script é chamado pelo script de inicialização.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para o cluster Big Data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome que você atribuiu ao cluster Big Data. |
   | <SQL_MASTER_IP> | O endereço IP da instância mestra. |
   | <SQL_MASTER_SA_PASSWORD> | A senha SA para a instância mestra. |
   | <KNOX_IP> | O endereço IP do gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | A senha para o gateway HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP para a instância mestra do SQL Server e o Knox. Execute `kubectl get svc -n <your-big-data-cluster-name>` e examine os endereços IP externos para a instância mestra (**Master-svc-external**) e Knox (**Gateway-svc-external**). O nome padrão de um cluster é **MSSQL-cluster**.

1. Execute o script de inicialização.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Próximas etapas

Depois que o script de inicialização é executado, seu cluster de Big Data tem os bancos de dados de exemplo e de HDFS. Os tutoriais a seguir usam os dados de exemplo para demonstrar Big Data recursos de cluster:

Virtualização de dados:

- [Tutorial: Consultar HDFS em um cluster SQL Server Big Data](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Consultar o Oracle em um cluster SQL Server Big Data](tutorial-query-oracle.md)

Ingestão de dados:

- [Tutorial: Ingerir dados em um pool de dados de SQL Server com o Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Ingerir dados em um pool de dados de SQL Server com trabalhos do Spark](tutorial-data-pool-ingest-spark.md)

Notebooks

- [Tutorial: Executar um bloco de anotações de exemplo em um cluster SQL Server Big Data 2019](tutorial-notebook-spark.md)