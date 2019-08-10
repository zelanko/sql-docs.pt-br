---
title: Como usar Notebooks SQL no Azure Data Studio
titleSuffix: Azure Data Studio
description: Saiba como usar Notebooks SQL no Azure Data Studio
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9af2e04a3973eddfcd714c7968c35e544302aba9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959260"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Como usar notebooks no Azure Data Studio

Este artigo descreve como iniciar a experiência de Notebook no Azure Data Studio e como começar a criar seus próprios notebooks. Ele também mostra como escrever Notebooks usando kernels diferentes.


## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Você pode se conectar ao tipo de conexão Microsoft SQL Server no Azure Data Studio.
No Azure Data Studio, você também pode pressionar F1 e clicar em **Nova Conexão** e conectar-se ao seu SQL Server.

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Iniciar Notebooks

Há várias maneiras de iniciar um novo notebook.

1. Vá para o **menu Arquivo** no Azure Data Studio e clique em **Novo Notebook**.

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. Clique com o botão direito do mouse na conexão **SQL Server** e inicie o **Novo Notebook**. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. Abra a paleta de comandos (**Ctrl+Shift+P**) e digite **Novo Notebook**. Um novo arquivo chamado `Notebook-1.ipynb` é aberto.

## <a name="supported-kernels-and-attach-to-context"></a>Kernels com suporte e anexar ao contexto

A instalação do Notebook no Azure Data Studio dá suporte nativo ao Kernel do SQL. Se você for um desenvolvedor de SQL e quiser usar Notebooks, esse será o Kernel escolhido. 

O Kernel do SQL também pode ser usado para se conectar a instâncias do servidor PostgreSQL. Se você for um desenvolvedor de PostgreSQL e quiser se conectar ao seu Servidor PostgreSQL, baixe a [**Extensão do PostgreSQL**](postgres-extension.md) no marketplace de extensão do Azure Data Studio.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel do SQL

Nas células de código dentro do Notebook, semelhante ao nosso editor de consultas, damos suporte à experiência moderna de codificação do SQL que facilita as tarefas diárias com recursos internos, como um editor SQL avançado, o IntelliSense e snippets de código internos. Os snippets de código permitem que você gere a sintaxe SQL adequada para criar bancos de dados, tabelas, exibições, procedimentos armazenados, entre outros, e para atualizar objetos de banco de dados existentes. Use snippets de código para criar rapidamente cópias de seu banco de dados para fins de desenvolvimento ou teste e para gerar e executar scripts.

Clique em **Executar** para executar cada célula.

Kernel do SQL para se conectar à instância do SQL Server

![image7](media/sql-notebooks/intellisense-code-cell.png)

Resultados da consulta

![image19](media/sql-notebooks/sql-cell-results.png)

Kernel do SQL para se conectar à instância do Servidor PostgreSQL 

![image18](media/sql-notebooks/pgsql-code-cell.png)

Resultados da consulta

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurar o Python para Notebooks

Ao selecionar qualquer um dos outros kernels além do SQL na lista suspensa de kernels, você precisa **Configurar o Python para Notebooks**. As dependências do Notebook são instaladas em uma localização especificada, mas você pode decidir se deseja definir a localização de instalação. Essa instalação pode levar algum tempo e é recomendável não fechar o aplicativo até que ela seja concluída. Quando a instalação for concluída, você poderá começar a escrever o código na linguagem com suporte.

![image21](media/sql-notebooks/configure-python.png)

Depois que a instalação for realizada com sucesso, você encontrará uma notificação no Histórico de Tarefas junto com a localização do servidor de back-end do Jupyter em execução no Terminal de Saída.

![image22](media/sql-notebooks/jupyter-backend.png)

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

![image8](media/sql-notebooks/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você verá a visualização ao mesmo tempo

![image9](media/sql-notebooks/notebook-markdown-cell.png)

Clicar fora da célula de texto mostrará o texto de markdown.

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Confiável e não confiável

Os Notebooks abertos no Azure Data Studio são **Confiáveis** por padrão.

Se você abrir um Notebook de alguma outra fonte, ele será aberto no modo **Não Confiável** e você poderá configurá-lo como **Confiável**.

### <a name="save"></a>Salvar 

Você pode salvar o Notebook pressionando **CTRL + S** ou clicando nos comandos **Salvar Arquivo**, **Salvar Arquivo Como...** e **Salvar Todos os Arquivos** no menu Arquivo ou, ainda, nos comandos **Arquivo: Salvar** inseridos na paleta de comandos.

### <a name="pyspark3pyspark-kernel"></a>Kernel do Pyspark3/PySpark

Escolha o `PySpark Kernel` e, na célula, digite o código a seguir.

Clique em **Executar**.

O Aplicativo Spark é iniciado e retorna a seguinte saída:

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel do Spark | Linguagem Scala

Escolha o `Spark|Scala Kernel` e, na célula, digite o código a seguir.

![image13](media/sql-notebooks/spark-scala.png)

Você também pode exibir as "Opções de Célula" clicando no ícone de opções abaixo –

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel do Spark | Linguagem R

Escolha Spark | R no menu suspenso de kernels. Na célula, digite ou cole o código. Clique em **Executar** para ver a seguinte saída.

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Kernel do Python local

Escolha o Kernel do Python local e, na célula, digite -

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Gerenciar pacotes
Um dos aspectos que otimizamos para o desenvolvimento de Python local foi a inclusão da capacidade de instalar pacotes de que os clientes precisariam para seus cenários. Por padrão, incluímos os pacotes comuns, como `pandas`, `numpy` etc., mas se você estiver esperando um pacote que não está incluído, escreva o seguinte código na célula do notebook: 

```python
import <package-name>
```

Quando você executa esse comando, `Module not found` é retornado. Se o pacote existir, você não receberá o erro.

Se ele retornar um erro `Module not Found`, clique em **Gerenciar Pacotes** para iniciar a experiência do assistente. 

![image17](media/sql-notebooks/manage-packages.png)

Neste assistente, você poderá ver os pacotes **Instalados**. Você pode pesquisar na lista e na versão associada de cada um desses pacotes. Se precisar **desinstalar** algum dos pacotes, você poderá clicar em um dos pacotes e, em seguida, clicar na opção **Desinstalar pacotes selecionados**.

Você também poderá clicar em **Adicionar novos pacotes** para **Pesquisar** um pacote específico, escolher a versão relacionada e clicar em **instalar**. Por padrão, selecionamos a versão mais recente do pacote pesquisado. 

Depois que o pacote for instalado, você poderá ir para a célula do Notebook e digitar o seguinte comando:

```python
import <package-name>
```

Se precisar **desinstalar** algum dos pacotes, você poderá clicar em um ou em vários pacotes e, em seguida, clicar na opção **Desinstalar pacotes selecionados**.

## <a name="next-steps"></a>Próximas etapas

Para saber como trabalhar com um notebook existente, confira [Como gerenciar notebooks no Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).