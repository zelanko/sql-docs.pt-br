---
title: Executar um exemplo de notebook | Microsoft Docs
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial mostra como você pode carregar uma execução de um exemplo de notebook Spark em um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 45845efe34c94f0c8f21c7e154dde673b0bfb889
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241837"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-2019-big-data-cluster"></a>Tutorial: Executar um exemplo de notebook em um cluster de big data do SQL Server de 2019

Este tutorial demonstra como carregar e executar um bloco de anotações no estúdio de dados do Azure em um cluster de big data do SQL Server 2019 (visualização). Isso permite que os cientistas de dados e engenheiros de dados para executar o código do Python, R ou Scala no cluster.

> [!TIP]
> Se você preferir, você pode baixar e executar um script para os comandos neste tutorial. Para obter instruções, consulte a [amostras do Spark](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de big data](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
- [Carregar dados de exemplo no seu cluster de big data](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>Baixe o arquivo do bloco de anotações de exemplo

Use as instruções a seguir para carregar o arquivo do bloco de anotações de amostra **sql.ipynb spark** no estúdio de dados do Azure.

1. Abra um prompt de comando do bash (Linux) ou o Windows PowerShell.

1. Navegue até um diretório em que você deseja baixar o arquivo do bloco de anotações de exemplo para.

1. Execute o seguinte **curl** comando para baixar o arquivo do bloco de anotações do GitHub:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark-sql.ipynb' -o spark-sql.ipynb
   ```

## <a name="open-the-notebook"></a>Abra o bloco de anotações

As etapas a seguir mostram como abrir o arquivo do bloco de anotações no estúdio de dados do Azure:

1. No estúdio de dados do Azure, conecte-se ao gateway de HDFS/Spark do seu cluster de big data. Para obter mais informações, consulte [conectar-se ao gateway de HDFS/Spark](connect-to-big-data-cluster.md#hdfs).

1. Clique duas vezes na conexão de gateway de HDFS/Spark na **servidores** janela. Em seguida, selecione **abrir Notebook**.

   ![Abrir notebook](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. Aguarde até que o **Kernel** e o contexto de destino (**anexar a**) a ser preenchido. Defina as **Kernel** para **PySpark3**e defina **anexar a** para o endereço IP do seu ponto de extremidade do cluster de big data.

   ![Defina o Kernel e anexar a](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Executar as células do bloco de anotações

Você pode executar cada célula de notebook, pressionando o botão Reproduzir para a esquerda da célula. Os resultados são mostrados no bloco de anotações após a célula a execução.

![Executar a célula de notebook](media/tutorial-notebook-spark/run-notebook-cell.png)

Execute cada uma das células no bloco de anotações de amostra em sucessão. Para obter mais informações sobre como usar blocos de anotações com clusters de grandes dados do SQL Server, consulte os seguintes recursos:

- [Como usar blocos de anotações na visualização do SQL Server de 2019](notebooks-guidance.md)
- [Como gerenciar notebooks no estúdio de dados do Azure](notebooks-how-to-manage.md)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os blocos de anotações:
> [!div class="nextstepaction"]
> [Saiba mais sobre os blocos de anotações](notebooks-guidance.md)