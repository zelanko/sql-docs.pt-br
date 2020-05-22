---
title: 'Tutorial: desenvolver um modelo preditivo no R'
titleSuffix: SQL machine learning
description: Nesta série de tutoriais de quatro partes, você desenvolverá dados para treinar um modelo preditivo no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 237b8d5ac797b6e17a48bde2fff12de55844755e
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83607139"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>Tutorial: preparar os dados para treinar um modelo preditivo no R com o aprendizado de máquina do SQL.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Nesta séries de tutoriais de quatro partes, você usará R e um modelo de machine learning nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md) para prever o número de aluguéis de esqui.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Nesta séries de tutoriais de quatro partes, você usará o R e um modelo de machine learning nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) para prever o número de aluguéis de esqui.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Nesta séries de tutoriais de quatro partes, você usará o R e um modelo de machine learning no [SQL Server R Services](../r/sql-server-r-services.md) para prever o número de aluguéis de esqui.
::: moniker-end

Imagine que você tenha um negócio de aluguel de esqui e queira prever o número de locações que você terá em uma data futura. Essas informações ajudarão você a preparar seu estoque, sua equipe e suas instalações.

Na primeira parte desta série, você se preparará com os pré-requisitos. Nas partes dois e três, você desenvolverá alguns scripts de R em um notebook para preparar seus dados e treinar um modelo de machine learning. Em seguida, na parte três, você executará esses scripts do R dentro do SQL Server usando procedimentos armazenados do T-SQL.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * restaurar um banco de dados de exemplo no SQL Server 

Na [parte dois](r-predictive-model-prepare-data.md), você aprenderá a carregar os dados de um banco de dados em uma estrutura do Python e a prepará-los no R.

Na [parte três](r-predictive-model-train.md), você aprenderá a treinar um modelo de machine learning no R.

Na [parte quatro](r-predictive-model-deploy.md), você aprenderá a armazenar o modelo em um banco de dados e, em seguida, criará procedimentos armazenados com base nos scripts do R desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no servidor para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* Serviços de Machine Learning do SQL Server – para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* Serviços de Machine Learning do SQL Server – para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end

* IDE do R – Este tutorial usa o [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/).

* RODBC – este driver é usado nos scripts do R que você desenvolverá neste tutorial. Se ele ainda não estiver instalado, instale-o usando o comando R `install.packages("RODBC")`. Para saber mais sobre o RODBC, confira [CRAN – Pacote RODBC](https://CRAN.R-project.org/package=RODBC).

* Ferramenta de consulta SQL – este tutorial pressupõe que você está usando o [Azure Data Studio](../../azure-data-studio/what-is.md). Para obter mais informações, confira [Como usar notebooks no Azure Data Studio](../../azure-data-studio/sql-notebooks.md).

## <a name="restore-the-sample-database"></a>Restaurar o banco de dados de exemplo

O banco de dados de exemplo usado neste tutorial foi salvo em um arquivo **.bak** de backup de banco de dados para você baixar e usar.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Se você estiver usando Serviços de Machine Learning em Clusters de Big Data, confira como [Restaurar um banco de dados na instância mestra de cluster de Big Data do SQL Server](../../big-data-cluster/data-ingestion-restore-database.md).
::: moniker-end

1. Baixe o arquivo [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Siga as instruções em [Restaurar um banco de dados de um arquivo de backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) no Azure Data Studio, usando estes detalhes:

   * Importe do arquivo **TutorialDB.bak** que você baixou
   * Nomeie o banco de dados de destino como "TutorialDB"

1. Para verificar se o banco de dados restaurado existe, consulte a tabela **dbo.rental_data**:

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

1. Habilite scripts externos executando os seguintes comandos SQL:

    ```sql
    sp_configure 'external scripts enabled', 1;
    RECONFIGURE WITH override;
    ```

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Instalar os pré-requisitos
* Restaurar um banco de dados de exemplo no SQL Server

Para preparar os dados para o modelo de machine learning, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Preparar os dados para treinar um modelo preditivo no R](r-predictive-model-prepare-data.md)
