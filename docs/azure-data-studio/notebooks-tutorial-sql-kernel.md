---
title: Notebooks com o kernel do SQL no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do SQL Server.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 70136c114fe1d4e9421400eff5f171a70289098c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178687"
---
# <a name="create-and-run-a-sql-server-notebook"></a>Criar e executar um notebook do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como criar e executar um notebook no Azure Data Studio usando um SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio instalado](download-azure-data-studio.md)
- SQL Server instalado
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="new-notebook"></a>Novo notebook

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. No Azure Data Studio, conecte-se ao SQL Server.

2. Selecione-o na **Conexões** na janela **Servidores**. Em seguida, escolha **Novo Notebook**.

   ![Abrir notebook](media/notebook-tutorial/azure-data-studio-open-notebook.png)

3. Aguarde até que o **Kernel** e o contexto de destino (**Anexar a**) sejam preenchidos. Confirme se o **Kernel** está definido como **SQL** e defina **Anexar a** para o SQL Server (nesse caso, o *localhost*).

   ![Definir o kernel e Anexar a](media/notebook-tutorial/set-kernel-and-attach-to.png)

## <a name="run-a-notebook-cell"></a>Executar uma célula do notebook

Você pode executar cada célula do notebook pressionando o botão Reproduzir à esquerda da célula. Os resultados são mostrados no notebook após a conclusão da execução da célula.

### <a name="code"></a>Código

Adicione uma nova célula de código selecionando o comando **+Code** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

Esse exemplo cria um banco de dados.

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

Se você executar um script que retorna um resultado, poderá salvar esse resultado em formatos diferentes.

- Salvar como CSV
- Salvar como Excel
- Salvar como JSON
- Salvar como XML

Nesse caso, retornamos o resultado do [PI](../t-sql/functions/pi-transact-sql.md).

```sql
SELECT PI() AS PI;
GO
```

![Executar célula do notebook](media/notebook-tutorial/run-notebook-cell-2.png)

### <a name="text"></a>Texto

Adicione uma nova célula de texto selecionando o comando **+Text** na barra de ferramentas.

![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

A célula muda para o modo de edição. Agora, digite markdown e você poderá ver a versão prévia ao mesmo tempo

![Célula de markdown](media/notebooks-guidance/notebook-markdown-cell.png)

A seleção fora da célula de texto mostra o texto markdown.

![Texto de markdown](media/notebooks-guidance/notebook-markdown-preview.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Como usar notebooks com o SQL Server](notebooks-guidance.md)

- [Como gerenciar notebooks no Azure Data Studio](notebooks-manage-sql-server.md)

- [Executar um notebook de exemplo usando o Spark](../big-data-cluster/notebooks-tutorial-spark.md)