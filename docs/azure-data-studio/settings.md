---
title: Configurações do Workspace e do Usuário
titleSuffix: Azure Data Studio
description: Como personalizar o Azure Data Studio modificando as Configurações do Usuário e do Workspace.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a874aaf9ec136ff9ea27cbeaa92011a07f3718c7
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287060"
---
# <a name="modify-user-and-workspace-settings"></a>Modificar Configurações do Workspace e do Usuário

É fácil configurar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] de acordo com suas preferências usando as configurações. Quase todas as partes do editor, da interface do usuário e do comportamento funcional do [!INCLUDE[name-sos](../includes/name-sos-short.md)] têm opções que podem ser modificadas.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece dois escopos diferentes para as configurações:

* **Usuário** Essas configurações se aplicam globalmente a qualquer instância de [!INCLUDE[name-sos](../includes/name-sos-short.md)] que você abrir.
* **Workspace** Configurações do workspace são configurações específicas a uma pasta em seu computador e só estão disponíveis quando a pasta está aberta na barra lateral do Explorer. Configurações definidas nesse escopo substituem o escopo do usuário.

## <a name="creating-user-and-workspace-settings"></a>Criando Configurações do Workspace e do Usuário

O comando de menu **Arquivo** > **Preferências** > **Configurações** (**Código** > **Preferências** > **Configurações** no Mac) fornece o ponto de entrada para definir configurações do usuário e do workspace. Você recebe uma lista de Configurações Padrão. Copie as configurações que quiser alterar para o arquivo `settings.json` apropriado. As guias à direita permitem alternar rapidamente entre os arquivos de configurações do usuário e do workspace.

Você também pode abrir as configurações do usuário e do workspace na **Paleta de Comandos** (**Ctrl+Shift+P**) usando **Preferências: Abrir Configurações do Usuário** e **Preferências: Abrir Configurações do Workspace** ou usando o atalho de teclado (**Ctrl+,** ).

O exemplo a seguir desabilita números de linha no editor e configura as linhas de código para serem recuadas automaticamente.

![Configurações de exemplo](media/settings/sample-settings.png)

Alterações nas configurações são recarregadas por [!INCLUDE[name-sos](../includes/name-sos-short.md)] após o arquivo `settings.json` modificado ser salvo.

>**Observação:** as configurações do workspace são úteis para compartilhar configurações específicas do projeto com uma equipe.

## <a name="settings-file-locations"></a>Locais do arquivo de configurações

Dependendo de sua plataforma, o arquivo de configurações do usuário fica localizado aqui:

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

O arquivo de configuração do workspace fica localizado na pasta `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` de seu projeto.

## <a name="hot-exit"></a>Hot Exit

Por padrão, o Azure Data Studio memoriza alterações de arquivos não salvas quando você sai. É o mesmo que o recurso de Hot Exit do Visual Studio Code.

Por padrão, Hot Exit fica desativado. Habilite o recurso de Hot Exit editando a configuração `files.hotExit`. Para obter detalhes, confira [Hot Exit (na documentação do Visual Studio Code)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit).


## <a name="tab-color"></a>Cor da guia

Para simplificar a identificação das conexões com que você está trabalhando, as guias abertas no editor podem ter suas cores definidas de forma a corresponder à cor do grupo de servidores ao qual a conexão pertence. Por padrão, as cores das guias ficam desativadas. Habilite o recurso de cores das guias editando a configuração `sql.tabColorMode`.

## <a name="additional-resources"></a>Recursos adicionais

Como o [!INCLUDE[name-sos](../includes/name-sos-short.md)] herda a funcionalidade de configurações do usuário e do workspace do Visual Studio Code, há informações detalhadas sobre as configurações no artigo [Configurações para o Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings).
