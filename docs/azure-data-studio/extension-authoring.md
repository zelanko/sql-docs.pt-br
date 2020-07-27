---
title: Criar extensões
description: Saiba como criar e publicar extensões no Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 63a4c95f12aefafec97a58a186d33a5095b90dc2
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86483840"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estender a funcionalidade criando extensões do Azure Data Studio

As extensões no Azure Data Studio fornecem uma forma fácil de adicionar mais funcionalidade à instalação básica do Azure Data Studio.

As extensões são fornecidas pela equipe de Azure Data Studio (Microsoft), bem como pela comunidade de terceiros (você!).


## <a name="author-an-extension"></a>Criar uma extensão

Se estiver interessado em estender o Azure Data Studio, você poderá criar sua própria extensão e publicá-la na galeria de extensões.

**Como escrever uma extensão**

***Pré-requisitos***

Para desenvolver uma extensão, você precisa ter o [Node.js](https://nodejs.org/) instalado e disponível em seu `$PATH`. O Node.js inclui o npm, o Gerenciador de Pacotes do Node.js, que será usado para instalar o gerador de extensão.

Para criar sua extensão, você pode usar o Gerador de Extensão do Azure Data Studio. O [Gerador de Extensão](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman é um bom ponto de partida para projetos de extensão. Para iniciar o gerador, digite o seguinte em um prompt de comando:

```
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

Para obter um guia detalhado de como começar a usar seu modelo de extensão, confira [Criando uma extensão](https://docs.microsoft.com/sql/azure-data-studio/tutorial-create-extension?view=sql-server-ver15), que orienta você durante a criação de uma extensão de mapa de teclas.

**Referências de Extensibilidade**

Para saber mais sobre a Extensibilidade do Azure Data Studio, confira [Visão geral de extensibilidade](extensibility.md). Você também pode ver exemplos de como usar a API em [amostras](https://github.com/Microsoft/azuredatastudio/tree/main/samples) existentes.


## <a name="debug-an-extension"></a>Depurar uma extensão

Você pode depurar sua nova extensão usando a extensão do Visual Studio Code [Depuração do Azure Data Studio](https://github.com/kevcunnane/sqlops-debug).

Etapas
1. Abra a extensão com o [Visual Studio Code](https://code.visualstudio.com/).
1. Instale a extensão de Depuração do Azure Data Studio.
1. Pressione **F5** ou clique no ícone Depurar e clique em **Iniciar**.
1. Uma nova instância do Azure Data Studio é iniciada em um modo especial (Host de Desenvolvimento de Extensão) e essa nova instância agora está ciente de sua extensão.


## <a name="create-an-extension-package"></a>Criar um pacote de extensão

Depois de escrever sua extensão, você precisa criar um pacote VSIX para poder instalá-la no Azure Data Studio. Você pode usar [vsce](https://github.com/Microsoft/vscode-vsce) (Visual Studio Code Extensions) para criar o pacote VSIX. 

```
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

Com um pacote VSIX, você pode compartilhar a extensão localmente e de maneira privada compartilhando o arquivo `.vsix` e usando o comando **Extensões: Instalar do arquivo VSIX** na paleta de comandos para instalar a extensão no Azure Data Studio.


## <a name="publish-an-extension"></a>Publicar uma extensão

Para publicar sua nova extensão para o Azure Data Studio:

1. Adicione sua extensão a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. No momento, não há suporte para hospedar extensões de terceiros, portanto, em vez de baixar a extensão, o Azure Data Studio tem a opção de navegar até uma página de download. Para definir uma página de download para sua extensão, defina o valor do ativo "Microsoft.AzureDataStudio. DownloadPage".
3. Crie uma PR em relação ao branch de versão/extensões.
4. Envie uma solicitação de análise para a equipe.

Sua extensão será revisada e adicionada à galeria de extensões.

**Publicando atualizações de extensão**

O processo de publicar atualizações é semelhante ao de publicar a extensão. Verifique se a versão está atualizada em package.json.
