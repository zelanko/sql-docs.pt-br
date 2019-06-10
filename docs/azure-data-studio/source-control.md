---
title: Controle do código-fonte
titleSuffix: Azure Data Studio
description: Saiba como configurar o controle de origem no estúdio de dados do Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6431b869af8abc91a9de319f32c0576b82428a0a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798025"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Uso do controle do código-fonte no [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] oferece suporte ao Git para controle de versão/origem.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Suporte ao Git no [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] é fornecido com um Gerenciador de controle do código-fonte Git (SCM), mas você ainda precisará [instalar o Git (versão 2.0.0 ou posterior)](https://git-scm.com/download) antes que esses recursos estão disponíveis. 



## <a name="open-an-existing-git-repository"></a>Abrir um repositório Git existente

1. Sob o **arquivo** menu, selecione **Abrir pasta...**
2. Navegue até a pasta que contém os arquivos acompanhados pelo git e, em seguida, clique em **Selecionar pasta**. As subpastas no seu repositório local são okey selecionar aqui.


## <a name="initialize-a-new-git-repository"></a>Inicializar um novo repositório git

1. Selecione **controle de origem**, em seguida, selecione o ícone do git.

   ![Ícone do git de controle de origem](media/source-control/source-control.png)

1. Digite o caminho para a pasta que você deseja inicializar como um repositório Git e pressione **Enter**.

   ![Inicializar repositório Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabalhando com repositórios Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] herda sua implementação do Git do VS Code, mas não oferece suporte a provedores adicionais do SCM. Para obter detalhes sobre como trabalhar com Git, depois que você abre ou inicializar um repositório, consulte [suporte ao Git no VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionais
- [Documentação do Git](https://git-scm.com/documentation)
