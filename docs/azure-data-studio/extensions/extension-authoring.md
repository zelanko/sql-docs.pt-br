---
title: Criar extensões
description: É possível adicionar funcionalidade ao Azure Data Studio com uma extensão. Saiba como criar uma extensão e publicá-la na galeria de extensões.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: ''
ms.date: 08/26/2020
ms.openlocfilehash: 92c6a5d9522d015786eafdefaeea64b46925b92b
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364033"
---
# <a name="extend-functionality-by-creating-azure-data-studio-extensions"></a>Estender a funcionalidade criando extensões do Azure Data Studio

As extensões no Azure Data Studio fornecem uma forma fácil de adicionar mais funcionalidade à instalação básica do Azure Data Studio.

As extensões são fornecidas pela equipe do Azure Data Studio (Microsoft), bem como pela comunidade de terceiros (você!).

## <a name="author-an-extension"></a>Criar uma extensão

Se tiver interesse em estender o Azure Data Studio, você poderá criar a própria extensão e publicá-la na galeria de extensões.

### <a name="write-an-extension"></a>Escrever uma extensão

#### <a name="prerequisites"></a>Pré-requisitos

Para desenvolver uma extensão, você precisa ter o [Node.js](https://nodejs.org/) instalado e disponível em seu `$PATH`. O Node.js inclui o npm, o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.

Para criar sua extensão, você pode usar o gerador de extensão do Azure Data Studio. O [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman é um bom ponto de partida para projetos de extensão. Para iniciar o gerador, insira o seguinte comando em um prompt de comando:

```console
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

Para obter um guia detalhado de como começar a usar seu modelo de extensão, confira [extensão de mapa de teclas](keymap-extension.md), que orienta você durante a criação de uma extensão.

### <a name="extensibility-references"></a>Referências de extensibilidade

Para saber mais sobre a extensibilidade do Azure Data Studio, confira [Visão geral de extensibilidade](../extensibility.md). Você também pode ver exemplos de como usar a API em [amostras](https://github.com/Microsoft/azuredatastudio/tree/main/samples) existentes.

## <a name="debug-an-extension"></a>Depurar uma extensão

Você pode depurar sua nova extensão usando a extensão do Visual Studio Code [Depuração do Azure Data Studio](https://github.com/kevcunnane/sqlops-debug).

Para depurar sua extensão:

1. Abra a extensão com o [Visual Studio Code](https://code.visualstudio.com/).
2. Instale a extensão de Depuração do Azure Data Studio.
3. Selecione **F5** ou o ícone **Depurar** e, em seguida, **Iniciar**.
4. Uma nova instância do Azure Data Studio é iniciada em um modo especial (Host de Desenvolvimento de Extensão). Essa nova instância agora está ciente da sua extensão.

## <a name="create-an-extension-package"></a>Criar um pacote de extensão

Depois de escrever a extensão, você precisa criar um pacote VSIX que a instala no Azure Data Studio. Você pode usar [vscode-vsce](https://github.com/Microsoft/vscode-vsce) (Extensões do Visual Studio Code) para criar o pacote VSIX.

```console
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

Com um pacote VSIX, você pode compartilhar a extensão localmente e de maneira privada compartilhando o arquivo .vsix e usando o comando **Extensões: fazer a instalação com base no arquivo VSIX** na paleta de comandos para instalar a extensão no Azure Data Studio.

## <a name="publish-an-extension"></a>Publicar uma extensão

Para publicar sua nova extensão para o Azure Data Studio:

1. Adicione sua extensão à [galeria de extensões](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json).
2. No momento, não há suporte para hospedar extensões de terceiros. Em vez de baixar a extensão, o Azure Data Studio tem a opção de navegar até uma página de download. Para definir uma página de download para sua extensão, defina o valor do ativo **Microsoft.AzureDataStudio.DownloadPage**.
3. Crie uma PR em relação ao branch de versão/extensões.
4. Envie uma solicitação de análise para a equipe.

Sua extensão será examinada e adicionada à galeria de extensões.

### <a name="publish-extension-updates"></a>Publicar atualizações de extensão

O processo de publicar atualizações é semelhante ao de publicar a extensão. Verifique se a versão está atualizada em package.json.

## <a name="next-steps"></a>Próximas etapas

Confira um dos seguintes tutoriais de criação de extensões para obter instruções passo a passo sobre como começar a criá-los:

- [Tutorial da extensão de mapa de teclas](keymap-extension.md)
- [Tutorial da extensão de painel](dashboard-extension.md)
- [Tutorial da extensão de notebook](notebook-extension.md)
- [Tutorial da extensão do Jupyter Book](jupyter-book-extension.md)
- [Tutorial da extensão de assistente](wizard-extension.md)
