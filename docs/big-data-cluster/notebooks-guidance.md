---
title: Execute blocos de anotações no estúdio de dados do Azure
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo explica como executar blocos de anotações do Jupyter no Azure Data Studio conneected para um cluster de big data do SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ba203fcd7445add8fce00dd64913f85bcf4cc1
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161653"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Como usar blocos de anotações na visualização do SQL Server de 2019

Este artigo descreve como iniciar o Jupyter Notebooks em um cluster de big data e como começar a criar seus próprios blocos de anotações. Ele também mostra como enviar trabalhos no cluster.

## <a name="prerequisites"></a>Prerequisites

Para usar os blocos de anotações, você deve instalar os seguintes pré-requisitos:

- [Um cluster de big data do SQL Server de 2019](deployment-guidance.md)
- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>Conectar-se para o ponto de extremidade do cluster de big data do SQL Server

Você pode se conectar aos pontos de extremidade diferentes no cluster. Você pode conectar-se para o tipo de conexão do Microsoft SQL Server ou para o ponto de extremidade do cluster de big data do SQL Server.
No estúdio de dados do Azure, pressione F1 e clique em **nova Conexão** e você pode se conectar ao ponto de extremidade do cluster de big data do SQL Server.

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Procurar HDFS

Depois que você se conectar, você poderá procurar a pasta do HDFS. Partir do SQL Server que webhdfs é iniciado quando a implantação for concluída. Com o WebHDFS, você pode **Refresh**, adicione **novo diretório**, **carregar** arquivos, e **excluir**.

![image2](media/notebooks-guidance/image2.png)

Essas operações simples permitem que você traga seus próprios dados no HDFS.

## <a name="launch-new-notebooks"></a>Inicie novos blocos de anotações

>[!NOTE]
>Se você tiver vários processos de Python em execução no seu ambiente, primeiro exclua o `.scaleoutdata` pasta em seu diretório instalado. Isso deve disparar o `Reinstall Notebook dependencies` tarefa no Studio de dados do Azure. Levará alguns minutos para que todas as dependências a serem instalados.

Se houver problemas ao instalar as dependências do bloco de anotações, clique em Ctrl + Shift + P ou para Macintosh Cmd + Shift + P, tipo e `Reinstall Notebook dependencies` na paleta de comandos.

![image3](media/notebooks-guidance/image3.png)

Há várias maneiras de iniciar um novo bloco de anotações.

1. Dos **gerenciar painel**. Depois de fazer uma nova conexão, você verá um painel. Clique em **novo Notebook** tarefas do painel.
  
    ![image4](media/notebooks-guidance/image4.png)

1. A conexão de HDFS/Spark com o botão direito e clique em **novo Notebook** no menu de contexto.

    ![image5](media/notebooks-guidance/image5.png)

    Um novo arquivo chamado `Notebook-0.ipynb` é aberta.

    ![image6](media/notebooks-guidance/image6.png)

Quando você abre o bloco de anotações da paleta de comando, o bloco de anotações é aberto como `Untitled-0.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Suporte para kernels e anexe ao contexto

Oferece suporte a instalação de Notebook PySpark e Spark, os kernels de mágica do Spark, que permitem que você escreva código Python e Scala usando o Spark. Opcionalmente, você pode escolher o Python para fins de desenvolvimento local.

![image7](media/notebooks-guidance/image7.png)

Quando você seleciona um desses kernels, a instalação configura esse kernel no ambiente virtual e você pode começar a escrever código no idioma com suporte.

|Kernel|Descrição
|:-----|:-----
|PySpark3 e o Kernel PySpark| Escreva o código do Python usando computação Spark do cluster.
|Spark Kernel|Escreva código Scala e o R usando computação Spark do cluster.
|Python Kernel|Escreva o código do Python para o desenvolvimento local.

`Attach to` fornece o contexto para o Kernel anexar. Quando você está conectado para o ponto de extremidade de cluster de big data do SQL Server, o padrão `Attach to` é esse ponto de extremidade do cluster.

Quando você não está conectado ao ponto de extremidade do cluster do SQL Server big data, o Kernel padrão é Python e `Attach to` é `localhost`.

## <a name="hello-world-in-different-contexts"></a>Olá, mundo em contextos diferentes

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Escolha o PySpark Kernel e no tipo de célula no código a seguir.

Clique em **Executar**.

O aplicativo Spark é iniciado e retorna a seguinte saída:

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguagem scala

Escolha o Spark | Scala Kernel e no tipo de célula no código a seguir.

![image9](media/notebooks-guidance/image9.png)

Adicionar uma nova célula de código clicando o **+ código** comando na barra de ferramentas.

Agora, escolha o Spark | Na lista suspensa para os kernels e no tipo/colar de célula no – de scala

![image10](media/notebooks-guidance/image10.png)

Você também pode exibir as opções"célula" quando você clica no ícone de opções abaixo –

![image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguagem R

Escolha o Spark | R na lista suspensa para os kernels. Na célula, digite ou cole o código. Clique em **executar** para ver a saída a seguir.

![image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>Kernel Python local

Escolha o Kernel Python local e no tipo de célula no -

![image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Texto de markdown

Adicionar uma nova célula de texto clicando o **+ texto** comando na barra de ferramentas.

![image15](media/notebooks-guidance/image15.png)

Clique duas vezes dentro da célula de texto para alterar para editar o modo de exibição 

![image16](media/notebooks-guidance/image16.png)

O célula é alterado para modo de edição

![image17](media/notebooks-guidance/image17.png)

Agora o markdown de tipo e você verá a visualização ao mesmo tempo

![image18](media/notebooks-guidance/image18.png)

Clique em **Executar**. O aplicativo Spark for iniciado cria a sessão do Spark como **spark** e define o **HelloWorld** objeto.

O Notebook deve ser semelhante à imagem a seguir.

Clicar fora da célula de texto será alterado para o modo de visualização e oculta markdown.

![image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>Gerenciar pacotes
Uma das coisas que podemos otimizados para desenvolvimento de Python local era incluem a capacidade de instalar os pacotes que os clientes precisam para seus cenários. Por padrão, podemos incluir os pacotes comuns, como `pandas`, `numpy` etc., mas se você estiver esperando um pacote que não é incluído, em seguida, escrever o código a seguir na célula de notebook: 

```python
import <package-name>
```

Quando você executa esse comando, `Module not found` será retornado. Se o pacote existir, em seguida, você não obterá o erro.

Se ele retornar um `Module not Found` erro e, em seguida, clique em **gerenciar pacotes** para iniciar o terminal com o caminho para o seu Virtualenv identificado. Agora você pode instalar os pacotes localmente. Use os seguintes comandos para instalar os pacotes:

```bash
./pip install <package-name>
```

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