---
title: Usar Jupyter Notebooks no Azure Data Studio
description: Saiba como começar a usar Jupyter Notebooks no Azure Data Studio.
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: seo-lt-2019
ms.date: 07/01/2020
ms.openlocfilehash: 7e61b31a21a6a3a85a9830bc73a7d62777c78b9b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920484"
---
# <a name="use-jupyter-notebooks-in-azure-data-studio"></a>Usar Jupyter Notebooks no Azure Data Studio

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O Jupyter Notebook é um aplicativo Web de código-fonte aberto que permite que criar e compartilhar documentos que contêm código ao vivo, equações, visualizações e texto narrativo. O uso inclui limpeza de dados e transformação, simulação numérica, modelagem estatística, visualização de dados e aprendizado de máquina.

Este artigo descreve como criar um notebook na versão mais recente do [**Azure Data Studio**](../azure-data-studio/download.md) e como começar a criar seus próprios notebooks usando diferentes kernels.

Assista a este vídeo breve de 5 minutos para ver uma introdução sobre notebooks no Azure Data Studio:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-notebook"></a>Criar um notebook

Há várias maneiras de criar um notebook. Em todos os casos, um novo arquivo chamado `Notebook-1.ipynb` é aberto.

- Acesse o **Menu Arquivo** no Azure Data Studio e selecione **Novo Notebook**.

  ![Novo notebook](media/notebooks-guidance/file-new-notebook.png)

- Clique com o botão direito do mouse na conexão **SQL Server** e selecione **Novo Notebook**.

  ![Novo notebook](media/notebooks-guidance/server-new-notebook.png)

- Abra a paleta de comandos (**Ctrl + Shift + P**), digite "novo notebook" e selecione o comando **Novo Notebook**.

  ![Novo notebook](media/notebooks-guidance/command-palette-new-notebook.png)

## <a name="connect-to-a-kernel"></a>Conectar-se a um kernel

Os notebooks do Azure Data Studio dão suporte a vários kernels diferentes, incluindo SQL Server, Python, PySpark e outros. Cada kernel dá suporte a uma linguagem diferente nas células de código do notebook. Por exemplo, quando conectado ao kernel do SQL Server, você pode inserir e executar instruções T-SQL em uma célula de código do notebook.

**Anexar a** fornece o contexto do kernel. Por exemplo, se estiver usando o Kernel do SQL, você poderá usar anexar a qualquer uma de suas instâncias do SQL Server.
Se estiver usando o Kernel do Python3, anexe a **localhost** e você poderá usar esse kernel para desenvolvimento de Python local.

O Kernel do SQL também pode ser usado para se conectar a instâncias do servidor PostgreSQL. Se você for um desenvolvedor de PostgreSQL e quiser conectar os notebooks ao Servidor PostgreSQL, baixe a [**extensão do PostgreSQL**](../azure-data-studio/postgres-extension.md) no Marketplace de extensões do Azure Data Studio e se conecte ao servidor PostgreSQL.

Se você estiver conectado ao cluster de Big Data do SQL Server 2019, o valor padrão de **Anexar a** será o ponto de extremidade do cluster. Você pode enviar o código Python, Scala e R usando a computação de Spark do cluster.

| Kernel                      | Descrição                                                  |
|:----------------------------|:-------------------------------------------------------------|
| Kernel do SQL                  | Escreva o código SQL direcionado ao seu banco de dados relacional.         |
| Kernel PySpark3 e PySpark | Escreva o código Python usando a computação do Spark do cluster.      |
| Kernel do Spark                | Escreva o código Scala e R usando a computação do Spark do cluster. |
| Kernel do Python               | Escreva o código Python para desenvolvimento local.                     |

Para obter mais informações sobre kernels específicos, confira:

- [Criar e executar um notebook do SQL Server](notebooks-tutorial-sql-kernel.md)
- [Criar e executar um notebook do Python](notebooks-tutorial-python-kernel.md)
- [Extensão Kqlmagic no Azure Data Studio](notebooks-kqlmagic.md) – estende os recursos do kernel de Python

## <a name="add-a-code-cell"></a>Adicionar uma célula de código

As células de código permitem executar código interativamente no notebook.

Adicione uma nova célula de código clicando no comando **+Célula** na barra de ferramentas e selecionando **Célula de código**. Uma nova célula de código é adicionada após a célula selecionada.

Insira o código na célula para o kernel selecionado. Por exemplo, se estiver usando o kernel do SQL, você poderá inserir comandos T-SQL na célula de código.

Inserir código com o kernel do SQL é semelhante a um editor de consultas SQL. A célula de código dá suporte a uma experiência moderna de codificação em SQL com recursos internos como um editor SQL avançado, o IntelliSense e trechos de código internos. Os snippets de código permitem que você gere a sintaxe SQL correta para criar bancos de dados, tabelas, exibições, procedimentos armazenados e atualizar objetos de banco de dados existentes. Use snippets de código para criar rapidamente cópias de seu banco de dados para fins de desenvolvimento ou teste e para gerar e executar scripts.

![Kernel do SQL](media/notebooks-guidance/intellisense-code-cell.png)

## <a name="add-a-text-cell"></a>Adicionar uma célula de texto

As células de texto permitem que você documente seu código adicionando blocos de texto de Markdown entre as células de código.

Adicione uma nova célula de texto clicando no comando **+Célula** na barra de ferramentas e selecionando **Célula de texto**.

A célula é iniciada no modo de edição, no qual você pode digitar o texto de Markdown. Conforme você digita, uma visualização é mostrada abaixo.

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Selecionar fora da célula de texto mostra o texto de Markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

Se você clicar na célula de texto novamente, ela será alterada para o modo de edição.

## <a name="run-a-cell"></a>Executar uma célula

Para executar apenas uma célula, clique em **Executar célula** (a seta preta arredondada) à esquerda da célula ou selecione a célula e pressione F5. Você pode executar todas as células no notebook clicando em **Executar tudo** na barra de ferramentas. As células são executadas uma por vez e a execução é interrompida quando um erro é encontrado em uma célula.

Os resultados da célula são mostrados abaixo dela. Você pode limpar os resultados de todas as células executadas no notebook selecionando o botão **Limpar Resultados** na barra de ferramentas.

## <a name="save-a-notebook"></a>Salvar um notebook

Para salvar um notebook, realize um dos procedimentos a seguir.

- Digite Ctrl+S
- Selecione **Salvar** no menu **Arquivo**
- Selecione **Salvar como...** no menu **Arquivo**
- Selecione **Salvar todos** no menu **Arquivo**, o que salva todos os notebooks abertos
- Na paleta de comandos, insira **Arquivo: Salvar**

Os notebooks são salvos como arquivos `.ipynb`.

## <a name="trusted-and-non-trusted"></a>Confiável e não confiável

Os notebooks abertos no Azure Data Studio são **Confiáveis** por padrão.

Se você abrir um notebook de outra fonte, ele será aberto no modo **Não Confiável** e poderá ser configurado como **Confiável**.

## <a name="examples"></a>Exemplos

Os exemplos a seguir demonstram o uso de kernels diferentes para executar um comando "Olá, Mundo" simples. Selecione o kernel, insira o código de exemplo em uma célula e clique em **Executar célula**.

### <a name="pyspark"></a>Pyspark

![Aplicativo Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark--scala-language"></a>Spark | Linguagem Scala

![Spark Scala](media/notebooks-guidance/spark-scala.png)

### <a name="spark--r-language"></a>Spark | Linguagem R

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="python-3"></a>Python 3

![Python local](media/notebooks-guidance/local-python.png)

## <a name="next-steps"></a>Próximas etapas

- [Criar e executar um notebook do SQL Server](notebooks-tutorial-sql-kernel.md).
- [Criar e executar um notebook do Python](notebooks-tutorial-python-kernel.md)
- [Execute scripts Python e R em notebooks no Azure Data Studio com os Serviços de Machine Learning do SQL Server](../machine-learning/install/sql-machine-learning-azure-data-studio.md).
- [Implantar um cluster de Big Data do SQL Server com o notebook do Azure Data Studio](../big-data-cluster/notebooks-deploy.md).
- [Gerenciar Clusters de Big Data do SQL Server com notebooks do Azure Data Studio](../big-data-cluster/notebooks-manage-bdc.md).
- [Executar um notebook de exemplo usando o Spark](../big-data-cluster/notebooks-tutorial-spark.md).
