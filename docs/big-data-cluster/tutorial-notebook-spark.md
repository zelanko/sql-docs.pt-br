---
title: Executar um notebook de exemplo | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Este tutorial mostra como você pode carregar e executar um notebook de exemplo em um cluster de Big Data do SQL Server 2019 (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ab558194a67118719c144ea20f9e97496d2cb478
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957737"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-big-data-cluster"></a>Tutorial: Executar um notebook de exemplo em um cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como carregar e executar um notebook no Azure Data Studio em um cluster de Big Data do SQL Server 2019 (versão prévia). Isso permite que os cientistas e os engenheiros de dados executem código Python, R ou Scala no cluster.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos do Spark](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>Baixar o arquivo de notebook de exemplo

Use as instruções a seguir para carregar o arquivo de notebook de exemplo **spark-sql.ipynb** no Azure Data Studio.

1. Abra um prompt de comando do bash (Linux) ou o Windows PowerShell.

1. Navegue até um diretório no qual você deseja baixar o arquivo de notebook de exemplo.

1. Execute o seguinte comando de **rotação** para baixar o arquivo do notebook do GitHub:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>Abrir o notebook

As etapas a seguir mostram como abrir o arquivo do notebook no Azure Data Studio:

1. No Azure Data Studio, conecte-se à instância mestre do cluster de Big Data. Para obter mais informações, confira [Conectar-se a um cluster de Big Data](connect-to-big-data-cluster.md).

1. Clique duas vezes na conexão do gateway HDFS/Spark na janela **Servidores**. Em seguida, selecione **Abrir Notebook**.

   ![Abrir notebook](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. Aguarde até que o **Kernel** e o contexto de destino (**Anexar a**) sejam preenchidos. Defina o **Kernel** como **PySpark3** e defina **Anexar a** como o endereço IP do seu ponto de extremidade do cluster de Big Data.

   ![Definir o kernel e Anexar a](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Executar as células do notebook

Você pode executar cada célula do notebook pressionando o botão Reproduzir à esquerda da célula. Os resultados são mostrados no notebook após a conclusão da execução da célula.

![Executar célula do notebook](media/tutorial-notebook-spark/run-notebook-cell.png)

Execute cada uma das células no notebook de exemplo sucessivamente. Para obter mais informações sobre como usar notebooks com clusters de Big Data do SQL Server, confira os seguintes recursos:

- [Como usar notebooks na versão prévia do SQL Server 2019](notebooks-guidance.md)
- [Como gerenciar notebooks no Azure Data Studio](notebooks-how-to-manage.md)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:
> [!div class="nextstepaction"]
> [Saiba mais sobre os notebooks](notebooks-guidance.md)
