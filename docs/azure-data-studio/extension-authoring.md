---
title: Crie extensões
titleSuffix: Azure Data Studio
description: Saiba mais sobre como criar e adicionar extensões ao estúdio de dados do Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959603"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estender a funcionalidade com a criação de extensões do Studio de dados do Azure

Extensões no [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornecem uma maneira fácil de adicionar mais funcionalidade à base [!INCLUDE[name-sos](../includes/name-sos-short.md)] instalação.

Extensões são fornecidas pela equipe do estúdio de dados do Azure (Microsoft), bem como a comunidade de terceiros 3ª (você)!.


## <a name="author-an-extension"></a>Criar uma extensão

Se você estiver interessado em estender o estúdio de dados do Azure, você pode criar sua própria extensão e publicá-lo na Galeria de extensão.

**Escrevendo uma extensão**

***Pré-requisitos***

Para desenvolver uma extensão, você precisa Node. js instalado e disponível no seu $PATH. Node. js inclui npm, o Gerenciador de pacotes do Node. js, que será usado para instalar o gerador de extensão.

Para iniciar a nova extensão, você pode usar o gerador de extensão do Studio de dados do Azure. O Yeoman [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) torna muito fácil criar projetos de extensão simples. Para iniciar o gerador, digite o seguinte em um prompt de comando:

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**Referências de extensibilidade**

Para saber mais sobre a extensibilidade do Azure Data Studio consulte [visão geral da extensibilidade](extensibility.md). Você também pode ver exemplos de como usar a API existente [exemplos](https://github.com/Microsoft/azuredatastudio/tree/master/samples).


## <a name="debug-an-extension"></a>Uma extensão de depuração

Você pode depurar sua nova extensão usando a extensão do Visual Studio Code [Azure dados Studio depurar](https://github.com/kevcunnane/sqlops-debug).

Etapas
- Abra sua extensão com [Visual Studio Code](https://code.visualstudio.com/)
- Instalar a extensão Azure dados Studio depurar
- Pressione **F5** ou clique no ícone de depuração e clique em **iniciar**.
- Uma nova instância da Azure Data Studio é iniciado em um modo especial (Host de desenvolvimento de extensão) e essa nova instância já está ciente da sua extensão.


## <a name="create-an-extension-package"></a>Criar um pacote de extensão

Depois de escrever sua extensão, você precisará criar um pacote VSIX para ser capaz de instalá-lo no estúdio de dados do Azure. Você pode usar [vsce](https://github.com/Microsoft/vscode-vsce) para criar o pacote VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Publicar uma extensão

Para publicar sua nova extensão para o Studio de dados do Azure:

1. Adicionar sua extensão https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. No momento, não temos suporte para extensões de terceiros de host, portanto, em vez de baixar a extensão, o Studio de dados do Azure tem a opção para navegar até uma página de download. Para definir uma página de download para a sua extensão, defina o valor do ativo "Microsoft.AzureDataStudio.DownloadPage".
3. Crie uma solicitação de pull no branch de lançamento/extensões.
4. Envie uma solicitação de revisão para a equipe.

Sua extensão será revisada e adicionada à Galeria de extensão.

**A publicação de atualizações de extensão** o processo para publicar atualizações é semelhante a publicação da extensão. Verifique se que a versão é atualizada em Package. JSON
