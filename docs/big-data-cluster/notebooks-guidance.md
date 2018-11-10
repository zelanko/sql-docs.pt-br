---
title: Como usar blocos de anotações na visualização do SQL Server 2019 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 9f9db16431cd6c3befbb32383725ec008f5a9081
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221632"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Como usar blocos de anotações na visualização do SQL Server de 2019

Este artigo descreve como iniciar os blocos de anotações do Jupyter no cluster e começar a criar seus próprios blocos de anotações. Ele também mostra como enviar trabalhos no cluster.

## <a name="prerequisites"></a>Prerequisites

Para usar os blocos de anotações, você deve instalar os seguintes pré-requisitos:

- [Um cluster de big data do SQL Server de 2019](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [A extensão de 2019 do SQL Server (versão prévia)](../azure-data-studio/sql-server-2019-extension.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>Conectar-se ao ponto de extremidade Hadoop Gateway Knox

Você pode se conectar aos pontos de extremidade diferentes no cluster. Você pode conectar-se para o tipo de conexão do Microsoft SQL Server ou para o ponto de extremidade de Gateway HDFS/Spark.
No estúdio de dados do Azure (visualização), pressione F1 e clique em **nova Conexão** e você pode se conectar ao ponto de extremidade do Gateway HDFS/Spark.

![Image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Procurar HDFS

Depois que você se conectar, você poderá procurar a pasta do HDFS. WebHDFS é iniciado quando a implantação for concluída, e você conseguirá **Refresh**, adicionar **novo diretório**, **carregar** arquivos, e **excluir**.

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

  Forneça um nome do bloco de anotações, por exemplo, `Test.ipynb`. Clique em **Salvar**.

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>Suporte para kernels e anexe ao contexto

Oferece suporte a instalação de Notebook PySpark e Spark, os kernels de mágica do Spark, que permitem que você escreva código Python e Scala usando o Spark. Opcionalmente, você pode escolher o Python para fins de desenvolvimento local.

![image7](media/notebooks-guidance/image7.png)

Quando você seleciona um desses kernels, vamos instalar esse kernel no ambiente virtual e você pode começar a escrever código no idioma com suporte.

|Kernel|Description
|:-----|:-----
|Kernel PySpark|Para escrever o código do Python usando computação Spark do cluster.
|Kernel Spark|Para escrever código Scala usando computação Spark do cluster.
|Kernel Python|Para escrever o código do Python para o desenvolvimento local.

O `Attach to` fornece o contexto para o Kernel anexar. Quando você está conectado ao final HDFS/Spark Gateway (Knox), aponte o padrão `Attach to` é esse ponto de extremidade do cluster.

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>Olá, mundo em contextos diferentes

### <a name="pyspark-kernel"></a>Kernel Pyspark

Escolha o PySpark Kernel e no tipo de célula no código a seguir:

![image9](media/notebooks-guidance/image9.png)

Clique em executar e você deve ver o aplicativo Spark que está sendo iniciado e você verá a seguinte saída:

![Image10](media/notebooks-guidance/image10.png)

A saída deve ser algo semelhante à imagem a seguir.

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Kernel Spark
Adicionar uma nova célula de código clicando o **+ código** comando na barra de ferramentas.

![Image12](media/notebooks-guidance/image12.png)

Você também pode exibir as opções"célula" quando você clica no ícone de opções abaixo –

![Image13](media/notebooks-guidance/image13.png)

Aqui estão as opções para cada célula –

![Image14](media/notebooks-guidance/image14.png)-

Agora, escolha o Kernel do Spark na lista suspensa para os kernels e no tipo/colar de célula no –

![Image15](media/notebooks-guidance/image15.png)

Clique em **executados** e você deverá ver o aplicativo Spark que está sendo iniciado, e isso criará a sessão do Spark como **spark** e definirá o **HelloWorld** objeto.

O Notebook deve ser semelhante à imagem a seguir.

![image16](media/notebooks-guidance/image16.png)

Depois de definir o objeto, em seguida, na próxima célula do bloco de anotações, digite o código a seguir:

![image17](media/notebooks-guidance/image17.png)

Clique em **executar** no Notebook de menu e você deverá ver o "Hello, world!" na saída.

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>Kernel python local
Escolha o Kernel Python local e no tipo de célula no -

![Image19](media/notebooks-guidance/image19.png)

Você verá a seguinte saída:

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Texto de markdown
Adicionar uma nova célula de texto clicando o **+ texto** comando na barra de ferramentas.

![Image21](media/notebooks-guidance/image21.png)

Clique no ícone de visualização para adicionar o markdown

![Image22](media/notebooks-guidance/image22.png)

Clique no ícone de visualização novamente para alternar para ver apenas o markdown

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>Gerenciar pacotes
Uma das coisas que podemos otimizados para desenvolvimento de Python local era incluem a capacidade de instalar os pacotes que os clientes precisam para seus cenários. Por padrão, os pacotes comuns são incluídos como pandas, numpy etc., mas se você estiver esperando um pacote que não é incluído, em seguida, escrever o código a seguir na célula de Notebook: 

```python
import <package-name>
```

Quando você executar esse comando, você obterá um `Module not found` erro. Se o pacote existir, em seguida, você não obterá o erro.

Se você encontrar um `Module not Found` erro e, em seguida, clique em **gerenciar pacotes** para iniciar o terminal com o caminho para o seu Virtualenv identificado. Agora você pode instalar os pacotes localmente. Use os seguintes comandos para instalar os pacotes:

```bash
./pip install <package-name>
```

Depois de instalar o pacote, você deve ser capaz de entrar na célula do bloco de anotações e digite o seguinte comando:

```python
import <package-name>
```

Agora, quando você executar a célula, você não obterá o `Module not found` erro.

Para desinstalar um pacote, use o seguinte comando no seu terminal:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Próximas etapas

Para saber como trabalhar com um bloco de anotações existente, consulte [como gerenciar notebooks no estúdio de dados do Azure](notebooks-how-to-manage.md).