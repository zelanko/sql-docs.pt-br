---
title: Controle do código-fonte
description: O Azure Data Studio dá suporte ao Git para SCM (Gerenciamento de Controle do Código-Fonte). Saiba como abrir um repositório Git existente e como inicializar um novo.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2019
ms.openlocfilehash: 7f032d870952cdadbde79dbf56f4c63ae351d6e9
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081565"
---
# <a name="source-control-in-azure-data-studio"></a>Controle do código-fonte no Azure Data Studio

O Azure Data Studio é compatível com o Git para controle do código-fonte/versão.

## <a name="git-support-in-azure-data-studio"></a>Compatibilidade do Git no Azure Data Studio

O Azure Data Studio é fornecido com um SCM (gerenciador de controle do código-fonte) do Git, mas você ainda precisa [instalar o Git (versão 2.0.0 ou posterior)](https://git-scm.com/download) para que esses recursos fiquem disponíveis.

## <a name="open-an-existing-git-repository"></a>Abrir um repositório Git existente

1. No menu **Arquivo**, selecione **Abrir Pasta...**
2. Navegue até a pasta que contém os arquivos rastreados pelo Git e selecione **Selecionar Pasta**. As subpastas no repositório local podem ser selecionadas aqui.

## <a name="initialize-a-new-git-repository"></a>Inicializar um novo repositório Git

1. Selecione **Controle do Código-Fonte** e, em seguida, selecione o ícone do Git.

   ![Ícone do Git no controle do código-fonte](media/source-control/source-control.png)

1. Insira o caminho para a pasta que você deseja inicializar como um repositório Git e pressione **Enter**.

   ![Inicializar repositório Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabalhando com repositórios Git

O Azure Data Studio herda sua implementação do Git do VS Code, mas atualmente não é compatível com provedores de SCM adicionais. Para obter detalhes sobre como trabalhar com o Git depois de abrir ou inicializar um repositório, confira [Suporte do Git no VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).

## <a name="additional-resources"></a>Recursos adicionais

- [Documentação do Git](https://git-scm.com/documentation)
