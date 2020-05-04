---
title: Usar Jupyter Notebooks no Azure Data Studio com o SQL Server
description: Saiba como começar a usar Notebooks no Azure Data Studio.
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: seo-lt-2019
ms.date: 03/30/2020
ms.openlocfilehash: 480b5df927adddd38b8f9f2ea13fa25c3f653606
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178613"
---
# <a name="notebooks-with-sql-server-in-azure-data-studio"></a>Notebooks com o SQL Server no Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O Jupyter Notebook é um aplicativo Web de código-fonte aberto que permite que criar e compartilhar documentos que contêm código ao vivo, equações, visualizações e texto narrativo. O uso inclui limpeza de dados e transformação, simulação numérica, modelagem estatística, visualização de dados e aprendizado de máquina.

Este artigo descreve como iniciar a experiência no Notebook na versão mais recente do [**Azure Data Studio**](../azure-data-studio/download.md) e como começar a criar seus próprios notebooks. Ele também mostra como escrever Notebooks usando kernels diferentes.

Assista a este vídeo breve de 5 minutos para obter uma introdução sobre notebooks no Azure Data Studio:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Você pode se conectar ao tipo de conexão Microsoft SQL Server no Azure Data Studio.
No Azure Data Studio, selecione também F1 e **Nova Conexão** e conecte-se ao SQL Server.

![Informações de conexão](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Iniciar Notebooks

Há várias maneiras de iniciar um novo notebook.

- Acesse o **menu Arquivo** no Azure Data Studio e, em seguida, selecione **Novo Notebook**.

    ![Novo notebook](media/notebooks-guidance/file-new-notebook.png)

- Selecione com o botão direito do mouse a conexão **SQL Server** e, em seguida, inicie o **Novo Notebook**.

    ![Novo notebook](media/notebooks-guidance/server-new-notebook.png)

- Abra a paleta de comandos (**Ctrl+Shift+P**) e digite **Novo Notebook**. Um novo arquivo chamado `Notebook-1.ipynb` é aberto.

## <a name="supported-kernels-and-attach-to-context"></a>Kernels com suporte e anexar ao contexto

A instalação do Notebook no Azure Data Studio dá suporte nativo ao Kernel do SQL. Se você for um desenvolvedor do SQL e desejar usar Notebooks, o kernel do SQL será o kernel escolhido.

O Kernel do SQL também pode ser usado para se conectar a instâncias do servidor PostgreSQL. Se você for um desenvolvedor de PostgreSQL e quiser conectar os notebooks ao Servidor PostgreSQL, baixe a [**extensão do PostgreSQL**](../azure-data-studio/postgres-extension.md) no Marketplace de extensão do Azure Data Studio e, em seguida, inicie o **Novo Notebook** para abrir uma instância do notebook para se conectar ao servidor PostgreSQL.

![Conexão PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel do SQL

Nas células de código dentro do Notebook, semelhante ao nosso editor de consultas, damos suporte à experiência moderna de codificação do SQL que facilita as tarefas diárias com recursos internos, como um editor SQL avançado, o IntelliSense e snippets de código internos. Os snippets de código permitem que você gere a sintaxe SQL correta para criar bancos de dados, tabelas, exibições, procedimentos armazenados e atualizar objetos de banco de dados existentes. Use snippets de código para criar rapidamente cópias de seu banco de dados para fins de desenvolvimento ou teste e para gerar e executar scripts.

Selecione **Executar** para executar cada célula.

Kernel do SQL para se conectar à instância do SQL Server

![Kernel do SQL](media/notebooks-guidance/intellisense-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/sql-cell-results.png)

Kernel do SQL para se conectar à instância do Servidor PostgreSQL

![Conexão PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/pgsql-cell-results.png)

Caso deseje adicionar células de texto ao Notebook existente anexado ao kernel do SQL, selecione o comando **+Text** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você poderá ver a versão prévia ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

A seleção fora da célula de texto mostra o texto markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="configure-python-for-notebooks"></a>Configurar o Python para Notebooks

Ao selecionar um dos outros kernels além do SQL na lista suspensa de kernels, você precisará **Configurar o Python para Notebooks**. As dependências do Notebook são instaladas em uma localização especificada, mas você pode decidir se deseja definir a localização de instalação. Essa instalação pode levar algum tempo. É recomendável não fechar o aplicativo até que ela seja concluída. Quando a instalação for concluída, você poderá começar a escrever o código na linguagem com suporte.

![Configurar o Python](media/notebooks-guidance/configure-python.png)

Depois que a instalação for realizada com êxito, haverá uma notificação no Histórico de Tarefas junto com a localização do servidor de back-end do Jupyter em execução no Terminal de Saída.

![Back-end do Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descrição
|:-----|:-----
| Kernel do SQL | Escreva o código SQL direcionado ao seu banco de dados relacional.
|Kernel PySpark3 e PySpark| Escreva o código Python usando a computação do Spark do cluster.
|Kernel do Spark|Escreva o código Scala e R usando a computação do Spark do cluster.
|Kernel do Python|Escreva o código Python para desenvolvimento local.

`Attach to` fornece o contexto para o kernel a ser anexado. Se estiver usando o Kernel do SQL, você poderá usar `Attach to` para qualquer uma de suas instâncias do SQL Server.

Se você estiver usando o Kernel do Python3, `Attach to` será `localhost`. Você pode usar esse kernel para o desenvolvimento local do Python.

Quando você estiver conectado ao cluster de Big Data do SQL Server 2019, o `Attach to` padrão será o ponto de extremidade do cluster e permitirá que você envie código Python, Scala e R usando a computação do Spark do cluster.

### <a name="code-cells-and-markdown-cells"></a>Células de código e células de Markdown

Adicione uma nova célula de código selecionando o comando **+Code** na barra de ferramentas.

Adicione uma nova célula de texto selecionando o comando **+Text** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você poderá ver a versão prévia ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

A seleção fora da célula de texto mostra o texto markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Confiável e não confiável

Os Notebooks abertos no Azure Data Studio são **Confiáveis** por padrão.

Se você abrir um Notebook de outra fonte, ele será aberto no modo **Não Confiável** e poderá ser configurado como **Confiável**.

### <a name="run-cells"></a>Executar células

Caso deseje executar todas as células no Notebook, selecione o botão **Executar Células** na barra de ferramentas.

### <a name="clear-results"></a>Limpar Resultados

Caso deseje limpar os resultados de todas as células executadas no Notebook, selecione o botão **Limpar Resultados** na barra de ferramentas.

### <a name="save"></a>Salvar

Para salvar o notebook, realize um dos procedimentos a seguir.

- Selecione Ctrl+S
- Selecione **Arquivo** > **Salvar**
- Selecione **Arquivo** > **Salvar como...**
- Selecione **Arquivo** > **Salvar Todos**
- Na paleta de comandos, insira **Arquivo: Salvar**

### <a name="pyspark3pyspark-kernel"></a>Kernel do Pyspark3/PySpark

Escolha o `PySpark Kernel` e, na célula, digite o código a seguir.

Selecione **Executar**.

O Aplicativo Spark é iniciado e retorna a seguinte saída:

![Aplicativo Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel do Spark | Linguagem Scala

Escolha o `Spark|Scala Kernel` e, na célula, digite o código a seguir.

![Spark Scala](media/notebooks-guidance/spark-scala.png)

Você também pode ver as "Opções de Célula" selecionando o ícone de opções abaixo.

![Opções de célula](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel do Spark | Linguagem R

Escolha Spark | R no menu suspenso de kernels. Na célula, digite ou cole o código. Selecione **Executar** para ver a saída a seguir.

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel do Python local

Escolha o Kernel do Python local e, na célula, digite -

![Python local](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Gerenciar pacotes

Um dos aspectos que otimizamos para o desenvolvimento de Python local foi a inclusão da capacidade de instalar pacotes de que os clientes precisariam para seus cenários. Por padrão, incluímos os pacotes comuns, como `pandas`, `numpy` etc.,. No entanto, se você está esperando um pacote que não está incluído, escreva o seguinte código na célula do notebook:

```python
import <package-name>
```

Quando você executa esse comando, `Module not found` é retornado. Se o pacote existir, não haverá nenhum erro.

Se ele retornar um erro `Module not Found`, selecione **Gerenciar Pacotes** para iniciar o terminal. Agora você pode instalar pacotes localmente. Use os comandos a seguir para instalar os pacotes:

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

- [Como gerenciar notebooks no Azure Data Studio](notebooks-manage-sql-server.md).
- [Criar e executar um notebook do SQL Server](notebooks-tutorial-sql-kernel.md).
- [Implantar um cluster de Big Data do SQL Server com o notebook do Azure Data Studio](../big-data-cluster/notebooks-deploy.md).
- [Gerenciar Clusters de Big Data do SQL Server com notebooks do Azure Data Studio](../big-data-cluster/notebooks-manage-bdc.md).
- [Executar um notebook de exemplo usando o Spark](../big-data-cluster/notebooks-tutorial-spark.md).
- [Execute scripts Python e R em notebooks no Azure Data Studio com os Serviços de Machine Learning do SQL Server](../machine-learning/install/sql-machine-learning-azure-data-studio.md).
