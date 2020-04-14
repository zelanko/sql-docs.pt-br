---
title: Gerenciar um notebook do SQL Server
description: Aprenda a gerenciar notebooks no Azure Data Studio. Isso inclui abrir notebooks, salvá-los e alterar sua conexão de cluster de Big Data.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531589"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Como gerenciar notebooks no Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo mostra como abrir e salvar arquivos de notebook no Azure Data Studio com o SQL Server. Também demonstra como alterar sua conexão com o SQL Server.

## <a name="open-a-notebook"></a>Abrir um notebook

Há várias maneiras de abrir a caixa de diálogo **Abrir Notebook**. Você pode usar o menu Arquivo, o Painel e a Paleta de Comandos. As seções a seguir descrevem cada método.

### <a name="file-menu"></a>Menu Arquivo

Selecione **Abrir Arquivo** no menu Arquivo CTRL+O (no Windows) e Cmd+O (no Mac).

![Abra a caixa de diálogo Abrir Arquivo selecionando Abrir Arquivo](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>Painel

Clique em **Abrir Notebook** no painel para abrir a caixa de diálogo Abrir Arquivo.

![Abrir a caixa de diálogo Abrir Arquivo selecionando Abrir Notebook no painel](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>Paleta de Comandos

Use o comando **Arquivo: Abrir** da paleta de comandos digitando Ctrl+Shift+P (no Windows) e Cmd+Shift+P (no Mac).

![Abra a caixa de diálogo Abrir Arquivo inserindo Arquivo: Abrir na paleta de comandos](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>Salvar um notebook

Atualmente, há uma forma de salvar um notebook. Selecione **Salvar** na barra de ferramentas do notebook.

![Salve o arquivo selecionando Salvar na barra de ferramentas do notebook](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> Os métodos a seguir atualmente não salvam alterações em notebooks:
>
> - Os comandos **Salvar Arquivo**, **Salvar Arquivo como...** e **Salvar Tudo** do menu Arquivo.
> - Os comandos **Arquivo: Salvar** inseridos na paleta de comandos.

## <a name="change-the-connection"></a>Alterar a conexão

Para alterar a conexão de um notebook:

1. Selecione o menu **Anexar a** na barra de ferramentas do notebook e, em seguida, **Alterar Conexão**.

   ![Clique no menu Anexar a na barra de ferramentas do notebook](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. Agora você pode selecionar um servidor de conexão recente ou inserir novos detalhes de conexão para se conectar.

   ![Selecione um servidor no menu Anexar a](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre notebooks no Azure Data Studio, confira [Como usar notebooks no SQL Server 2019](notebooks-guidance.md).
