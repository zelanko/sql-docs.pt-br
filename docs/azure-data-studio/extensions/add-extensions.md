---
title: Adicionar extensões
description: Saiba como adicionar funcionalidade ao Azure Data Studio selecionando e instalando extensões entre as fornecidas pela Microsoft e por terceiros.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: ''
ms.date: 10/03/2019
ms.openlocfilehash: 2e2e76c436c02f2cbc5878228f1be2d57248816c
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123026"
---
# <a name="extend-the-functionality-of-azure-data-studio"></a>Estender a funcionalidade do Azure Data Studio

As extensões no Azure Data Studio fornecem uma forma fácil de adicionar mais funcionalidade à instalação básica do Azure Data Studio.

As extensões são fornecidas pela equipe do Azure Data Studio (Microsoft), bem como pela comunidade de terceiros (você!). Para obter mais informações sobre como criar extensões, confira [Criação de extensões](./extension-authoring.md).

## <a name="add-azure-data-studio-extensions"></a>Adicionar extensões do Azure Data Studio

1. Acesse as extensões disponíveis selecionando o ícone de extensões ou selecionando **Extensões** no menu **Exibição**. Você pode usar o comando **Exibir: Mostrar extensões**, disponível na **Paleta de Comandos** (F1 ou `Ctrl+Shift+P`).

    ![ícone do gerenciador de extensões](media/add-extensions/extension-manager-icon.png)

    Você também pode acessar rapidamente o gerenciador de extensões pressionando `Ctrl+Shift+X` (Windows/Linux) ou `Command+Shift+X` (Mac).

2. Selecione uma extensão disponível para exibir os detalhes.

    ![detalhes da extensão](media/add-extensions/extension-details.png)

3. Selecione a extensão que você deseja e **Instale**-a.

4. Após a instalação, clique em **Recarregar** para habilitar a extensão no Azure Data Studio (necessário somente ao instalar uma extensão pela primeira vez).

Se você estiver com problemas para acessar o Gerenciador de extensões no Azure Data Studio, poderá baixar a extensão necessária em nosso [Wiki no GitHub](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions).

## <a name="manage-extensions"></a>Gerenciar extensões

### <a name="list-installed-extensions"></a>Listar extensões instaladas

A exibição Extensões padrão mostra as extensões que estão habilitadas, todas as extensões recomendadas para você e um contêiner recolhido com todas as extensões desabilitadas. O comando **Extensões: Mostrar extensões instaladas**, disponível na **Paleta de Comandos** ou no menu suspenso **Mais Ações** `(...)`, mostra uma lista de todas as extensões instaladas, incluindo as extensões desabilitadas.

### <a name="uninstall-an-extension"></a>Desinstalar uma extensão

Para desinstalar uma extensão, clique no ícone de engrenagem à direita de uma entrada de extensão e escolha **Desinstalar** no menu suspenso. Isso desinstalará a extensão selecionada e solicitará que você recarregue o Azure Data Studio.

 ![menu suspenso de extensão](media/add-extensions/extension-gear-dropdown.png)

### <a name="disable-an-extension"></a>Desabilitar uma extensão

Você pode desabilitar temporariamente uma extensão em vez de removê-la permanentemente. É possível desabilitar a extensão em todas as sessões do Azure Data Studio (**Desabilitar**) ou apenas no workspace atual (**Desabilitar (Workspace)** ). Também é possível desabilitar todas as extensões instaladas por meio **Paleta de Comandos** usando os comandos **Extensões: Desabilitar todas as extensões** e **Extensões: Desabilitar todas as extensões (Workspace)** .

### <a name="enable-an-extension"></a>Habilitar uma extensão

Se uma extensão tiver sido desabilitada, ela estará na seção **Desabilitada** da lista de extensões e será marcada como ***Desabilitada***. Você pode habilitá-la novamente usando os comandos **Habilitar** ou **Habilitar (Workspace)** no menu suspenso. A **Paleta de Comandos** também permite habilitar todas as extensões usando os comandos **Extensões: Habilitar todas as extensões** e **Extensões: Habilitar todas as extensões (Workspace)** .

![habilitando extensão](media/add-extensions/extensions-enable.png)

### <a name="updating-an-extension"></a>Atualizar uma extensão

O Azure Data Studio verifica automaticamente e instala atualizações de todas as extensões instaladas. Se quiser desativar o recurso de atualização automática, você poderá desabilitar a atualização automática com o comando **Extensões: Desabilitar extensões com atualização automática**.

Para atualizar manualmente uma extensão, você pode verificar se há atualizações dela usando o comando **Extensões: Mostrar extensões desatualizadas**, que pesquisa em sua lista de extensões usando o filtro `@outdated`. Isso mostrará todas as atualizações disponíveis para todas as extensões instaladas. Clique no botão **Atualizar** de uma extensão desatualizada e a atualização será instalada. Em seguida, você será solicitado a recarregar o Azure Data Studio. Você também pode atualizar todas as suas extensões desatualizadas simultaneamente com o comando **Extensões: Atualizar todas as extensões**.

O comando **Extensões: Verificar se há atualizações de extensões** é outra maneira de verificar quais extensões têm atualizações disponíveis.

## <a name="install-from-a-vsix"></a>Instalar de um VSIX

Você pode instalar manualmente uma extensão do Azure Data Studio empacotada em um arquivo `.vsix` usando o comando **Instalar do VSIX** na lista suspensa de comandos da exibição Extensões ou usando o comando **Extensões: Instalar do VSIX** na Paleta de Comandos e apontando para o arquivo `.vsix` da extensão.

## <a name="access-installed-azure-data-studio-extensions"></a>Acessar as extensões instaladas do Azure Data Studio

Cada extensão aprimora sua experiência no Azure Data Studio de uma maneira diferente. Como resultado, o ponto de entrada para extensões pode variar. Veja a documentação individual da extensão instalada para obter informações sobre como seus recursos podem ser acessados após a instalação.

## <a name="extensions-view-filters"></a>Filtros de exibição de extensões

A caixa de pesquisa de exibição Extensões dá suporte a filtros que ajudam você a localizar e gerenciar extensões. Os comandos **Mostrar extensões instaladas** e **Mostrar extensões recomendadas** usam filtros como `@installed` e `@recommended` na caixa de pesquisa.

Você pode ver uma lista completa de todos os filtros e classificar os comandos digitando @ na caixa de pesquisa de extensões e navegando pelas sugestões:

![classificação de extensão](media/add-extensions/extension-sort.png)

Estes são os filtros da exibição Extensões:

- `@builtin` – Mostrar extensões fornecidas com o Azure Data Studio. Agrupado por tipo (linguagens de programação, temas etc.).
- `@disabled` – Mostrar as extensões instaladas desabilitadas.
- `@enabled` – Mostrar as extensões instaladas habilitadas. As extensões podem ser habilitadas/desabilitadas individualmente.
- `@installed` – Mostrar extensões instaladas.
- `@outdated` – Mostrar extensões instaladas desatualizadas. Uma versão mais recente está disponível no Marketplace.
- `@recommended` – Mostrar extensões recomendadas. Agrupadas como específicas do Workspace ou de uso geral.
- `@category` – Mostrar extensões que pertencem à categoria especificada. Abaixo estão algumas categorias com suporte. Para obter uma lista completa, digite @category e siga as opções na lista de sugestões:
    - `@category:themes`
    - `@category:formatters`
    - `@category:snippets` Esses filtros também podem ser combinados. Por exemplo, `@installed @category:themes` exibe todos os temas instalados.

Se nenhum filtro for fornecido, a exibição Extensões exibirá as extensões instaladas e recomendadas.

### <a name="sorting"></a>Classificação

Você pode classificar as extensões com o filtro `@sort`, que pode usar os seguintes valores:

- `installs` – Classificar por contagem de instalações da galeria de extensões, em ordem decrescente.
- `rating` – Classificar por classificação na galeria de extensões (1 a 5 estrelas), em ordem decrescente.
- `name` – Classificar em ordem alfabética pelo nome da extensão.

## <a name="common-questions"></a>Perguntas comuns

### <a name="where-are-extensions-installed"></a>Onde as extensões são instaladas?

As extensões são instaladas em uma pasta de extensões por usuário. Dependendo da plataforma, o local é a seguinte pasta:

- Windows `%USERPROFILE%\.azuredatastudio\extensions`
- macOS `~/.azuredatastudio/extensions`
- Linux `~/.azuredatastudio/extensions`
