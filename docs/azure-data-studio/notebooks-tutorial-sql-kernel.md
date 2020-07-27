---
title: Notebooks com o kernel do SQL no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do SQL Server.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: 66d8c464a0f03eb227e9fda50f6b5ad249f828da
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920422"
---
# <a name="create-and-run-a-sql-server-notebook"></a>Criar e executar um notebook do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este tutorial demonstra como criar e executar um notebook no Azure Data Studio usando um SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio instalado](download-azure-data-studio.md)
- SQL Server instalado
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="create-a--notebook"></a>Criar um notebook

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. No Azure Data Studio, conecte-se ao SQL Server.

1. Selecione-o na **Conexões** na janela **Servidores**. Em seguida, escolha **Novo Notebook**.

   ![Abrir notebook](media/notebook-tutorial/azure-data-studio-open-notebook.png)

1. Aguarde até que o **Kernel** e o contexto de destino (**Anexar a**) sejam preenchidos. Confirme se o **Kernel** está definido como **SQL** e defina **Anexar a** para o SQL Server (neste exemplo, o *localhost*).

   ![Definir o kernel e Anexar a](media/notebook-tutorial/set-kernel-and-attach-to.png)

Você pode salvar o notebook usando o comando **Salvar** ou **Salvar como...** no menu **Arquivo**. 

Para abrir um notebook, você pode usar o comando **Abrir arquivo...** no menu **Arquivo**, selecionar **Abrir arquivo** na página **Inicial** ou usar o comando **Arquivo: abrir** da paleta de comandos.

## <a name="change-the-sql-connection"></a>Alterar a conexão SQL

Para alterar a conexão SQL de um notebook:

1. Selecione o menu **Anexar a** na barra de ferramentas do notebook e, em seguida, **Alterar Conexão**.

   ![Clique no menu Anexar a na barra de ferramentas do notebook](./media/notebook-tutorial/select-attach-to-1.png)

2. Agora você pode selecionar um servidor de conexão recente ou inserir novos detalhes de conexão para se conectar.

   ![Selecione um servidor no menu Anexar a](./media/notebook-tutorial/select-attach-to-2.png)

## <a name="run-a-code-cell"></a>Executar uma célula de código

Você pode criar células contendo código SQL que pode ser executado no local clicando no botão **Executar célula** (a seta preta redonda) à esquerda da célula. Os resultados são mostrados no notebook após a conclusão da execução da célula.

Por exemplo:

1. Adicione uma nova célula de código selecionando o comando **+Code** na barra de ferramentas.

   ![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

1. Copie e cole o exemplo a seguir na célula e clique em **Executar célula**. Esse exemplo cria um banco de dados.

   ```sql
   USE master
   GO
   
   -- Drop the database if it already exists
   IF  EXISTS (
           SELECT name
           FROM sys.databases
           WHERE name = N'TestNotebookDB'
      )
   DROP DATABASE TestNotebookDB
   GO
   
   -- Create the database
   CREATE DATABASE TestNotebookDB
   GO
   ```

   ![Executar célula do notebook](media/notebook-tutorial/run-notebook-cell.png)

## <a name="save-the-result"></a>Salvar o resultado

Se você executar um script que retorna um resultado, poderá salvar esse resultado em formatos diferentes usando a barra de ferramentas exibida acima do resultado.

- Salvar como CSV
- Salvar como Excel
- Salvar como JSON
- Salvar como XML

Por exemplo, o código a seguir retorna o resultado de [PI](../t-sql/functions/pi-transact-sql.md).

```sql
SELECT PI() AS PI;
GO
```

![Executar célula do notebook](media/notebook-tutorial/run-notebook-cell-2.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Como usar notebooks no Azure Data Studio](notebooks-guidance.md)
- [Criar e executar um notebook do Python](notebooks-tutorial-python-kernel.md)
- [Executar um notebook de exemplo usando o Spark](../big-data-cluster/notebooks-tutorial-spark.md)