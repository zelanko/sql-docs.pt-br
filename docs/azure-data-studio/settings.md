---
title: Configurações do Workspace e do Usuário
description: Saiba como usar configurações para personalizar o editor, a interface do usuário e o comportamento funcional do Azure Data Studio para atender às suas preferências.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 06e9efa72ef82d8335db4b7ec6b8941c95501790
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364177"
---
# <a name="modify-user-and-workspace-settings"></a>Modificar Configurações do Workspace e do Usuário

É fácil configurar o Azure Data Studio de acordo com suas preferências usando as configurações. Quase todas as partes do editor, da interface do usuário e do comportamento funcional do Azure Data Studio têm opções que podem ser modificadas.

O Azure Data Studio oferece dois escopos diferentes para as configurações:

* **Usuário** – Essas configurações se aplicarão globalmente a qualquer instância do Azure Data Studio que você abre.
* **Workspace** – Configurações do workspace são configurações específicas a uma pasta em seu computador e só estão disponíveis quando a pasta está aberta na barra lateral do Explorer. Configurações definidas nesse escopo substituem o escopo do usuário.

## <a name="creating-user-and-workspace-settings"></a>Criando Configurações do Workspace e do Usuário

O comando de menu **Arquivo** > **Preferências** > **Configurações** (**Código** > **Preferências** > **Configurações** no Mac) fornece o ponto de entrada para definir configurações do usuário e do workspace. Você recebe uma lista de Configurações Padrão. Copie as configurações que quiser alterar para o arquivo `settings.json` apropriado. As guias à direita permitem alternar rapidamente entre os arquivos de configurações do usuário e do workspace.

Você também pode abrir as configurações do usuário e do workspace na **Paleta de Comandos** (**Ctrl+Shift+P**) usando **Preferências: Abrir Configurações do Usuário** e **Preferências: Abrir Configurações do Workspace** ou usando o atalho de teclado (**Ctrl+,** ).

O exemplo a seguir desabilita números de linha no editor e configura as linhas de código para serem recuadas automaticamente.

![Configurações de exemplo](media/settings/sample-settings.png)

As alterações nas configurações são recarregadas pelo Azure Data Studio depois que o arquivo modificado `settings.json` é salvo.

> [!NOTE]
> as configurações do workspace são úteis para compartilhar configurações específicas do projeto com uma equipe.

## <a name="settings-file-locations"></a>Locais do arquivo de configurações

Dependendo de sua plataforma, o arquivo de configurações do usuário fica localizado aqui:

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

O arquivo de configuração do workspace fica localizado na pasta `.Azure Data Studio` de seu projeto.

## <a name="hot-exit"></a>Hot Exit

Por padrão, o Azure Data Studio memoriza alterações de arquivos não salvas quando você sai. No Visual Studio Code, é o mesmo que o recurso de Hot Exit.

Por padrão, Hot Exit fica desativado. Habilite o recurso de Hot Exit editando a configuração `files.hotExit`. Para obter detalhes, confira [Hot Exit (na documentação do Visual Studio Code)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit).

## <a name="tab-color"></a>Cor da guia

Para simplificar a identificação das conexões com que você está trabalhando, as guias abertas no editor podem ter as respectivas cores definidas de maneira a corresponder à cor do grupo de servidores ao qual a conexão pertence. Por padrão, as cores das guias ficam desativadas. Habilite o recurso de cores das guias editando a configuração `sql.tabColorMode`.

## <a name="additional-resources"></a>Recursos adicionais

Como o Azure Data Studio herda a funcionalidade de configurações do usuário e do workspace do Visual Studio Code, há informações detalhadas sobre as configurações no artigo [Configurações para o Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings).
