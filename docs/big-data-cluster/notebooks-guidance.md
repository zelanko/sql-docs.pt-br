---
title: Execute blocos de anotações no estúdio de dados do Azure
titleSuffix: SQL Server big data clusters
description: Este artigo explica como executar o Jupyter Notebooks no estúdio de dados do Azure conectado a um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a220b78fe93b286837e0e235b881ffd1a612e512
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58859967"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Como usar blocos de anotações na visualização do SQL Server de 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como iniciar a experiência de bloco de anotações no estúdio de dados do Azure e como começar a criar seus próprios blocos de anotações. Ele também mostra como gravar blocos de anotações usar kernels diferentes.

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Você pode conectar-se para o tipo de conexão do Microsoft SQL Server no estúdio de dados do Azure.
No estúdio de dados do Azure, você pode também pressionar F1 e clique em **nova Conexão** e conecte-se ao SQL Server.

![Informações de Conexão](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Inicie os blocos de anotações

Há várias maneiras de iniciar um novo bloco de anotações.

- Vá para o **Menu arquivo** no Studio de dados do Azure e, em seguida, clique em **novo Notebook**.

    ![Novo bloco de anotações](media/notebooks-guidance/file-new-notebook.png)

- Clique com botão direito do **do SQL Server** conexão e, em seguida, inicie **novo Notebook**.

    ![Novo bloco de anotações](media/notebooks-guidance/server-new-notebook.png)

- Abra a paleta de comandos (**Ctrl + Shift + P**)) e, em seguida, digite **novo Notebook**. Um novo arquivo chamado `Notebook-1.ipynb` é aberta.

## <a name="supported-kernels-and-attach-to-context"></a>Suporte para kernels e anexe ao contexto

A instalação do bloco de anotações no estúdio de dados do Azure dá suporte nativamente a Kernel de SQL. Se você for um desenvolvedor SQL e gostaria de usar blocos de anotações, então isso seria escolhido Kernel. 

O Kernel de SQL também pode ser usado para se conectar a instâncias de servidor PostgreSQL. Se você for um desenvolvedor PostgreSQL e gostaria de se conectar ao servidor PostgreSQL, em seguida, baixe o [ **PostgreSQL extensão** ](../azure-data-studio/postgres-extension.md) no marketplace de extensão do estúdio de dados do Azure.

![Conexão do PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL Kernel

As células de código dentro do bloco de anotações, semelhante ao nosso editor de consultas, damos suporte a SQL moderna experiência que facilita as tarefas diárias com recursos internos, como um editor SQL Avançado, IntelliSense e trechos de código internos de codificação. Trechos de código que você possa gerar a sintaxe apropriada do SQL para criar bancos de dados, tabelas, exibições, procedimentos armazenados, etc. e para atualizar os objetos de banco de dados existente. Use trechos de código para rapidamente criar cópias de seu banco de dados para fins de teste ou desenvolvimento e para gerar e executar scripts.

Clique em **executar** para executar cada célula.

Kernel de SQL para se conectar à instância do SQL Server

![SQL Kernel](media/notebooks-guidance/intellisense-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/sql-cell-results.png)

Kernel de SQL para se conectar à instância do servidor PostgreSQL 

![Conexão do PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Resultados da consulta

![Resultados da consulta](media/notebooks-guidance/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurar o Python para blocos de anotações

Quando você seleciona qualquer um dos outros kernels além do SQL no menu suspenso do kernel, isso solicita que você **configurar o Python para Notebooks**. As dependências de bloco de anotações são instaladas em um local especificado, mas você pode decidir se é necessário definir o local de instalação. Essa instalação pode levar algum tempo e é recomendável não fechar o aplicativo até que a instalação for concluída. Depois que a instalação for concluída, você pode começar a escrever código no idioma com suporte.

![Configurar o python](media/notebooks-guidance/configure-python.png)

Depois que a instalação for bem-sucedida, você encontrará uma notificação no histórico de tarefa, juntamente com o local do servidor de back-end de Jupyter em execução no Terminal de saída.

![Back-end do Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descrição
|:-----|:-----
| SQL Kernel | Escreva o código de SQL direcionado a seu banco de dados relacional.
|PySpark3 e o Kernel PySpark| Escreva o código do Python usando computação Spark do cluster.
|Spark Kernel|Escreva código Scala e o R usando computação Spark do cluster.
|Python Kernel|Escreva o código do Python para o desenvolvimento local.

`Attach to` fornece o contexto para o Kernel anexar. Se você estiver usando o Kernel de SQL, você pode `Attach to` qualquer uma de suas instâncias do SQL Server.

Se você estiver usando o Kernel Python3 a `Attach to` é `localhost`. Você pode usar este kernel para o desenvolvimento de Python local.

Quando você está conectado ao cluster de big data de 2019 do SQL Server, o padrão `Attach to` é esse ponto de extremidade do cluster e permitirá que você enviar o código do Python, Scala e R usando a computação do Spark do cluster.

### <a name="code-cells-and-markdown-cells"></a>Células de código e células de Markdown

Adicionar uma nova célula de código clicando o **+ código** comando na barra de ferramentas.

Adicionar uma nova célula de texto clicando o **+ texto** comando na barra de ferramentas.

![Barra de ferramentas do bloco de anotações](media/notebooks-guidance/notebook-toolbar.png)

O célula é alterado para modo de edição e digite agora markdown e você verá a visualização ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Ao clicar fora da célula de texto, você verá o texto do markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Não confiáveis e não confiáveis

Blocos de anotações aberto no Studio de dados do Azure são o padrão **confiáveis**.

Se você abrir um bloco de anotações de alguma outra origem, ele será aberto no **não confiáveis** modo e, em seguida, você pode torná-lo **confiáveis**.

### <a name="save"></a>Salvar

Você pode salvar o bloco de anotações pela **Ctrl + S** ou clicando o **salvar arquivo**, **salvar arquivo como...**  e **arquivo Salvar tudo** comandos no menu Arquivo e **arquivo: Salvar** comandos inseridos na paleta de comandos.

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Escolha o `PySpark Kernel` e no tipo de célula no código a seguir.

Clique em **Executar**.

O aplicativo Spark é iniciado e retorna a seguinte saída:

![Aplicativo Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguagem scala

Escolha o `Spark|Scala Kernel` e no tipo de célula no código a seguir.

![Spark Scala](media/notebooks-guidance/spark-scala.png)

Você também pode exibir as opções"célula" quando você clica no ícone de opções abaixo –

![Opções de célula](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguagem R

Escolha o Spark | R na lista suspensa para os kernels. Na célula, digite ou cole o código. Clique em **executar** para ver a saída a seguir.

![Spark, R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel Python local

Escolha o Kernel Python local e no tipo de célula no -

![Python local](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Gerenciar pacotes

Uma das coisas que podemos otimizados para desenvolvimento de Python local era incluem a capacidade de instalar os pacotes que os clientes precisam para seus cenários. Por padrão, podemos incluir os pacotes comuns, como `pandas`, `numpy` etc., mas se você estiver esperando um pacote que não é incluído, em seguida, escrever o código a seguir na célula de notebook: 

```python
import <package-name>
```

Quando você executa esse comando, `Module not found` será retornado. Se o pacote existir, em seguida, você não obterá o erro.

Se ele retornar um `Module not Found` erro e, em seguida, clique em **gerenciar pacotes** para iniciar o terminal. Agora você pode instalar os pacotes localmente. Use os seguintes comandos para instalar os pacotes:

```bash
./pip install <package-name>
```

   > [!Tip]
   > No Mac, siga as instruções na janela do Terminal para instalar pacotes. 

Depois de instalar o pacote, você deve ser capaz de entrar na célula do bloco de anotações e digite o seguinte comando:

```python
import <package-name>
```

Para desinstalar um pacote, use o seguinte comando no seu terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Próximas etapas

Para saber como trabalhar com um bloco de anotações existente, consulte [como gerenciar notebooks no estúdio de dados do Azure](notebooks-how-to-manage.md).