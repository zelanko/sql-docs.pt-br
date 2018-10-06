---
title: Como usar blocos de anotações na visualização do SQL Server 2019 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 989ee419406d0f69cd7bda26485d3d44cbf56550
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827327"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Como usar blocos de anotações na visualização do SQL Server de 2019

Este artigo mostra como iniciar os blocos de anotações em um cluster de big data do SQL Server de 2019. Ele também mostra como começar a criar seus próprios blocos de anotações e como enviar trabalhos no cluster.

## <a name="prerequisites"></a>Prerequisites

Para usar os blocos de anotações, você deve instalar os seguintes pré-requisitos:

- [Um cluster de big data do SQL Server de 2019](deployment-guidance.md)
- [Studio de dados do Azure](../azure-data-studio/what-is.md)
- [A extensão de 2019 do SQL Server (versão prévia)](../azure-data-studio/sql-server-2019-extension.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>Conectar-se para o ponto de extremidade do cluster de big data do SQL Server

Você pode se conectar a diferentes pontos de extremidade do cluster. Você pode conectar-se para o tipo de conexão do Microsoft SQL Server ou para o ponto de extremidade do cluster de big data do SQL Server.

No estúdio de dados do Azure (visualização), digite **F1** > **nova Conexão**e se conectar ao seu ponto de extremidade do cluster de big data do SQL Server.

![Image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Procurar HDFS
Depois que você se conectar, você poderá procurar a pasta do HDFS. WebHDFS é iniciado quando a implantação for concluída, e você conseguirá **Refresh**, adicionar **novo diretório**, **carregar** arquivos, e **excluir**.

![image2](media/notebooks-guidance/image2.png)

Essas operações simples permitem que você traga seus próprios dados no HDFS.

## <a name="launch-new-notebooks"></a>Inicie novos blocos de anotações

Há várias maneiras de iniciar um novo bloco de anotações.

1. Do painel de gerenciar. Sobre como fazer uma nova conexão, você verá um painel. Clique na tarefa do novo bloco de anotações do painel.

  ![image3](media/notebooks-guidance/image3.png)

1. Clique com o botão direito na conexão de HDFS/Spark e você tem um novo bloco de anotações no menu de contexto

![image4](media/notebooks-guidance/image4.png)

Forneça um nome do bloco de anotações (exemplo: *Test.ipynb*) e clique em **salvar**.

![image5](media/notebooks-guidance/image5.png)

## <a name="supported-kernels-and-attach-to-context"></a>Suporte para kernels e anexe ao contexto

Em nossa instalação do bloco de anotações, damos suporte PySpark e Spark, os kernels Spark Magic que permitem que os usuários escrevam código Python e Scala usando o Spark. Também permitimos que os usuários escolham o Python para suas finalidades de desenvolvimento local.

![image6](media/notebooks-guidance/image6.png)

Quando você seleciona um desses kernels, vamos instalar esse kernel no ambiente virtual e você pode começar a escrever código no idioma com suporte.

| Kernel | Description
|---- |----
|Kernel PySpark| Para escrever o código do Python usando o Spark, computação de cluster.
|Kernel Spark|Para escrever código Scala usando o Spark, computação de cluster.
|Kernel Python|Para escrever o código do Python para o desenvolvimento local.

A seleção para anexar fornece o contexto para o Kernel anexar. Quando você está conectado ao ponto de extremidade do cluster grande de dados de SQL Server, a seleção padrão para anexar será esse ponto de extremidade do cluster.

![image7](media/notebooks-guidance/image7.png)

## <a name="hello-world-in-the-different-contexts"></a>Olá, mundo em diferentes contextos

### <a name="pyspark-kernel"></a>Kernel Pyspark

Escolha o PySpark Kernel e no tipo de célula no código a seguir:

![image8](media/notebooks-guidance/image8.png)

Clique em executar e você deve ver o aplicativo Spark que está sendo iniciado e você verá a seguinte saída:

![image9](media/notebooks-guidance/image9.png)

A saída deve ser algo semelhante à imagem a seguir.

![Image10](media/notebooks-guidance/image10.png)

### <a name="spark-kernel"></a>Kernel Spark
Adicionar uma nova célula de código clicando o + comando na barra de ferramentas de código.

![Image11](media/notebooks-guidance/image11.png)

Escolha o Kernel do Spark na lista suspensa para os kernels e em que o tipo de célula/colar em 

![Image12](media/notebooks-guidance/image12.png)

Clique em **executados** você deve ver o aplicativo Spark que está sendo iniciada e isso criará a sessão do Spark **spark** e definirá o **HelloWorld** objeto.

O Notebook deve ser semelhante à imagem a seguir.

![Image13](media/notebooks-guidance/image13.png)

Uma vez você definir o objeto, em seguida, em que o próximo tipo de célula do bloco de anotações no código a seguir:

![Image14](media/notebooks-guidance/image14.png)

Clique em **executar** no Notebook de menu e você deverá ver o "Hello, world!" na saída.

![Image15](media/notebooks-guidance/image15.png)

### <a name="local-python-kernel"></a>Kernel python local
Escolha o Kernel Python local e no tipo de célula no * *

![image16](media/notebooks-guidance/image16.png)

Você verá a seguinte saída:

![image17](media/notebooks-guidance/image17.png)

### <a name="markdown-text"></a>Texto de markdown
Adicionar uma nova célula de texto clicando o + comando de texto na barra de ferramentas.

![Image18](media/notebooks-guidance/image18.png)

Clique no ícone de visualização para adicionar o markdown

![Image19](media/notebooks-guidance/image19.png)

Clique no ícone de visualização novamente para alternar para ver apenas o markdown

![Image20](media/notebooks-guidance/image20.png)

## <a name="manage-packages"></a>Gerenciar pacotes
Uma das coisas que podemos otimizados para desenvolvimento de Python local era incluem a capacidade de instalar os pacotes que os clientes precisam para seus cenários. Por padrão, os pacotes comuns são incluídos como pandas, numpy etc., mas se você estiver esperando um pacote que não é incluído, em seguida, escrever o código a seguir na célula de Notebook

```python
import <package-name>
```

Quando você executar esse comando, você obterá um `Module not found` erro. Se o pacote existir, em seguida, você não obterá o erro.

Se você encontrar um `Module not Found` erro e, em seguida, clique em de **gerenciar pacotes** para iniciar o terminal com o caminho para o seu Virtualenv identificado. Agora você pode instalar os pacotes localmente. Use o seguinte comando para instalar os pacotes:

```
./pip install <package-name>
```

Depois de instalar o pacote, você deve ser capaz de entrar na célula do bloco de anotações e digite o seguinte comando:

```python
import <package-name>
```

Agora, quando você executar a célula, você não obterá o `Module not found` erro.

Se você quiser desinstalar um pacote, use o seguinte comando no seu terminal:

```
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Próximas etapas

Para saber como trabalhar com um bloco de anotações existente, consulte [como gerenciar notebooks no estúdio de dados do Azure](notebooks-how-to-manage.md).