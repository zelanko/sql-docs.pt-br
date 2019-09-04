---
title: 'Tutorial do Python: Locações de esqui (regressão linear)'
description: Neste tutorial, você usará a regressão linear e Python em SQL Server Serviços de Machine Learning para prever o número de locações de esqui.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242504"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Tutorial do Python: Prever o aluguel de esqui com regressão linear no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nesta série de tutoriais de quatro partes, você usará a regressão de Python e linear em [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md) para prever o número de locações de esqui. O tutorial usa um [Notebook Python em Azure Data Studio](../../azure-data-studio/sql-notebooks.md), mas você também pode usar seu próprio IDE (ambiente de desenvolvimento integrado) do Python.

Imagine que você tenha um negócio de aluguel de esqui e queira prever o número de locações que você terá em uma data futura. Essas informações ajudarão você a tornar suas ações, sua equipe e suas instalações prontas.

Na primeira parte desta série, você terá a configuração dos pré-requisitos. Nas partes dois e três, você desenvolverá alguns scripts Python em um notebook Jupyter para preparar seus dados e treinar um modelo de aprendizado de máquina. Em seguida, na parte três, você executará esses scripts do Python dentro SQL Server usando procedimentos armazenados do T-SQL.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Importar um banco de dados de exemplo no SQL Server 

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprenderá a carregar os dados de SQL Server em um quadro de dados do Python e a preparar os dados no Python.

Na [terceira parte](python-ski-rental-linear-regression-train-model.md), você aprenderá a treinar um modelo de regressão linear no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo para SQL Server e, em seguida, criar procedimentos armazenados a partir dos scripts Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no SQL Server para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* SQL Server Serviços de Machine Learning-para saber como instalar o Serviços de Machine Learning, consulte o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o guia de instalação do [Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json).

* Python IDE – este tutorial usa um bloco de notas do Python no [Azure Data Studio](../../azure-data-studio/what-is.md). Para obter mais informações, consulte [como usar blocos de anotações no Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    Você também pode usar seu próprio IDE do Python, como um notebook Jupyter ou [Visual Studio Code](https://code.visualstudio.com/docs) com a [extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e a [extensão MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* pacote [revoscalepy](../python/ref-py-revoscalepy.md) -o pacote **revoscalepy** está incluído no SQL Server serviços de Machine Learning. Para usar o pacote em um computador cliente, consulte [configurar um cliente de ciência de dados para desenvolvimento em Python](../python/setup-python-client-tools-sql.md) para obter opções para instalar esse pacote localmente.

    Se você estiver usando um bloco de anotações do Python em Azure Data Studio, siga estas etapas adicionais para usar o **revoscalepy**:

    1. Abrir Azure Data Studio
    1. No menu **arquivo** , selecione **preferências** e, em seguida, **configurações**
    1. Expanda **extensões** e selecione **configuração do notebook**
    1. Em **caminho do Python**, insira o caminho onde você instalou as bibliotecas (por exemplo `C:\path-to-python-for-mls`,)
    1. Certifique-se de que **usar python existente** está marcado
    1. Reiniciar Azure Data Studio

    Se você estiver usando um IDE do Python diferente, siga as etapas semelhantes para o IDE.

* Ferramenta de consulta SQL – este tutorial pressupõe que você esteja usando [Azure Data Studio](../../azure-data-studio/what-is.md). Você também pode usar o [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Pacotes python adicionais-os exemplos nesta série de tutoriais usam pacotes python que você pode ou não ter instalado. Use os comandos **Pip** a seguir para instalar esses pacotes, se necessário.

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>Restaurar o banco de dados de exemplo

O conjunto de dados de exemplo usado neste tutorial foi salvo em um arquivo de backup de banco de dados **. bak** para download e uso.

1. Baixe o arquivo [TutorialDB. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Siga as instruções em [restaurar um banco de dados de um arquivo de backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) em Azure Data Studio, usando estes detalhes:

   * Importar do arquivo **TutorialDB. bak** que você baixou
   * Nomeie o banco de dados de destino como "TutorialDB"

1. Você pode verificar se o conjunto de dados existe depois de ter restaurado a consulta da tabela **dbo. rental_data** :

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Instalou os pré-requisitos
* Importar um banco de dados de exemplo para um SQL Server

Para preparar os dados do banco de TutorialDB, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Preparar dados para treinar um modelo de regressão linear](python-ski-rental-linear-regression-prepare-data.md)