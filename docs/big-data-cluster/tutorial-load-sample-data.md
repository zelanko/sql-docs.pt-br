---
title: Carregar dados de exemplo
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial demonstra como carregar dados de exemplo em um cluster de big data do SQL Server. Os dados de exemplo incluem dados relacionais na instância mestre do SQL Server. Ele também inclui dados do HDFS no pool de armazenamento. Esses dados dá suporte a outros tutoriais nesta seção.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 207d2d01278d96456bcec44814efe76fdae70fdf
ms.sourcegitcommit: e3f5b70bbb4c66294df8c7b2c70186bdf2365af9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397505"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-2019-big-data-cluster"></a>Tutorial: Carregar dados de exemplo em um cluster de big data do SQL Server de 2019

Este tutorial explica como usar um script para carregar dados de exemplo em um cluster de big data do SQL Server 2019 (visualização). Muitos dos tutoriais na documentação do usam esses dados de exemplo.

> [!TIP]
> Você pode encontrar exemplos adicionais para o cluster de big data de 2019 do SQL Server (versão prévia) na [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) repositório do GitHub. Eles estão localizados os **sql-server-samples/samples/features/sql-big-data-cluster/** caminho.

## <a name="prerequisites"></a>Prerequisites

- [Um cluster de big data implantados](deployment-guidance.md)
- [Ferramentas de big data](deploy-big-data-tools.md)
   - **mssqlctl**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> Carregar dados de exemplo

As etapas a seguir usam um script de inicialização para baixar um backup de banco de dados do SQL Server e carregar os dados em seu cluster de big data. Para facilidade de uso, essas etapas foram divididas [Windows](#windows) e [Linux](#linux) seções.

## <a id="windows"></a> Windows

As etapas a seguir descrevem como usar um cliente do Windows para carregar os dados de exemplo no seu cluster de big data.

1. Abra um novo prompt de comando do Windows.

   > [!IMPORTANT]
   > Não use o Windows PowerShell para essas etapas. No PowerShell, o script falhará, pois ele usará a versão do PowerShell do **curl**.

1. Use **curl** para baixar o script de inicialização para os dados de exemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Baixe o **bootstrap-exemplo-db.sql** script Transact-SQL. Esse script é chamado pelo script de inicialização.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para seu cluster de big data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome fornecido para seu cluster de big data. |
   | <SQL_MASTER_IP> | O endereço IP da sua instância do mestre. |
   | <SQL_MASTER_SA_PASSWORD> | A senha de SA para a instância mestre. |
   | <KNOX_IP> | O endereço IP do Gateway de HDFS/Spark. |
   | <KNOX_PASSWORD> | A senha para o Gateway HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP para a instância mestre do SQL Server e o Knox. Execute `kubectl get svc -n <your-cluster-name>` e examine os endereços de IP externo para a instância mestre (**ponto de extremidade de mestre de pool**) e Knox (**serviço-segurança-lb** ou **serviço-segurança-nodeport**).

1. Execute o script de inicialização.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

As etapas a seguir descrevem como usar um cliente Linux para carregar os dados de exemplo no seu cluster de big data.

1. Baixe o script de inicialização e atribua permissões executáveis a ele.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Baixe o **bootstrap-exemplo-db.sql** script Transact-SQL. Esse script é chamado pelo script de inicialização.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. O script de inicialização requer os seguintes parâmetros posicionais para seu cluster de big data:

   | Parâmetro | Descrição |
   |---|---|
   | <CLUSTER_NAMESPACE> | O nome fornecido para seu cluster de big data. |
   | <SQL_MASTER_IP> | O endereço IP da sua instância do mestre. |
   | <SQL_MASTER_SA_PASSWORD> | A senha de SA para a instância mestre. |
   | <KNOX_IP> | O endereço IP do Gateway de HDFS/Spark. |
   | <KNOX_PASSWORD> | A senha para o Gateway HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para localizar os endereços IP para a instância mestre do SQL Server e o Knox. Execute `kubectl get svc -n <your-cluster-name>` e examine os endereços de IP externo para a instância mestre (**ponto de extremidade de mestre de pool**) e Knox (**serviço-segurança-lb** ou **serviço-segurança-nodeport**).

1. Execute o script de inicialização.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Próximas etapas

Depois que o script de inicialização é executado, o seu cluster de big data tem bancos de dados de exemplo e dados do HDFS. Para começar a explorar esses dados e os clusters de big data, consulte o [tutoriais](tutorial-query-hdfs-storage-pool.md) nesta seção.
