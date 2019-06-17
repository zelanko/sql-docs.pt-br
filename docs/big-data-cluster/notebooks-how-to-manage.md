---
title: Gerenciar notebooks no estúdio de dados do Azure
titleSuffix: SQL Server big data clusters
description: Saiba como gerenciar notebooks no estúdio de dados do Azure. Isso inclui a abertura de blocos de anotações, salvando-os e alterar sua conexão de cluster de big data.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 9173c630514465914a31bb5b4c2999145884c78a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790052"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Como gerenciar notebooks no estúdio de dados do Azure

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo mostra como abrir e salvar arquivos de notebook no estúdio de dados do Azure com a visualização do SQL Server de 2019. Ele também demonstra como alterar sua conexão para seu cluster de big data do SQL Server.

## <a name="prerequisites"></a>Prerequisites

Este artigo pressupõe que você já tenha um bloco de anotações que você deseja usar no estúdio de dados do Azure. Se você quiser criar um bloco de anotações, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md). Para usar notebooks no estúdio de dados do Azure, você deve cumprir os seguintes pré-requisitos:

- [Implantar um cluster de big data](quickstart-big-data-cluster-deploy.md).
- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Abra um bloco de anotações

Há várias maneiras para abrir o **abrir o Notebook** caixa de diálogo. Você pode usar o menu Arquivo, o painel e a paleta de comandos. As seções a seguir descrevem cada método.

### <a name="file-menu"></a>Menu Arquivo

Selecione **abrir arquivo** no menu Arquivo Ctrl + O (no Windows) e o Cmd + O (em Mac).

![Abra a caixa de diálogo Abrir arquivo selecionando o arquivo aberto](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Painel

Clique em **abrir o Notebook** no painel para abrir a caixa de diálogo Abrir arquivo.

![Abra a caixa de diálogo Abrir arquivo, selecionando o bloco de anotações aberto no painel](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Paleta de comandos

Use o comando **arquivo: Abra** da paleta de comandos, digitando Ctrl + Shift + P (no Windows) e o Cmd + Shift + P (no Mac).

![Abra a caixa de diálogo Abrir arquivo digitando File:Open na paleta de comandos](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Salvar um bloco de anotações

Atualmente, há uma maneira de salvar um bloco de anotações. Você deve selecionar **salvar** na barra de ferramentas do bloco de anotações.

![Salve o arquivo clicando em Salvar na barra de ferramentas do bloco de anotações](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> Os métodos a seguir no momento não salvar as alterações a blocos de anotações:
>
> - **Salvar arquivo**, **salvar arquivo como...**  e **arquivo Salvar tudo** comandos no menu arquivo.
> - **Arquivo: Salvar** comandos inseridos na paleta de comandos.

## <a name="change-the-big-data-cluster"></a>Alterar o cluster de big data

Para alterar o cluster de big data do SQL Server para um bloco de anotações:

1. Clique o **anexar a** menu da barra de ferramentas do bloco de anotações.

   ![Clique em Anexar ao menu na barra de ferramentas do bloco de anotações](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Clique em um servidor a partir de **anexar a** menu.

   ![Selecione um servidor na anexação ao menu](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os blocos de anotações no estúdio de dados do Azure, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).