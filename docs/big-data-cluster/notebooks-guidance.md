---
title: Executar notebooks no Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Este artigo explica como executar notebooks do Jupyter no Azure Data Studio conectado a um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 166964f97f5201d906ea2d1f6262b7a221eb2cba
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958295"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Como usar notebooks na versão prévia do SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como iniciar a experiência no Notebook na versão mais recente do [**Azure Data Studio**](../azure-data-studio/download.md) e como começar a criar seus próprios notebooks. Ele também mostra como escrever Notebooks usando kernels diferentes.

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Você pode se conectar ao tipo de conexão Microsoft SQL Server no Azure Data Studio.
No Azure Data Studio, você também pode pressionar F1 e clicar em **Nova Conexão** e conectar-se ao seu SQL Server.

![Informações de conexão](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Iniciar Notebooks

Há várias maneiras de iniciar um novo notebook.

- Vá para o **menu Arquivo** no Azure Data Studio e clique em **Novo Notebook**.

    ![Novo notebook](media/notebooks-guidance/file-new-notebook.png)

- Clique com o botão direito do mouse na conexão **SQL Server** e inicie o **Novo Notebook**.

    ![Novo notebook](media/notebooks-guidance/server-new-notebook.png)

- Abra a paleta de comandos (**Ctrl+Shift+P**) e digite **Novo Notebook**. Um novo arquivo chamado `Notebook-1.ipynb` é aberto.

## <a name="supported-kernels-and-attach-to-context"></a>Kernels com suporte e anexar ao contexto

A instalação do Notebook no Azure Data Studio dá suporte nativo ao Kernel do SQL. Se você for um desenvolvedor de SQL e quiser usar Notebooks, esse será o Kernel escolhido. 

O Kernel do SQL também pode ser usado para se conectar a instâncias do servidor PostgreSQL. Se você for um desenvolvedor PostgreSQL e quiser conectar os notebooks ao seu Servidor PostgreSQL, baixe a [**extensão do PostgreSQL**](../azure-data-studio/postgres-extension.md) no marketplace de extensão do Azure Data Studio e, em seguida, inicie o **Novo Notebook** para abrir uma instância do notebook para se conectar ao servidor PostgreSQL.

![Conexão PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel do SQL

Nas células de código dentro do Notebook, semelhante ao nosso editor de consultas, damos suporte à experiência moderna de codificação do SQL que facilita as tarefas diárias com recursos internos, como um editor SQL avançado, o IntelliSense e snippets de código internos. Os snippets de código permitem que você gere a sintaxe SQL adequada para criar bancos de dados, tabelas, exibições, procedimentos armazenados, entre outros, e para atualizar objetos de banco de dados existentes. Use snippets de código para criar rapidamente cópias de seu banco de dados para fins de desenvolvimento ou teste e para gerar e executar scripts.

Clique em **Executar** para executar cada célula.

Kernel do SQL para se conectar à instância do SQL Server

![Kernel do SQL](media/notebooks-guidance/intellisense-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/sql-cell-results.png)

Kernel do SQL para se conectar à instância do Servidor PostgreSQL 

![Conexão PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/pgsql-cell-results.png)

Se você quiser adicionar células de texto ao seu notebook existente anexado ao kernel do SQL, clique no comando **+Text** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você verá a visualização ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Clicar fora da célula de texto mostrará o texto de markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)


### <a name="configure-python-for-notebooks"></a>Configurar o Python para Notebooks

Ao selecionar qualquer um dos outros kernels além do SQL na lista suspensa de kernels, você precisa **Configurar o Python para Notebooks**. As dependências do Notebook são instaladas em uma localização especificada, mas você pode decidir se deseja definir a localização de instalação. Essa instalação pode levar algum tempo e é recomendável não fechar o aplicativo até que ela seja concluída. Quando a instalação for concluída, você poderá começar a escrever o código na linguagem com suporte.

![Configurar o Python](media/notebooks-guidance/configure-python.png)

Depois que a instalação for realizada com sucesso, você encontrará uma notificação no Histórico de Tarefas junto com a localização do servidor de back-end do Jupyter em execução no Terminal de Saída.

![Back-end do Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descrição
|:-----|:-----
| Kernel do SQL | Escreva o código SQL direcionado ao seu banco de dados relacional.
|Kernel PySpark3 e PySpark| Escreva o código Python usando a computação do Spark do cluster.
|Kernel do Spark|Escreva o código Scala e R usando a computação do Spark do cluster.
|Kernel do Python|Escreva o código Python para desenvolvimento local.

`Attach to` fornece o contexto para o kernel a ser anexado. Se estiver usando o Kernel do SQL, você poderá usar `Attach to` para qualquer uma de suas instâncias do SQL Server.

Se você estiver usando o Kernel do Python3, `Attach to` será `localhost`. Você pode usar esse kernel para o desenvolvimento local do Python.

Quando você estiver conectado ao cluster de Big Data do SQL Server 2019, o `Attach to` padrão será o ponto de extremidade do cluster e permitirá que você envie código Python, Scala e R usando a computação de Spark do cluster.

### <a name="code-cells-and-markdown-cells"></a>Células de código e células de Markdown

Adicione uma nova célula de código clicando no comando **+Code** na barra de ferramentas.

Adicione uma nova célula de texto clicando no comando **+Text** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você verá a visualização ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Clicar fora da célula de texto mostrará o texto de markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Confiável e não confiável

Os Notebooks abertos no Azure Data Studio são **Confiáveis** por padrão.

Se você abrir um Notebook de alguma outra fonte, ele será aberto no modo **Não Confiável** e você poderá configurá-lo como **Confiável**.

### <a name="run-cells"></a>Executar células
Se você quiser executar todas as células no Notebook, clique no botão **Executar Células** na barra de ferramentas.

![Texto de markdown](media/notebooks-guidance/run-cell.png)


### <a name="clear-results"></a>Limpar Resultados

Se você quiser limpar os resultados de todas as células executadas no Notebook, poderá clicar no botão **Limpar Resultados** na barra de ferramentas.

![Texto de markdown](media/notebooks-guidance/clear-results.png)

### <a name="save"></a>Salvar

Para salvar o notebook, siga um destes procedimentos.

- Selecione Ctrl+S
- Clique em **Arquivo** > **Salvar**
- Clique em **Arquivo** > **Salvar Como...**
- Clique em **Arquivo** > **Salvar Tudo** 
- Na paleta de comandos, insira **Arquivo: Salvar** 

### <a name="pyspark3pyspark-kernel"></a>Kernel do Pyspark3/PySpark

Escolha o `PySpark Kernel` e, na célula, digite o código a seguir.

Clique em **Executar**.

O Aplicativo Spark é iniciado e retorna a seguinte saída:

![Aplicativo Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel do Spark | Linguagem Scala

Escolha o `Spark|Scala Kernel` e, na célula, digite o código a seguir.

![Spark Scala](media/notebooks-guidance/spark-scala.png)

Você também pode exibir as "Opções de Célula" clicando no ícone de opções abaixo –

![Opções de célula](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel do Spark | Linguagem R

Escolha Spark | R no menu suspenso de kernels. Na célula, digite ou cole o código. Clique em **Executar** para ver a seguinte saída.

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel do Python local

Escolha o Kernel do Python local e, na célula, digite -

![Python local](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Gerenciar pacotes

Um dos aspectos que otimizamos para o desenvolvimento de Python local foi a inclusão da capacidade de instalar pacotes de que os clientes precisariam para seus cenários. Por padrão, incluímos os pacotes comuns, como `pandas`, `numpy` etc., mas se você estiver esperando um pacote que não está incluído, escreva o seguinte código na célula do notebook: 

```python
import <package-name>
```

Quando você executa esse comando, `Module not found` é retornado. Se o pacote existir, você não receberá o erro.

Se ele retornar um erro `Module not Found`, clique em **Gerenciar Pacotes** para iniciar o terminal. Agora você pode instalar pacotes localmente. Use os comandos a seguir para instalar os pacotes:

```bash
./pip install <package-name>
```

   > [!Tip]
   > No Mac, siga as instruções na janela do Terminal para instalar pacotes. 

Depois que o pacote for instalado, você poderá ir para a célula do Notebook e digitar o seguinte comando:

```python
import <package-name>
```

Para desinstalar um pacote, use o seguinte comando do seu terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Próximas etapas

Para saber como trabalhar com um notebook existente, confira [Como gerenciar notebooks no Azure Data Studio](notebooks-how-to-manage.md).