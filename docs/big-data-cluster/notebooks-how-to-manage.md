---
title: 'Gerenciar notebooks: Azure Data Studio'
titleSuffix: SQL Server Big Data Clusters
description: Aprenda a gerenciar notebooks no Azure Data Studio. Isso inclui abrir notebooks, salvá-los e alterar sua conexão de cluster de Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8cf37ff6a4ad5e2b627fa5d968391cc5a7597a4a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244086"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Como gerenciar notebooks no Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo mostra como abrir e salvar arquivos de notebook no Azure Data Studio com o SQL Server. Ele também demonstra como alterar sua conexão com o cluster de Big Data do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

Este artigo pressupõe que você já tem um notebook que deseja usar no Azure Data Studio. Se quiser criar um notebook, confira [Como usar notebooks no SQL Server](notebooks-guidance.md). Para usar notebooks no Azure Data Studio, você deve atender aos seguintes pré-requisitos:

- [Implantar um cluster de Big Data](quickstart-big-data-cluster-deploy.md).
- [Ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Abrir um notebook

Há várias maneiras de abrir a caixa de diálogo **Abrir Notebook**. Você pode usar o menu Arquivo, o Painel e a Paleta de Comandos. As seções a seguir descrevem cada método.

### <a name="file-menu"></a>Menu Arquivo

Selecione **Abrir Arquivo** no menu Arquivo CTRL+O (no Windows) e Cmd+O (no Mac).

![Abra a caixa de diálogo Abrir Arquivo selecionando Abrir Arquivo](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Painel

Clique em **Abrir Notebook** no painel para abrir a caixa de diálogo Abrir Arquivo.

![Abrir a caixa de diálogo Abrir Arquivo selecionando Abrir Notebook no painel](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Paleta de Comandos

Use o comando **Arquivo: Abrir** da paleta de comandos digitando Ctrl+Shift+P (no Windows) e Cmd+Shift+P (no Mac).

![Abrir a caixa de diálogo Abrir Arquivo inserindo Arquivo:Abrir na paleta de comandos](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Salvar um notebook

Atualmente, há uma maneira de salvar um notebook. Você precisa selecionar **Salvar** na barra de ferramentas do notebook.

![Salvar o arquivo clicando em Salvar na barra de ferramentas do notebook](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> Os métodos a seguir atualmente não salvam alterações em notebooks:
>
> - Os comandos **Salvar Arquivo**, **Salvar Arquivo como...** e **Salvar Tudo** do menu Arquivo.
> - Os comandos **Arquivo: Salvar** inseridos na paleta de comandos.

## <a name="change-the-big-data-cluster"></a>Alterar um cluster de Big Data

Para alterar o cluster de Big Data do SQL Server para um notebook:

1. Clique no menu **Anexar a** da barra de ferramentas do notebook.

   ![Clique no menu Anexar a na barra de ferramentas do notebook](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Clique em um servidor no menu **Anexar a**.

   ![Selecione um servidor no menu Anexar a](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre notebooks no Azure Data Studio, confira [Como usar notebooks no SQL Server 2019](notebooks-guidance.md).
