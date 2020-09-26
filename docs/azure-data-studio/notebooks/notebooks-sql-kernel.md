---
title: Notebooks com o kernel do SQL no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do SQL Server.
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: cd71a160036bdcb5768e7a2ca51529989f733eeb
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364203"
---
# <a name="create-and-run-a-sql-server-notebook"></a>Criar e executar um notebook do SQL Server

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Este tutorial demonstra como criar e executar um notebook no Azure Data Studio usando um SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio instalado](../download-azure-data-studio.md)
- SQL Server instalado
  - [Windows](../../database-engine/install-windows/install-sql-server.md)
  - [Linux](../../linux/sql-server-linux-setup.md)

## <a name="create-a--notebook"></a>Criar um notebook

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. No Azure Data Studio, conecte-se ao SQL Server.

2. Selecione-o na **Conexões** na janela **Servidores**. Em seguida, escolha **Novo Notebook**.

3. Aguarde até que o **Kernel** e o contexto de destino (**Anexar a**) sejam preenchidos. Confirme se o **Kernel** está definido como **SQL** e defina **Anexar a** para o SQL Server (neste exemplo, o *localhost*).

   ![Definir o kernel e Anexar a](media/notebooks-sql-kernel/set-kernel-and-attach-to.png)

Você pode salvar o notebook usando o comando **Salvar** ou **Salvar como...** no menu **Arquivo**.

Para abrir um notebook, você pode usar o comando **Abrir arquivo...** no menu **Arquivo**, selecionar **Abrir arquivo** na página **Inicial** ou usar o comando **Arquivo: abrir** da paleta de comandos.

## <a name="change-the-sql-connection"></a>Alterar a conexão SQL

Para alterar a conexão SQL de um notebook:

1. Selecione o menu **Anexar a** na barra de ferramentas do notebook e, em seguida, **Alterar Conexão**.

   ![Selecionar o menu Anexar a na barra de ferramentas do notebook](./media/notebooks-sql-kernel/select-attach-to-1.png)

2. Agora você pode selecionar um servidor de conexão recente ou inserir novos detalhes de conexão para se conectar.

## <a name="run-a-code-cell"></a>Executar uma célula de código

Você pode criar células contendo código SQL que pode ser executado no local clicando no botão **Executar célula** (a seta preta redonda) à esquerda da célula. Os resultados são mostrados no notebook após a conclusão da execução da célula.

Por exemplo:

1. Adicione uma nova célula de código selecionando o comando **+Code** na barra de ferramentas.

   ![Barra de ferramentas do Notebook](media/notebooks-guidance/notebook-toolbar.png)

2. Copie e cole o exemplo a seguir na célula e clique em **Executar célula**. Esse exemplo cria um banco de dados.

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

   ![Executar célula](media/notebooks-sql-kernel/run-notebook-cell.png)

## <a name="save-the-result"></a>Salvar o resultado

Se você executar um script que retorna um resultado, poderá salvar esse resultado em formatos diferentes usando a barra de ferramentas exibida acima do resultado.

- Salvar como CSV
- Salvar como Excel
- Salvar como JSON
- Salvar como XML

Por exemplo, o código a seguir retorna o resultado de [PI](../../t-sql/functions/pi-transact-sql.md).

```sql
SELECT PI() AS PI;
GO
```

![Salvar o resultado](media/notebooks-sql-kernel/run-notebook-cell-2.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Como usar notebooks no Azure Data Studio](./notebooks-guidance.md)
- [Criar e executar um notebook do Python](././notebooks-python-kernel.md)
- [Executar um notebook de exemplo usando o Spark](../../big-data-cluster/notebooks-tutorial-spark.md)