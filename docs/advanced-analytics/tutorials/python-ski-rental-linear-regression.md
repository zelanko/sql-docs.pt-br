---
title: 'Tutorial do Python: Locações de esqui'
description: Neste tutorial, você usará a regressão linear e o Python nos Serviços de Machine Learning do SQL Server para prever o número de locações de esqui.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 927816988be8882d4149115f6d4aee38dd3a8f3f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727039"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nesta séries de tutoriais de quatro partes, você usará a regressão linear e o Python nos [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md) para prever o número de locações de esqui. O tutorial usa um [notebook do Python no Azure Data Studio](../../azure-data-studio/sql-notebooks.md), mas você também pode usar seu próprio IDE (ambiente de desenvolvimento integrado) do Python.

Imagine que você tenha um negócio de aluguel de esqui e queira prever o número de locações que você terá em uma data futura. Essas informações ajudarão você a preparar seu estoque, sua equipe e suas instalações.

Na primeira parte desta série, você se preparará com os pré-requisitos. Nas partes dois e três, você desenvolverá alguns scripts do Python em um Jupyter Notebook para preparar seus dados e treinar um modelo de machine learning. Em seguida, na parte três, você executará esses scripts Python dentro do SQL Server usando procedimentos armazenados do T-SQL.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Importar um banco de dados de exemplo no SQL Server 

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprenderá a carregar os dados do SQL Server em uma estrutura de dados do Python e a preparar os dados no Python.

Na [parte três](python-ski-rental-linear-regression-train-model.md), você aprenderá a treinar um modelo de regressão linear no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo no SQL Server e, em seguida, criará procedimentos armazenados com base nos scripts do Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no SQL Server para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Prerequisites

* Serviços de Machine Learning do SQL Server – para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json).

* IDE do Python – este tutorial usa um notebook Python no [Azure Data Studio](../../azure-data-studio/what-is.md). Para obter mais informações, confira [Como usar notebooks no Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    Você também pode usar seu próprio IDE do Python, tal como um Jupyter Notebook ou um [Visual Studio Code](https://code.visualstudio.com/docs), com a [extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e a [extensão do MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* Pacote do [revoscalepy](../python/ref-py-revoscalepy.md) – o pacote do **revoscalepy** está incluído nos Serviços de Machine Learning do SQL Server. Para usar o pacote em um computador cliente, confira [Configurar um cliente de ciência de dados para desenvolvimento em Python](../python/setup-python-client-tools-sql.md) para obter opções para instalar esse pacote localmente.

    Se você estiver usando um notebook do Python no Azure Data Studio, siga estas etapas adicionais para usar o **revoscalepy**:

    1. Abrir o Azure Data Studio
    1. No menu **Arquivo**, selecione **Preferências** e **Configurações**
    1. Expanda **Extensões** e selecione **Configuração do notebook**
    1. Em **Caminho do Python**, insira o caminho em que você instalou as bibliotecas (por exemplo, `C:\path-to-python-for-mls`)
    1. Verifique se a opção **Usar o Python Existente** está marcada
    1. Reiniciar o Azure Data Studio

    Se você estiver usando um IDE do Python diferente, siga as etapas semelhantes para o IDE.

* Ferramenta de consulta SQL – este tutorial pressupõe que você está usando o [Azure Data Studio](../../azure-data-studio/what-is.md). Você também pode usar o SSMS ([SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md)).

* Pacotes do Python adicionais – os exemplos nesta série de tutoriais usam pacotes do Python que você pode ou não ter instalado. Use os comandos do **pip** a seguir para instalar esses pacotes, se necessário.

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>Restaurar o banco de dados de exemplo

O conjunto de dados de exemplo usado neste tutorial foi salvo em um arquivo **.bak** de backup de banco de dados para você baixar e usar.

1. Baixe o arquivo [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Siga as instruções em [Restaurar um banco de dados de um arquivo de backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) no Azure Data Studio, usando estes detalhes:

   * Importe do arquivo **TutorialDB.bak** que você baixou
   * Nomeie o banco de dados de destino como "TutorialDB"

1. Depois de você ter restaurado o banco de dados, é possível verificar se o conjunto de dados existe, consultando para isso a tabela **dbo.rental_data**:

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Instalar os pré-requisitos
* Importar um banco de dados de exemplo no SQL Server

Para preparar os dados do banco de dados TutorialDB, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Preparar os dados para treinar um modelo de regressão linear](python-ski-rental-linear-regression-prepare-data.md)