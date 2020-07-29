---
title: Carregar dados de exemplo
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como carregar dados de exemplo em um cluster de Big Data do SQL Server. Os dados de exemplo incluem dados relacionais na instância mestre do SQL Server. Eles também incluem dados do HDFS no pool de armazenamento. Esses dados dão suporte a outros tutoriais nesta seção.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8a4412c5b32b42074d760acbc162d5df56e0976f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772860"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Tutorial: Carregar dados de exemplo em um cluster de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este tutorial explica como usar um script para carregar dados de exemplo em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Muitos dos outros tutoriais da documentação usam esses dados de exemplo.

> [!TIP]
> É possível encontrar exemplos adicionais para o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] no repositório do GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster). Eles ficam localizados no caminho **sql-server-samples/samples/features/sql-big-data-cluster/** .

## <a name="prerequisites"></a>Pré-requisitos

- [Um cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a name="load-sample-data"></a><a id="sampledata"></a> Carregar dados de exemplo

As etapas a seguir usam um script de inicialização para baixar um backup de um banco de dados do SQL Server e carregar os dados em seu cluster de Big Data. Para facilitar o uso, essas etapas foram divididas em seções referentes ao [Windows](#windows) e ao [Linux](#linux). Se você quiser usar o nome de usuário/senha básico como mecanismo de autenticação, defina as variáveis de ambiente AZDATA_USERNAME e AZDATA_PASSWORD antes de executar o script. Caso contrário, o script usará a autenticação integrada para se conectar à instância mestra do SQL Server e ao gateway do Knox. Além disso, o nome DNS deve ser especificado para os pontos de extremidade a fim de usar a autenticação integrada.

## <a name="windows"></a><a id="windows"></a> Windows

As etapas a seguir descrevem como usar um cliente do Windows para carregar os dados de exemplo em seu cluster de Big Data.

1. Abra um novo prompt de comando do Windows.

   > [!IMPORTANT]
   > Não use o Windows PowerShell para essas etapas. No PowerShell, o script falhará pois usará a versão do PowerShell para **curl**.

1. Use **curl** para baixar o script de inicialização para os dados de exemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Baixe o script Transact-SQL **bootstrap-sample-db.sql**. Esse script é chamado pelo script de inicialização.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para o cluster de Big Data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome que você atribuiu ao cluster de Big Data. |
   | <SQL_MASTER_ENDPOINT> | O nome DNS ou o endereço IP da instância mestre. |
   | <KNOX_ENDPOINT> | O nome DNS ou o endereço IP do gateway de HDFS/Spark. |
   
   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP da instância mestre do SQL Server e o Knox. Execute `kubectl get svc -n <your-big-data-cluster-name>` e examine os endereços IP externos da instância mestra (**master-svc-external**) e do Knox (**gateway-svc-external**). O nome padrão de um cluster é **mssql-cluster**.

1. Execute o script de inicialização.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## <a name="linux"></a><a id="linux"></a> Linux

As etapas a seguir descrevem como usar um cliente do Linux para carregar os dados de exemplo em seu cluster de Big Data.

1. Baixe o script de inicialização e atribua permissões executáveis a ele.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Baixe o script Transact-SQL **bootstrap-sample-db.sql**. Esse script é chamado pelo script de inicialização.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para o cluster de Big Data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome que você atribuiu ao cluster de Big Data. |
   | <SQL_MASTER_ENDPOINT> | O nome DNS ou o endereço IP da instância mestre. |
   | <KNOX_ENDPOINT> | O nome DNS ou o endereço IP do gateway de HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP da instância mestre do SQL Server e o Knox. Execute `kubectl get svc -n <your-big-data-cluster-name>` e examine os endereços IP externos da instância mestra (**master-svc-external**) e do Knox (**gateway-svc-external**). O nome padrão de um cluster é **mssql-cluster**.

1. Execute o script de inicialização.

   ```bash
   ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## <a name="next-steps"></a>Próximas etapas

Depois que o script de inicialização for executado, seu cluster de Big Data terá os bancos de dados de exemplo e dados do HDFS. Os tutoriais a seguir usam os dados de exemplo para demonstrar os recursos do cluster de Big Data:

Virtualização de dados:

- [Tutorial: Consultar o HDFS em um cluster de Big Data do SQL Server](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Consultar o Oracle em um cluster de Big Data do SQL Server](tutorial-query-oracle.md)

Ingestão de dados:

- [Tutorial: Ingerir dados em um pool de dados do SQL Server com Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Ingerir dados em um pool de dados do SQL Server com trabalhos do Spark](tutorial-data-pool-ingest-spark.md)

Notebooks:

- [Tutorial: Executar um notebook de exemplo em um cluster de Big Data do SQL Server 2019](notebooks-tutorial-spark.md)
