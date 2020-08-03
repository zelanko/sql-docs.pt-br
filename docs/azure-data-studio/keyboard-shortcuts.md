---
title: Criar e personalizar atalhos de teclado
description: Saiba como exibir, editar e criar atalhos de teclado no Azure Data Studio, usando uma funcionalidade baseada naquela do Visual Studio Code.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 008c44e8e0ca61d4b2e84ba9e25863d4ffa78fa7
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411067"
---
# <a name="keyboard-shortcuts-in-azure-data-studio"></a>Atalhos de teclado no Azure Data Studio

Este artigo apresenta as etapas para ver, editar e criar rapidamente atalhos de teclado no Azure Data Studio.

Uma vez que o Azure Data Studio herda a funcionalidade de associação de teclas do Visual Studio Code, informações detalhadas sobre personalizações avançadas usando diferentes layouts de teclado etc. estão no artigo [Associações de teclas para o Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings). Alguns recursos de associação de teclas podem não estar disponíveis (por exemplo, não há suporte para extensões de mapa de teclas no Azure Data Studio).

## <a name="open-the-keyboard-shortcuts-editor"></a>Abrir o editor de Atalhos de Teclado

Para exibir todos os atalhos de teclado definidos no momento:

Abra o editor de **Atalhos de Teclado** no menu **Arquivo**: **Arquivo** > **Preferências** > **Atalhos de Teclado** (**Azure Data Studio** > **Preferências** > **Atalhos de Teclado** no Mac).

Além de exibir as associações de teclas atuais, o editor de **Atalhos de Teclado** lista os comandos disponíveis que não têm atalhos de teclado definidos. O editor de **Atalhos de Teclado** permite que você altere, remova, redefina e defina facilmente novas associações de teclas.  

## <a name="edit-existing-keyboard-shortcuts"></a>Editar atalhos de teclado existentes

Para alterar a associação de teclas para um atalho de teclado existente:

1. Localize o atalho de teclado que você deseja alterar usando a caixa de pesquisa ou rolando na lista.
   > [!TIP]
   > Pesquise por tecla, por comando, por fonte etc. para retornar todos os atalhos de teclado relevantes.

2. Clique com o botão direito do mouse na entrada desejada e selecione **Alterar Associação de Teclas**

   ![editar atalho de teclado](media/keyboard-shortcuts/change-keybinding.png)

3. Pressione a combinação de teclas desejada e pressione **Enter** para salvá-la. 

   ![salvar atalho de teclado](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Criar novos atalhos de teclado

Para criar novos atalhos de teclado:

1. clique com o botão direito do mouse em um comando que não tem nenhuma associação de teclas e selecione **Adicionar Associação de Teclas**.

   ![criar atalho de teclado](media/keyboard-shortcuts/add-keybinding.png)

2. Pressione a combinação de teclas desejada e pressione **Enter** para salvá-la.