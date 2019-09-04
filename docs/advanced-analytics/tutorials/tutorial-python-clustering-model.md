---
title: 'Tutorial: Executar clustering em Python'
description: Nesta série de tutoriais de quatro partes, você executará o clustering de clientes em um banco de dados SQL usando o Python com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 595652a2bfa7392d3b4f900082f33cc589631147
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238661"
---
# <a name="tutorial-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Executar clustering em Python com SQL Server Serviços de Machine Learning

Nesta série de tutoriais de quatro partes, você usará o Python para desenvolver e implantar um modelo de clustering K-means em [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md) aos dados do cliente de cluster.

Na parte um desta série, você configurará os pré-requisitos para o tutorial e, em seguida, importará um conjunto de dados de exemplo para um banco de dados SQL. Posteriormente nesta série, você usará esses dados para treinar e implantar um modelo de clustering em Python com SQL Server Serviços de Machine Learning.

Nas partes dois e três desta série, você desenvolverá alguns scripts de Python em um Azure Data Studio Notebook para analisar e preparar seus dados e treinar um modelo de aprendizado de máquina. Em seguida, na parte quatro, você executará esses scripts Python dentro de um banco de dados SQL usando procedimentos armazenados.

O clustering pode ser explicado como organizar dados em grupos em que os membros de um grupo são semelhantes de alguma forma. Para esta série de tutoriais, imagine que você possui uma empresa de varejo. Você usará o algoritmo **K-** means para executar o clustering de clientes em um conjunto de uma série de compras e Devoluções de produtos. Ao agrupar clientes, você pode concentrar seus esforços de marketing com mais eficiência, direcionando grupos específicos.
O clustering K-means é um algoritmo de *aprendizado* não supervisionado que procura padrões em dados com base em semelhanças.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Importar um banco de dados de exemplo em uma instância de SQL Server

Na [parte dois](tutorial-python-clustering-model-prepare-data.md), você aprenderá a preparar os dados de um banco de dado SQL para executar o clustering.

Na [terceira parte](tutorial-python-clustering-model-build.md), você aprenderá a criar e treinar um modelo de clustering K-means em Python.

Na [parte quatro](tutorial-python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados SQL que pode executar o clustering em Python com base em novas informações.

## <a name="prerequisites"></a>Pré-requisitos

* [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md) com a opção de linguagem Python – siga as instruções de instalação no [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou no guia de instalação do [Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15).

* Python IDE – este tutorial usa um bloco de notas do Python no [Azure Data Studio](../../azure-data-studio/what-is.md). Para obter mais informações, consulte [como usar blocos de anotações no Azure Data Studio](../../azure-data-studio/sql-notebooks.md). Você também pode usar seu próprio IDE do Python, como um notebook Jupyter ou [Visual Studio Code](https://code.visualstudio.com/docs) com a [extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e a [extensão MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).

* pacote [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) -o pacote **revoscalepy** está incluído no SQL Server serviços de Machine Learning. Para usar o pacote em um computador cliente, consulte [configurar um cliente de ciência de dados para desenvolvimento em Python](../python/setup-python-client-tools-sql.md) para obter opções para instalar esse pacote localmente.

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
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="import-the-sample-database"></a>Importar o banco de dados de exemplo

O conjunto de dados de exemplo usado neste tutorial foi salvo em um arquivo de backup de banco de dados **. bak** para download e uso. Esse conjunto de DataSet é derivado do conjunto de [tpcx-BB](http://www.tpc.org/tpcx-bb/default.asp) fornecido pelo [TPC (Conselho de desempenho de processamento de transações)](http://www.tpc.org/default.asp).

1. Baixe o arquivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) na pasta SQL Server Backup. Para a instância de banco de dados padrão, a pasta é:

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\`

1. Abra Azure Data Studio, conecte-se à sua instância do SQL Server e abra uma nova janela de consulta.

1. Execute os comandos a seguir para restaurar o banco de dados.

   ```sql
   USE master;
   GO

   RESTORE DATABASE tpcxbb_1gb
   FROM DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\tpcxbb_1gb.bak'
   WITH MOVE 'tpcxbb_1gb' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.mdf'
      , MOVE 'tpcxbb_1gb_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.ldf';
   GO
   ```

## <a name="clean-up-resources"></a>Limpar recursos

Se você não for continuar com este tutorial, exclua o banco de dados tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte um desta série de tutoriais, você concluiu estas etapas:

* Importar um banco de dados de exemplo em uma instância de SQL Server

Para preparar os dados para o modelo de aprendizado de máquina, siga a parte dois desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Preparar dados para executar o clustering em Python com SQL Server Serviços de Machine Learning](tutorial-python-clustering-model-prepare-data.md)
