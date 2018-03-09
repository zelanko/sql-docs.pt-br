---
title: "Fonte de controle no Studio de operações do SQL (visualização) | Microsoft Docs"
description: "Saiba como configurar o controle de origem no Studio de operações do SQL (visualização)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f28199262b087ad5362da0ddf56827216aec748
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Usando o controle de origem no[!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)]suporta Git para controle de versão/origem.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Suporte do Git em[!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)]é fornecido com um Gerenciador de controle do código-fonte Git (SCM), mas você ainda precisa [instale o Git (versão 2.0.0 ou superior)](https://git-scm.com/download) antes que esses recursos estão disponíveis. 



## <a name="open-an-existing-git-repository"></a>Abrir um repositório Git existente

1. Sob o **arquivo** menu, selecione **Abrir pasta...**
2. Navegue até a pasta que contém os arquivos controlados pelo git e, em seguida, clique em **Selecionar pasta**. As subpastas no seu repositório local são okey selecionar aqui.


## <a name="initialize-a-new-git-repository"></a>Inicializar um novo repositório git

1. Selecione **controle de origem**, em seguida, selecione o ícone de git.

   ![Ícone de git de controle do código-fonte](media/source-control/source-control.png)

1. Digite o caminho para a pasta que deseja inicializar como um repositório Git e pressione **Enter**.

   ![inicializar o repositório Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabalhando com repositórios Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)]herda sua implementação do Git de código VS, mas não oferece suporte a provedores SCM adicionais. Para obter detalhes sobre como trabalhar com Git, depois que você abre ou inicializar um repositório, consulte [Git suporte no código VS](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionais
- [Documentação do Git](https://git-scm.com/documentation)
