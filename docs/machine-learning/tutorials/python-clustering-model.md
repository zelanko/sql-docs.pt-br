---
title: 'Tutorial do Python: Categorizar usuários'
description: Nesta série de tutoriais de quatro partes, você executará o clustering de clientes, usando o K-Means, em um Banco de Dados SQL usando Python com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 12/17/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7112b89375251244ba54182197855e0bed412455
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116519"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>Tutorial: Categorizar clientes que usam clustering de K-Means com Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nesta série de tutoriais de quatro partes, você usará o Python para desenvolver e implantar um modelo de clustering de K-Means nos [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md) para os dados do cliente do cluster.

Na primeira parte desta série, você configurará os pré-requisitos para o tutorial e, em seguida, restaurará um conjunto de dados de exemplo para um Banco de Dados SQL. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de clustering em Python com os Serviços de Machine Learning do SQL Server.

Nas partes dois e três desta série, você desenvolverá alguns scripts do Python em um notebook do Azure Data Studio para analisar e preparar seus dados e treinar um modelo de machine learning. Em seguida, na parte quatro, você executará esses scripts Python dentro de um Banco de Dados SQL usando procedimentos armazenados.

O *clustering* pode ser explicado como organizador de dados em grupos, nos quais os membros de um grupo são semelhantes de algum modo. Para esta série de tutoriais, imagine que você tenha uma empresa de varejo. Você usará o algoritmo **K-Means** para executar o clustering de clientes em um conjunto de dados de compras e devoluções de produtos. Ao realizar o clustering de clientes, você pode concentrar seus esforços de marketing com mais eficiência, direcionando-os a grupos específicos.
O clustering de K-Means é um algoritmo de *aprendizado não supervisionado* que procura padrões em dados com base em semelhanças.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Restaurar um banco de dados de exemplo em uma instância do SQL Server

Na [parte dois](python-clustering-model-prepare-data.md), você aprenderá a preparar os dados de um Banco de Dados SQL para executar o clustering.

Na [parte três](python-clustering-model-build.md), você aprenderá a criar e treinar um modelo de cluster K-means em Python.

Na [parte quatro](python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um Banco de Dados SQL que pode executar clusters em Python com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md) com a opção de linguagem Python – siga as instruções de instalação no [guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou no [guia de instalação do Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fmachine-learning%2ftoc.json&view=sql-server-linux-ver15).

* [Azure Data Studio](../../azure-data-studio/what-is.md). Você usará um notebook no Azure Data Studio para Python e para SQL. Para obter mais informações sobre notebooks, confira [Como usar notebooks no Azure Data Studio](../../azure-data-studio/sql-notebooks.md).

  * Python – você também pode usar seu IDE do Python, tal como um Jupyter Notebook ou um [Visual Studio Code](https://code.visualstudio.com/docs), com a [extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e a [extensão do MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).
  * SQL – você também pode usar o SSMS ([SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md)).

* Pacotes do Python adicionais – os exemplos nesta série de tutoriais usam pacotes do Python que você pode ou não ter instalado.

  Abra um **Prompt de Comando** e altere para o caminho de instalação da versão do Python que você usa em Azure Data Studio. Por exemplo, `cd %LocalAppData%\Programs\Python\Python37-32`. Em seguida, execute os comandos a seguir para instalar qualquer um desses pacotes que ainda não estão instalados.

  ```console
  pip install matplotlib
  pip install pandas
  pip install pyodbc
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>Restaurar o banco de dados de exemplo

O conjunto de dados de exemplo usado neste tutorial foi salvo em um arquivo **.bak** de backup de banco de dados para você baixar e usar. Esse conjunto de dados é derivado do conjunto de dados [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp), fornecido pela [TPC (Transaction Processing Performance Council)](http://www.tpc.org/default.asp).

1. Baixe o arquivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Siga as instruções em [Restaurar um banco de dados de um arquivo de backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) no Azure Data Studio, usando estes detalhes:

   * Importe do arquivo **tpcxbb_1gb.bak** que você baixou
   * Nomeie o banco de dados de destino como "tpcxbb_1gb"

1. Consultando a tabela **dbo.customer**, é possível verificar se o conjunto de dados existe depois de você ter restaurado o banco de dados:

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Restaurar um banco de dados de exemplo em uma instância do SQL Server

Para preparar os dados para o modelo de machine learning, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Preparar dados para realizar clustering de clientes em Python com os Serviços de Machine Learning do SQL Server](python-clustering-model-prepare-data.md)
