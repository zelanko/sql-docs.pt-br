---
title: Criar extensões
titleSuffix: Azure Data Studio
description: Aprender a criar e adicionar extensões ao Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959603"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estender a funcionalidade criando extensões do Azure Data Studio

As extensões em [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornecem uma maneira fácil de adicionar mais funcionalidade à instalação básica do [!INCLUDE[name-sos](../includes/name-sos-short.md)].

As extensões são fornecidas pela equipe de Azure Data Studio (Microsoft), bem como pela comunidade de terceiros (você!).


## <a name="author-an-extension"></a>Criar uma extensão

Se estiver interessado em estender o Azure Data Studio, você poderá criar sua própria extensão e publicá-la na galeria de extensões.

**Como escrever uma extensão**

***Pré-requisitos***

Para desenvolver uma extensão, você precisa ter o Node.js instalado e disponível em seu $PATH. O Node.js inclui o npm, o Gerenciador de Pacotes do Node.js, que será usado para instalar o gerador de extensão.

Para iniciar sua nova extensão, você pode usar o gerador de Extensão do Azure Data Studio. O [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman torna muito fácil criar projetos de extensão simples. Para iniciar o gerador, digite o seguinte em um prompt de comando:

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**Referências de Extensibilidade**

Para saber mais sobre a Extensibilidade do Azure Data Studio, confira [Visão geral de extensibilidade](extensibility.md). Você também pode ver exemplos de como usar a API em [amostras](https://github.com/Microsoft/azuredatastudio/tree/master/samples) existentes.


## <a name="debug-an-extension"></a>Depurar uma extensão

Você pode depurar sua nova extensão usando a extensão do Visual Studio Code [Depuração do Azure Data Studio](https://github.com/kevcunnane/sqlops-debug).

Etapas
- Abra sua extensão com o [Visual Studio Code](https://code.visualstudio.com/)
- Instalar a extensão de Depuração do Azure Data Studio
- Pressione **F5** ou clique no ícone Depurar e clique em **Iniciar**.
- Uma nova instância do Azure Data Studio é iniciada em um modo especial (Host de Desenvolvimento de Extensão) e essa nova instância agora está ciente de sua extensão.


## <a name="create-an-extension-package"></a>Criar um pacote de extensão

Depois de escrever sua extensão, você precisa criar um pacote VSIX para poder instalá-la no Azure Data Studio. Você pode usar o [vsce](https://github.com/Microsoft/vscode-vsce) para criar o pacote VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Publicar uma extensão

Para publicar sua nova extensão para o Azure Data Studio:

1. Adicione sua extensão a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. No momento, não há suporte para hospedar extensões de terceiros, portanto, em vez de baixar a extensão, o Azure Data Studio tem a opção de navegar até uma página de download. Para definir uma página de download para sua extensão, defina o valor do ativo "Microsoft.AzureDataStudio. DownloadPage".
3. Crie uma PR em relação ao branch de versão/extensões.
4. Envie uma solicitação de análise para a equipe.

Sua extensão será revisada e adicionada à galeria de extensões.

**Como publicar atualizações de extensão** O processo para publicar atualizações é semelhante ao de publicar a extensão. Verifique se a versão esteja atualizada em package.json
