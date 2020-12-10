---
title: Criar uma extensão do Jupyter Notebook
description: Saiba mais sobre como empacotar notebooks em uma extensão usando o gerador de extensão.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 44080250d95d21cecca16ff605ca22683e5b4440
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96900809"
---
# <a name="create-a-jupyter-notebook-extension"></a>Criar uma extensão do Jupyter Notebook

Este tutorial demonstra como criar uma extensão do Jupyter Notebook no Azure Data Studio. A extensão envia um Jupyter Notebook de exemplo que pode ser aberto e executado no Azure Data Studio.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> - Criar um projeto de extensão.
> - Instalar o gerador de extensão.
> - Criar sua extensão de notebook.
> - Executar sua extensão.
> - Empacotar sua extensão.
> - Publicar sua extensão no marketplace.

## <a name="apis-used"></a>APIs usadas

- `azdata.nb.showNotebookDocument`

### <a name="extension-use-cases"></a>Casos de uso da extensão

Há algumas razões diferentes para criaria uma extensão de notebook:
- Compartilhar a documentação interativa
- Salvar e ter acesso constante a esse notebook
- Fornecer problemas de codificação para que os usuários acompanhem
- Controlar a versão e as atualizações do notebook

## <a name="prerequisites"></a>Pré-requisitos

O Azure Data Studio se baseia na mesma estrutura que o Visual Studio Code, portanto, as extensões para o Azure Data Studio são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- O [Node.js](https://nodejs.org) instalado e disponível em seu `$PATH`. O Node.js inclui o [npm](https://www.npmjs.com/), o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.
- O [Visual Studio Code](https://code.visualstudio.com) para depurar a extensão.
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção **Adicionar ao Caminho** em setup.exe. Para Mac ou Linux, execute o **Comando instalar 'azuredatastudio' no caminho**.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) usando o Yeoman. Para instalá-lo, execute o seguinte comando no prompt de comando:

```console
npm install -g yo generator-azuredatastudio
```

## <a name="create-your-extension"></a>Criar sua extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novos Notebooks (Individuais)** na lista de tipos de extensão.

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Gerador de extensão do notebook":::

3. Siga as etapas para preencher o nome da extensão. Neste tutorial, use um **Notebook de Teste**. Em seguida, preencha um nome de editor. Para este tutorial, use **Microsoft**. Por fim, adicione uma descrição.

Agora, é aí que existe uma ramificação. Você pode adicionar Jupyter Notebooks já criados ou usar notebooks de exemplo fornecidos por meio do gerador.

Neste tutorial, usaremos um notebook do Python de exemplo:

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="Selecionar exemplo do Python":::

Caso você tenha notebooks que queira enviar, responda que você tem notebooks existentes que deseja enviar. Forneça o caminho absoluto do arquivo em que todos os seus notebooks ou arquivos markdown residem.

A conclusão das etapas anteriores cria uma pasta com o notebook de exemplo. Abra a pasta no Visual Studio Code e você estará pronto para enviar sua nova extensão de notebook.

## <a name="understand-your-extension"></a>Noções básicas da extensão

É esta a aparência que o projeto deverá ter:

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="estrutura do arquivo de extensão":::

O arquivo `vsc-extension-quickstart.md` fornece uma referência dos arquivos importantes. `README.md` é o arquivo em que você pode fornecer a documentação da nova extensão. Observe os arquivos `package.json`, `notebook.ts` e `pySample.ipynb`.

Se houver arquivos ou pastas que você não quer publicar, inclua os nomes deles no arquivo `.vscodeignore`.

Vamos dar uma olhada em `notebook.ts` para entender o que a extensão recém-formada faz.

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from the
// command palette in Azure Data Studio. If you want any additional functionality
// to occur when you launch the book, add it to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command.
}
```

Essa é a função principal em `notebook.ts` chamada sempre que executamos a extensão por meio do comando **Iniciar Notebooks:** Testar Notebook. Criamos nosso comando usando a API `vscode.commands.registerCommand`. A definição a seguir dentro das chaves é o código executado cada vez que chamamos nosso comando. Para cada notebook encontrado na função `processNotebooks`, nós o abrimos no Azure Data Studio usando `azdata.nb.showNotebookDocument`.

O arquivo `package.json` também desempenha um papel importante no registro do comando **Iniciar Notebooks:** Testar Notebook.

```json
"activationEvents": [
        "onCommand:launchNotebooks.test-notebook"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchNotebooks.test-notebook",
                "title": "Launch Notebooks: Test Notebook"
            }
        ]
    }
```

Temos um evento de ativação para o comando e também adicionamos pontos de contribuição específicos. Esses pontos de contribuição são exibidos no marketplace de extensões, em que as extensões são publicadas, quando os usuários veem sua extensão. Caso deseje adicionar mais comandos, lembre-se de adicioná-los ao campo `activationEvents`. Para ver mais opções, confira [Eventos de ativação](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar a extensão com outras pessoas, você precisará empacotá-la em um só arquivo. Sua extensão pode ser publicada no marketplace de extensões do Azure Data Studio ou compartilhada entre a sua equipe ou sua comunidade. Para realizar essa etapa, você precisa instalar outro pacote npm da linha de comando.

```console
npm install -g vsce
```

Edite o arquivo `README.md` de sua preferência. Navegue até o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

Depois que essas linhas forem adicionadas, um arquivo `my test-notebook-0.0.1.vsix` será criado e estará pronto para ser instalado e compartilhado com outras pessoas.

## <a name="run-your-extension"></a>Executar a extensão

Para executar e testar a extensão, abra o Azure Data Studio e a paleta de comandos selecionando **Ctrl+Shift+P**. Localize o comando **Extensões: fazer a instalação com base no arquivo VSIX** e procure a pasta que contém a nova extensão.

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="Instalar o VSIX":::

Agora sua extensão será exibida no painel de extensões do Azure Data Studio. Abra a paleta de comandos novamente e você encontrará o comando que criamos com a extensão **Abrir Livro: Livro de Teste**. Após a execução, ele deve abrir o Jupyter Book que empacotamos com nossa extensão.

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Comando do notebook":::

Parabéns! Você criou e agora poderá enviar sua primeira extensão do Jupyter Notebook.

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio está em construção. Para publicar, hospede o VSIX de extensão em algum lugar, por exemplo, em uma página de versão do GitHub. Em seguida, envie uma solicitação de pull que atualiza [esse arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com suas informações de extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Criar um projeto de extensão.
> - Instalar o gerador de extensão.
> - Criar sua extensão de notebook.
> - Criar sua extensão.
> - Empacotar sua extensão.
> - Publicar sua extensão no marketplace.

Esperamos que, depois de ler esse artigo, você tenha inspiração para criar uma extensão para o Azure Data Studio.

Caso tenha uma ideia, mas não saiba exatamente como começar a desenvolvê-la, abra um problema ou envie um tweet para a equipe em [azuredatastudio](https://twitter.com/azuredatastudio).

Para obter mais informações, o [guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) abrange todas as APIs e os padrões existentes.
