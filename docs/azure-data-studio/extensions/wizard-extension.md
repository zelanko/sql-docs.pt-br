---
title: Criar uma extensão de assistente
description: Este tutorial demonstra como criar uma extensão de assistente para adicionar uma funcionalidade personalizada ao Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 50440aca120dad6cfd165262bd4bfd2e139393cf
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364053"
---
# <a name="create-an-azure-data-studio-wizard-extension"></a>Criar uma extensão de assistente do Azure Data Studio

Este tutorial demonstra como criar uma **extensão de assistente do Azure Data Studio**. A extensão contribui com um assistente para interagir com os usuários no Azure Data Studio.

Neste artigo, você aprenderá a:
> [!div class="checklist"]
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Adicionar um assistente personalizado à extensão
> - Testar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

## <a name="prerequisites"></a>Pré-requisitos

O Azure Data Studio se baseia na mesma estrutura que o Visual Studio Code, portanto, as extensões para o Azure Data Studio são criadas usando o Visual Studio Code. Para começar, você precisa dos seguintes componentes:

- O [Node.js](https://nodejs.org) instalado e disponível em seu `$PATH`. O Node.js inclui o [npm](https://www.npmjs.com/), o Gerenciador de Pacotes do Node.js, que é usado para instalar o gerador de extensão.
- O [Visual Studio Code](https://code.visualstudio.com) para depurar a extensão.
- A [Extensão de depuração](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) do Azure Data Studio (opcional). Ela permite testar sua extensão sem a necessidade de empacotar e instalá-la no Azure Data Studio.
- Certifique-se de que `azuredatastudio` está em seu caminho. Para o Windows, escolha a opção `Add to Path` em setup.exe. Para Mac ou Linux, execute o *Comando instalar 'azuredatastudio' no caminho*.

## <a name="install-the-extension-generator"></a>Instalar o gerador de extensão

Para simplificar o processo de criação de extensões, criamos um [gerador de extensão](https://code.visualstudio.com/docs/extensions/yocode) usando o Yeoman. Para instalá-lo, execute o seguinte no prompt de comando:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-wizard-extension"></a>Criar sua extensão de assistente

### <a name="introduction-to-wizards"></a>Introdução aos assistentes

Os assistentes são um tipo de interface do usuário que apresenta páginas passo a passo para os usuários preencherem, a fim de realizar uma tarefa. Exemplos comuns incluem assistentes de instalação de software e assistentes de solução de problemas. Por exemplo:

:::image type="content" source="media/wizard-extension/dacpac-wizard.gif" alt-text="Assistente do DACPAC":::

Como os assistentes costumam ser úteis ao trabalhar com os dados e estender a funcionalidade do Azure Data Studio, o Azure Data Studio oferece APIs para criar seus assistentes personalizados. Veremos como gerar um modelo de assistente e modificá-lo para criar seu assistente personalizado.

### <a name="run-the-extension-generator"></a>Executar o gerador de extensão

Para criar uma extensão:

1. Inicie o gerador de extensão com o seguinte comando:

   `yo azuredatastudio`

2. Escolha **Novo Assistente ou Nova Caixa de Diálogo** na lista de tipos de extensão. Em seguida, selecione **Assistente** seguido de **Modelo de Introdução**

3. Siga as etapas para preencher o nome da extensão (neste tutorial, use **Minha Extensão de Teste**) e adicione uma descrição.

    :::image type="content" source="media/wizard-extension/extension-generator.png" alt-text="Gerador de extensão":::

Seguir as etapas anteriores cria uma nova pasta. Abra a pasta no Visual Studio Code e você estará pronto para criar sua extensão de assistente.

### <a name="run-the-extension"></a>Executar a extensão

Vamos ver o que o modelo de assistente nos oferece executando a extensão. Antes da execução, verifique se a **extensão de Depuração do Azure Data Studio** está instalada no Visual Studio Code.

Selecione **F5** no VS Code para iniciar o Azure Data Studio no modo de depuração com a extensão em execução. Em seguida, no Azure Data Studio, execute o comando **Iniciar Assistente** na paleta de comandos (CTRL + SHIFT + P) na nova janela. Isso iniciará o assistente padrão com o qual esta extensão contribui:

:::image type="content" source="media/wizard-extension/wizard-template.gif" alt-text="Modelo de assistente":::

Em seguida, veremos como modificar esse assistente padrão.

### <a name="develop-the-wizard"></a>Desenvolver o assistente

Os arquivos mais importantes para começar a usar o desenvolvimento de extensões são `package.json`, `src/main.ts` e `vsc-extension-quickstart.md`:

- `package.json`: esse é o arquivo de manifesto, no qual o comando **Iniciar Assistente** é registrado. Ele também é o local em que `main.ts` é declarado o ponto de entrada do programa principal.
- `main.ts`: contém o código usado para adicionar elementos de interface do usuário ao assistente, como páginas, texto e botões
- `vsc-extension-quickstart.md`: contém a documentação técnica que pode ser uma referência útil durante o desenvolvimento

Vamos fazer uma alteração no assistente: adicionaremos uma quarta página em branco. Modifique `src/main.ts` conforme mostrado abaixo e verá uma página adicional ser exibida ao iniciar o assistente.

:::image type="content" source="media/wizard-extension/wizard-main.png" alt-text="Página principal do assistente":::
Quando você estiver familiarizado com o modelo, experimente mais estas ideias:

- Adicionar um botão com uma largura igual a 300 à nova página
- Adicionar um componente flexível no qual o botão será colocado
- Adicionar uma ação ao botão. Por exemplo, quando o botão receber um clique, inicie uma caixa de diálogo de abertura de arquivo ou abra um editor de consultas.

## <a name="package-your-extension"></a>Empacotar sua extensão

Para compartilhar com outras pessoas, você precisa empacotar a extensão em um único arquivo. Ele pode ser publicado no marketplace de extensões do Azure Data Studio ou compartilhado entre sua equipe ou comunidade. Para fazer isso, você precisa instalar outro pacote npm na linha de comando:

```console
npm install -g vsce`
```

Edite o `README.md` como desejar, procure o diretório base da extensão e execute `vsce package`. Opcionalmente, você pode vincular um repositório com a extensão ou continuar sem um. Para adicionar um, adicione uma linha semelhante ao arquivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

Depois que essas linhas forem adicionadas, um arquivo my-test-extension-0.0.1.vsix terá sido criado e estará pronto para ser instalado no Azure Data Studio.

:::image type="content" source="media/wizard-extension/install-vsix.png" alt-text="Instalar o VSIX":::

## <a name="publish-your-extension-to-the-marketplace"></a>Publicar sua extensão no marketplace

O marketplace de extensões do Azure Data Studio ainda não está totalmente implementado, mas o processo atual é hospedar o VSIX da extensão em algum lugar (por exemplo, uma página de Versão do GitHub) e enviar uma PR atualizando [este arquivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) com as informações de sua extensão.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> - Instalar o gerador de extensão
> - Criar sua extensão
> - Adicionar um assistente personalizado à extensão
> - Testar sua extensão
> - Empacotar sua extensão
> - Publicar sua extensão no marketplace

Esperamos que, depois de ler isto, você se sinta inspirado a criar sua própria extensão para o Azure Data Studio. Temos suporte para Insights do Painel (grafos bonitos que são executados em seu SQL Server), várias APIs específicas do SQL e um grande conjunto de pontos de extensão herdados do Visual Studio Code.

Se você tiver uma ideia, mas não souber exatamente como começar, abra um problema ou envie um tweet para a equipe: [azuredatastudio](https://twitter.com/azuredatastudio).

Você sempre pode consultar o [Guia de extensão do Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview), pois ele abrange todas as APIs e padrões existentes.

Para saber como trabalhar com T-SQL no Azure Data Studio, conclua o tutorial do Editor de T-SQL:

> [!div class="nextstepaction"]
> [Usar o editor de Transact-SQL para criar objetos de banco de dados](../tutorial-sql-editor.md)
