---
title: Criar uma extensão do Jupyter Book
description: Saiba mais sobre como empacotar um Jupyter Book em uma extensão usando o gerador de extensão
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: af6cb013109d5d871c709f72cf5a564ae69940cb
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288168"
---
# <a name="create-a-jupyter-book-extension"></a>Criar uma extensão do Jupyter Book

Este tutorial demonstra como criar uma extensão do Jupyter Book no Azure Data Studio. A extensão fornece um exemplo de Jupyter Book que pode ser aberto e executado no Azure Data Studio. 

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão
> - Criar sua extensão do Jupyter Book
> - Executar a extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

## <a name="apis-used"></a>APIs usadas

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>Casos de uso da extensão

Há algumas razões diferentes para criaria uma extensão do Jupyter Book:

- Compartilhar uma documentação interativa, organizada e dividida em seções
- Compartilhar um livro inteiro (semelhante a um livro eletrônico, mas distribuído por meio do Azure Data Studio)
- Controlar a versão e as atualizações do Jupyter Book

A principal diferença entre um Jupyter Book e uma extensão de notebook é que um Jupyter Book oferece organização. Dezenas de notebooks podem ser divididos em diferentes capítulos de um livro, mas a extensão de notebooks pretende fornecer um pequeno número de notebooks individuais.

## <a name="prerequisites"></a>Pré-requisitos

O Azure Data Studio se baseia na mesma estrutura que o Visual Studio Code, portanto, as extensões para o Azure Data Studio são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- O [Node.js](https://nodejs.org) instalado e disponível em seu `$PATH`. O Node.js inclui o [npm](https://www.npmjs.com/), o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.
- O [Visual Studio Code](https://code.visualstudio.com), para fazer alterações na extensão e depurá-la.
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção `Add to Path` em setup.exe. Para Mac ou Linux, execute o *Comando instalar 'azuredatastudio' no caminho*.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://www.npmjs.com/package/generator-azuredatastudio) usando o Yeoman. Para instalá-lo, execute o seguinte comando no prompt de comando:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>Criar sua extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novo Jupyter Book** na lista de tipos de extensão:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="gerador de extensão":::

3. Siga as etapas para preencher o nome da extensão (neste tutorial, use **Livro de Teste**), um nome de fornecedor (neste tutorial, use **Microsoft**) e adicione uma descrição.

Opte por fornecer um Jupyter Book existente, usar um livro de exemplo fornecido ou trabalhar para criar um Jupyter Book. As três opções são mostradas abaixo.

### <a name="providing-an-existing-book"></a>Como fornecer um livro existente

Caso deseje enviar um livro já criado, forneça o caminho absoluto do arquivo para a pasta em que reside o conteúdo do livro. Depois, você estará pronto para continuar aprendendo sobre a extensão e como enviá-la.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="Livro existente":::

### <a name="using-the-sample-book"></a>Como usar o livro de exemplo

Caso você não tenha notebooks existentes, use o exemplo fornecido no gerador.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="Jupyter Book de exemplo":::

O livro de exemplo demonstra a aparência de um Jupyter Book simples. Caso deseje saber mais sobre como personalizar um Jupyter Book, confira a seção a seguir sobre como criar um livro com notebooks existentes.

### <a name="creating-a-new-book"></a>Como criar um livro

Caso você tenha notebooks que deseja empacotar em um Jupyter Book, faça isso. O gerador pergunta se você deseja usar capítulos no livro e, em caso afirmativo, quantos e os respectivos títulos. Veja qual é a aparência do processo de seleção abaixo. Use a barra de espaço para selecionar os notebooks que deseja inserir em cada capítulo.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="Criar um Jupyter Book":::

A conclusão das etapas anteriores cria uma pasta com o novo Jupyter Book. Abra a pasta no Visual Studio Code e você estará pronto para enviar sua extensão do Jupyter Book.

## <a name="understanding-your-extension"></a>Noções básicas sobre a extensão

É esta a aparência que o projeto deverá ter:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="Estrutura do arquivo de extensão":::

O `vsc-extension-quickstart.md` fornece uma referência dos arquivos importantes. O `README.md` é o arquivo em que você pode fornecer a documentação da nova extensão. Observe os arquivos `package.json`, `jupyter-book.ts`, `content` e `toc.yml`. A pasta `content` contém todos os arquivos de notebook ou markdown. O `toc.yml` estrutura o Jupyter Book e é gerado automaticamente se você optou por criar um Jupyter Book personalizado por meio do gerador de extensão.

Se você criar um livro usando o gerador e optar por incluir capítulos no livro, a estrutura de pastas será um pouco diferente. Em vez de os arquivos de markdown e do Jupyter Notebook residirem na pasta `content`, haverá subpastas que correspondem aos títulos que você escolheu para os capítulos. 

Se houver arquivos ou pastas que você não deseja publicar, inclua os nomes deles no arquivo `.vscodeignore`.

Vamos dar uma olhada em `jupyter-book.ts` para entender o que a extensão recém-formada faz.

```javascript
// This function is called when you run the command `Launch Book: Test Book` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command
}
```

A função `activate` é a ação principal da extensão. Todos os comandos que você deseja registrar devem ser exibidos dentro da função `activate`, semelhante ao comando `launchBook.test-book`. Dentro da função `processNotebooks`, encontramos a pasta de extensão que contém o Jupyter Book e chamamos `bookTreeView.openBook` usando a pasta da extensão como um parâmetro. 

O arquivo `package.json` também desempenha um papel importante no registro do comando da extensão:

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

O evento de ativação, `onCommand`, dispara a função que registramos quando invocamos o comando. Há alguns outros eventos de ativação que são possíveis para personalização adicional. Para obter mais informações, confira [Eventos de ativação](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar a extensão com outras pessoas, você precisará empacotá-la em um só arquivo. Isso pode ser publicado no Marketplace de extensões do Azure Data Studio ou compartilhado entre a sua equipe ou sua comunidade. Para fazer isso, você precisa instalar outro pacote npm na linha de comando:

```console
`npm install -g vsce`
```

Edite o `README.md` como desejar, procure o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

Depois que essas linhas forem adicionadas, o arquivo my test-book-0.0.1.vsix terá sido criado e estará pronto para ser instalado no Azure Data Studio.

## <a name="run-your-extension"></a>Executar a extensão

Para executar e testar a extensão, abra o Azure Data Studio e a paleta de comandos (`Ctrl + Shift + P`). Localize o comando **Extensões: Instalar por meio do VSIX** e procure a pasta que contém a nova extensão. Agora ela será exibida no painel de extensões do Azure Data Studio.

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="Instalar o VSIX":::

Abra a paleta de comandos novamente e localize o comando que registramos, **Abrir Livro:** Testar Notebook. Após a execução, ele deve abrir o Jupyter Book que empacotamos com nossa extensão.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="Comando do notebook":::

Parabéns! Você criou sua primeira extensão do Jupyter Book e agora poderá enviá-la. Para obter mais informações sobre os Jupyter Books, confira [Livros com o Jupyter](https://jupyterbook.org/intro.html).

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no Marketplace

O Marketplace de extensões do Azure Data Studio ainda não foi totalmente implementado. Para publicar a extensão, hospede o VSIX da extensão em algum lugar (por exemplo, uma página de Versão do GitHub) e envie uma PR atualizando [esse arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com as suas informações de extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Criar um projeto de extensão
> - Instalar o gerador de extensão
> - Criar sua extensão do Jupyter Book
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

Esperamos que, depois de ler este artigo, você tenha ideias sobre Jupyter Books que deseja compartilhar com a comunidade do Azure Data Studio. 

Caso tenha uma ideia, mas não saiba exatamente como começar a desenvolvê-la, abra um problema ou envie um tweet para a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre pode consultar o [Guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview), pois ele abrange todas as APIs e padrões existentes.
