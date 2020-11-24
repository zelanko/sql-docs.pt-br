---
title: 'Tutorial: Desenvolver um modelo de clustering no R'
titleSuffix: SQL Machine Learning
description: Nesta série de tutoriais de quatro partes, você desenvolverá um modelo para executar clustering no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/26/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 8ee1d60eb9af4232957ff9c1a7df4b976366513f
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870306"
---
# <a name="tutorial-develop-a-clustering-model-in-r-with-sql-machine-learning"></a>Tutorial: Desenvolver um modelo de clustering no R com o machine learning do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Nesta série de tutoriais de quatro partes, você usará o R para desenvolver e implantar um modelo de cluster K-Means nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md) para categorizar dados de clientes.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Nesta série de tutoriais de quatro partes, você usará o R para desenvolver e implantar um modelo de cluster K-Means nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) para os dados de clientes do cluster.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Nesta série de tutoriais de quatro partes, você usará o R para desenvolver e implantar um modelo de cluster K-Means no [SQL Server R Services](../r/sql-server-r-services.md) para os dados de clientes do cluster.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Nesta série de tutoriais de quatro partes, você usará o R para desenvolver e implantar um modelo de cluster K-means do [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) nos dados do cliente do cluster.
::: moniker-end

Na primeira parte desta série, você configurará os pré-requisitos do tutorial e, em seguida, restaurará um conjunto de dados de exemplo para um banco de dados. Nas partes dois e três, você desenvolverá alguns scripts do R em um notebook do Azure Data Studio para analisar e preparar esses dados de exemplo e treinar um modelo de machine learning. Em seguida, na quarta parte, você executará esses scripts do R em um banco de dados usando os procedimentos armazenados.

O *clustering* pode ser explicado como organizador de dados em grupos, nos quais os membros de um grupo são semelhantes de algum modo. Para esta série de tutoriais, imagine que você tenha uma empresa de varejo. Você usará o algoritmo **K-Means** para executar o clustering de clientes em um conjunto de dados de compras e devoluções de produtos. Ao realizar o clustering de clientes, você pode concentrar seus esforços de marketing com mais eficiência, direcionando-os a grupos específicos. O clustering de K-Means é um algoritmo de *aprendizado não supervisionado* que procura padrões em dados com base em semelhanças.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Restaurar um banco de dados de exemplo

Na [parte dois](r-clustering-model-prepare-data.md), você aprenderá a preparar os dados de um banco de dados para executar clustering.

Na [parte três](r-clustering-model-build.md), você aprenderá a criar e treinar um modelo de cluster K-means no R.

Na [parte quatro](r-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados que pode executar clustering no R com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) com a opção de linguagem Python – siga as instruções de instalação no [guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou no [guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%252fsql%252fmachine-learning%252ftoc.json&view=sql-server-linux-ver15&preserve-view=true). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) com a opção de linguagem R – siga as instruções de instalação no [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para obter informações, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).

* [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) para restaurar o banco de dados de exemplo na Instância Gerenciada de SQL do Azure.
::: moniker-end

* [Azure Data Studio](../../azure-data-studio/what-is.md). Você usará um notebook no Azure Data Studio para SQL. Para obter mais informações sobre notebooks, confira [Como usar notebooks no Azure Data Studio](../../azure-data-studio/notebooks/notebooks-guidance.md).

* IDE do R – Este tutorial usa o [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

* RODBC – este driver é usado nos scripts do R que você desenvolverá neste tutorial. Se ele ainda não estiver instalado, instale-o usando o comando R `install.packages("RODBC")`. Para saber mais sobre o RODBC, confira [CRAN – Pacote RODBC](https://CRAN.R-project.org/package=RODBC).

## <a name="restore-the-sample-database"></a>Restaurar o banco de dados de exemplo

O conjunto de dados de exemplo usado neste tutorial foi salvo em um arquivo **.bak** de backup de banco de dados para você baixar e usar. Esse conjunto de dados é derivado do conjunto de dados [tpcx-bb](http://www.tpc.org/tpcx-bb/default5.asp), fornecido pela [TPC (Transaction Processing Performance Council)](http://www.tpc.org/).

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Se você estiver usando Serviços de Machine Learning em Clusters de Big Data, confira como [Restaurar um banco de dados na instância mestra de cluster de Big Data do SQL Server](../../big-data-cluster/data-ingestion-restore-database.md).
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
1. Baixe o arquivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Siga as instruções em [Restaurar um banco de dados de um arquivo de backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) no Azure Data Studio, usando estes detalhes:

   * Importe do arquivo **tpcxbb_1gb.bak** que você baixou
   * Nomeie o banco de dados de destino como "tpcxbb_1gb"

1. Consultando a tabela **dbo.customer**, é possível verificar se o conjunto de dados existe depois de você ter restaurado o banco de dados:

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
1. Baixe o arquivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Siga as instruções descritas em [Restaurar um banco de dados em uma Instância Gerenciada](/azure/sql-database/sql-database-managed-instance-get-started-restore) no SQL Server Management Studio usando estes detalhes:

   * Importe do arquivo **tpcxbb_1gb.bak** que você baixou
   * Nomeie o banco de dados de destino como "tpcxbb_1gb"

1. Consultando a tabela **dbo.customer**, é possível verificar se o conjunto de dados existe depois de você ter restaurado o banco de dados:

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```
::: moniker-end

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb.

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Instalar os pré-requisitos
* Restaurar um banco de dados de exemplo

Para preparar os dados para o modelo de machine learning, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Preparar dados para executar clustering](r-clustering-model-prepare-data.md)