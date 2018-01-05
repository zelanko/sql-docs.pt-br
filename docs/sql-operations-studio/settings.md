---
title: "Operações do SQL Studio (visualização) usuário e configurações de espaço de trabalho | Microsoft Docs"
description: "Como modificar o Studio de operações do SQL (visualização) usuário e configurações de espaço de trabalho."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2edea069c05e7ac0316042250f336f1a8c455af0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="user-and-workspace-settings"></a>Configurações do usuário e espaço de trabalho

É fácil de configurar [!INCLUDE[name-sos](../includes/name-sos-short.md)] de sua preferência por meio de configurações. Quase todas as partes do [!INCLUDE[name-sos](../includes/name-sos-short.md)]do editor de interface do usuário e comportamento funcional tem opções você pode modificar.

[!INCLUDE[name-sos](../includes/name-sos-short.md)]fornece dois escopos diferentes configurações:

* **Usuário** essas configurações se aplicam globalmente a qualquer instância do [!INCLUDE[name-sos](../includes/name-sos-short.md)] abrir.
* **Espaço de trabalho** configurações de espaço de trabalho são configurações específicas para uma pasta no seu computador e estão disponíveis somente quando a pasta é aberta na barra lateral do Explorer. As configurações definidas neste escopo substituem o escopo do usuário.

## <a name="creating-user-and-workspace-settings"></a>Criação de usuário e configurações de espaço de trabalho

O comando de menu **arquivo** > **preferências** > **configurações** (**código**  >  **Preferências** > **configurações** no Mac) fornece o ponto de entrada para definir as configurações de usuário e o espaço de trabalho. São fornecidos com uma lista de configurações padrão. Copie qualquer configuração que você deseja alterar a apropriada `settings.json` arquivo. As guias à direita permitem que você alternar rapidamente entre os arquivos de configurações do usuário e o espaço de trabalho.

Você também pode abrir as configurações de usuário e o espaço de trabalho do **comando paleta** (**Ctrl + Shift + P**) com **preferências: Abra as configurações do usuário** e  **Preferências: Configurações de espaço de trabalho aberta** ou use o atalho de teclado (**Ctrl +**).

O exemplo a seguir desabilita os números de linha no editor e configura as linhas de quebra automaticamente com base no tamanho do editor de texto.

![Configurações de exemplo](media/settings/sample-settings.png)

Alterações nas configurações serão recarregadas por [!INCLUDE[name-sos](../includes/name-sos-short.md)] após a modificação `settings.json` arquivo é salvo.

>**Observação:** configurações de espaço de trabalho são úteis para o compartilhamento de configurações específicas do projeto em uma equipe.

## <a name="settings-file-locations"></a>Locais de arquivo de configurações

Dependendo de sua plataforma, o arquivo de configurações do usuário está localizado aqui:

* **Windows**`%APPDATA%\sqlops\User\settings.json`
* **Mac**`$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux**`$HOME/.config/sqlops/User/settings.json`

O arquivo de configuração do espaço de trabalho está localizado sob o `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` pasta em seu projeto.


## <a name="additional-resources"></a>Recursos adicionais

Porque [!INCLUDE[name-sos](../includes/name-sos-short.md)] herda as configurações de usuário e o espaço de trabalho a funcionalidade do código do Visual Studio, informações detalhadas sobre configurações está no [configurações para o código do Visual Studio](https://code.visualstudio.com/docs/getstarted/settings) artigo.