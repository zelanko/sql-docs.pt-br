---
title: Criar uma extensão do Jupyter Notebook
description: Saiba mais sobre como empacotar notebooks em uma extensão usando o gerador de extensão
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 52a38a8074814737a30cb2f31d22da922eb76901
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288148"
---
# <a name="create-a-jupyter-notebook-extension"></a>Criar uma extensão do Jupyter Notebook

Este tutorial demonstra como criar uma extensão do Notebooks para o Azure Data Studio. A extensão envia um Jupyter Notebook de exemplo que pode ser aberto e executado no Azure Data Studio.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão
> - Criar sua extensão de notebook
> - Executar a extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

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
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção `Add to Path` em setup.exe. Para Mac ou Linux, execute o *Comando instalar 'azuredatastudio' no caminho*.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) usando o Yeoman. Para instalá-lo, execute o seguinte no prompt de comando:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>Criar sua extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novos Notebooks (Individuais)** na lista de tipos de extensão:

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Gerador de extensão do notebook":::

3. Siga as etapas para preencher o nome da extensão (neste tutorial, use **Notebook de Teste**), um nome de fornecedor (neste tutorial, use **Microsoft**) e adicione uma descrição.

Agora é nesse ponto em que há um branch: você pode adicionar Jupyter Notebooks já criados ou usar notebooks de exemplo fornecidos por meio do gerador.

Neste tutorial, usaremos um notebook do Python de exemplo:

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="Selecionar exemplo do Python":::

Se você tiver notebooks que esteja interessado em enviar, responda que você tem notebooks que deseja enviar e forneça o caminho de arquivo absoluto no qual todos os notebooks ou os arquivos de markdown residem.

A conclusão das etapas anteriores cria uma pasta com o notebook de exemplo. Abra a pasta no Visual Studio Code e você estará pronto para enviar sua nova extensão de notebook.

## <a name="understanding-your-extension"></a>Noções básicas sobre a extensão

É esta a aparência que o projeto deverá ter:

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="estrutura do arquivo de extensão":::

O `vsc-extension-quickstart.md` fornece uma referência dos arquivos importantes. O `README.md` é o arquivo em que você pode fornecer a documentação da nova extensão. Observe os arquivos `package.json`, `notebook.ts` e `pySample.ipynb`.

Se houver arquivos ou pastas que você não deseja publicar, inclua os nomes deles no arquivo `.vscodeignore`.

Vamos dar uma olhada em `notebook.ts` para entender o que a extensão recém-formada faz.

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command
}
```

Essa é a função principal em `notebook.ts` que é chamada sempre que executamos a extensão por meio do comando **Iniciar Notebooks:** Testar Notebook. Criamos o comando usando a API `vscode.commands.registerCommand`, e a definição a seguir dentro das chaves é que o código é executado sempre que chamamos o comando. Para cada notebook encontrado na função `processNotebooks`, nós o abrimos no Azure Data Studio usando `azdata.nb.showNotebookDocument`. 

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

Temos um evento de ativação para o comando e também adicionamos pontos de contribuição específicos. Eles são exibidos no marketplace de extensões, em que as extensões são publicadas, quando os usuários veem sua extensão. Caso deseje adicionar outros comandos, lembre-se de adicioná-los ao campo `activationEvents`. Para obter mais opções, confira [Eventos de ativação](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar com outras pessoas, você precisa empacotar a extensão em um único arquivo. Ele pode ser publicado no marketplace de extensões do Azure Data Studio ou compartilhado entre sua equipe ou comunidade. Para fazer isso, você precisa instalar outro pacote npm na linha de comando:

```console
`npm install -g vsce`
```

Edite o `README.md` como desejar, procure o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

Depois disso, o arquivo my test-notebook-0.0.1.vsix terá sido criado e estará pronto para ser instalado e compartilhado com o mundo.

## <a name="run-your-extension"></a>Executar a extensão

Para executar e testar a extensão, abra o Azure Data Studio e a paleta de comandos (`Ctrl + Shift + P`). Localize o comando **Extensões: Instalar por meio do VSIX** e procure a pasta que contém a nova extensão.

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="Instalar o VSIX":::

Agora ela será exibida no painel de extensões do Azure Data Studio. Abra a paleta de comandos novamente e você encontrará o novo comando que criamos com a extensão **Abrir Livro: Livro de Teste**. Após a execução, ele deve abrir o Jupyter Book que empacotamos com nossa extensão.

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Comando do notebook":::

Parabéns! Você criou e agora poderá enviar sua primeira extensão do Jupyter Notebook.

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio ainda não foi totalmente implementado. Para publicar a extensão, hospede o VSIX da extensão em algum lugar (por exemplo, uma página de Versão do GitHub) e envie uma PR atualizando [esse arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com as suas informações de extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão – Criar sua extensão de notebook
> - Criar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

Esperamos que, depois de ler isto, você se sinta inspirado a criar sua própria extensão para o Azure Data Studio.

Se você tiver uma ideia, mas não souber exatamente como começar, abra um problema ou envie um tweet para a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre pode consultar o [Guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview), pois ele abrange todas as APIs e padrões existentes.