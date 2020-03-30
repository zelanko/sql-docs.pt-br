---
title: Controle do código-fonte
titleSuffix: Azure Data Studio
description: Saiba como configurar o controle do código-fonte no Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c278bcf6cff451396b3d677b203f207b68fd6dc5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959284"
---
#  <a name="using-source-control-in-name-sos"></a>Usando o controle do código-fonte no [!INCLUDE[name-sos](../includes/name-sos-short.md)]

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] dá suporte ao Git para controle do código-fonte/versão.


## <a name="git-support-in-name-sos"></a>Suporte do Git em [!INCLUDE[name-sos](../includes/name-sos-short.md)]

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] é fornecido com um SCM (gerenciador de controle do código-fonte) do Git, mas você ainda precisa [instalar o Git (versão 2.0.0 ou posterior)](https://git-scm.com/download) para que esses recursos fiquem disponíveis. 



## <a name="open-an-existing-git-repository"></a>Abrir um repositório Git existente

1. No menu **Arquivo**, selecione **Abrir Pasta...**
2. Navegue até a pasta que contém os arquivos rastreados pelo Git e clique em **Selecionar Pasta**. As subpastas no repositório local podem ser selecionadas aqui.


## <a name="initialize-a-new-git-repository"></a>Inicializar um novo repositório Git

1. Selecione **Controle do Código-Fonte** e, em seguida, selecione o ícone do Git.

   ![Ícone do Git no controle do código-fonte](media/source-control/source-control.png)

1. Insira o caminho para a pasta que você deseja inicializar como um repositório Git e pressione **Enter**.

   ![Inicializar repositório Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabalhando com repositórios Git

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] herda sua implementação do Git do VS Code, mas atualmente não dá suporte a provedores de SCM adicionais. Para obter detalhes sobre como trabalhar com o Git depois de abrir ou inicializar um repositório, confira [Suporte do Git no VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionais
- [Documentação do Git](https://git-scm.com/documentation)
