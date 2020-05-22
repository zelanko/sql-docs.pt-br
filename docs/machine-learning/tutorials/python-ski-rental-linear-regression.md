---
title: 'Tutorial do Python: Locações de esqui'
titleSuffix: SQL machine learning
description: Nesta série de tutoriais de quatro partes, você criará um modelo de regressão linear em Python para prever os aluguéis de esqui com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b34687440763f2c514016989542ae3f2d7c0e6ed
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606903"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-with-sql-machine-learning"></a>Tutorial do Python: Prever o aluguel de esquis com regressão linear com aprendizado de máquina do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Nesta séries de tutoriais de quatro partes, você usará a regressão linear e o Python nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md) para prever o número de aluguéis de esqui. O tutorial usa um [notebook do Python no Azure Data Studio](../../azure-data-studio/sql-notebooks.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Nesta séries de tutoriais de quatro partes, você usará a regressão linear e o Python nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) para prever o número de locações de esqui. O tutorial usa um [notebook do Python no Azure Data Studio](../../azure-data-studio/sql-notebooks.md).
::: moniker-end

Imagine que você tenha um negócio de aluguel de esqui e queira prever o número de locações que você terá em uma data futura. Essas informações ajudarão você a preparar seu estoque, sua equipe e suas instalações.

Na primeira parte desta série, você se preparará com os pré-requisitos. Nas partes dois e três, você desenvolverá alguns scripts do Python em um notebook para preparar seus dados e treinar um modelo de machine learning. Em seguida, na parte três, você executará esses scripts Python dentro do SQL Server usando procedimentos armazenados do T-SQL.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Importar um banco de dados de exemplo no SQL Server 

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprenderá a carregar os dados de um banco de dados em uma estrutura do Python e a prepará-los no Python.

Na [parte três](python-ski-rental-linear-regression-train-model.md), você aprenderá a treinar um modelo de regressão linear no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo em um banco de dados e, em seguida, criará procedimentos armazenados com base nos scripts do Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no servidor para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* Serviços de Machine Learning do SQL Server – para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* Serviços de Machine Learning do SQL Server – para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end

* IDE do Python – este tutorial usa um notebook Python no [Azure Data Studio](../../azure-data-studio/what-is.md). Para obter mais informações, confira [Como usar notebooks no Azure Data Studio](../../azure-data-studio/sql-notebooks.md).

* Ferramenta de consulta SQL – este tutorial pressupõe que você está usando o [Azure Data Studio](../../azure-data-studio/what-is.md).

* Pacotes adicionais do Python – os exemplos nesta série de tutoriais usam os seguintes pacotes do Python que podem ou não estar instalados por padrão:

  * pandas
  * pyodbc
  * sklearn

  Para instalar esses pacotes:
  1. No Azure Data Studio, selecione **Gerenciar Pacotes**.
  2. No painel **Gerenciar Pacotes**, selecione a guia **Adicionar Novo**.
  3. Para cada pacote a seguir, insira o nome do pacote, clique em **Pesquisar**e em **Instalar**.

  Como alternativa, você pode abrir um **Prompt de Comando**, alterar para o caminho de instalação da versão do Python usada no Azure Data Studio (por exemplo, `cd %LocalAppData%\Programs\Python\Python37-32`) e executar `pip install` para cada pacote.

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
* Importar um banco de dados de exemplo no SQL Server

Para preparar os dados do banco de dados TutorialDB, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Preparar os dados para treinar um modelo de regressão linear](python-ski-rental-linear-regression-prepare-data.md)