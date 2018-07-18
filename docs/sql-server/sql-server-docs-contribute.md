---
title: Como contribuir para a documentação do SQL Server | Microsoft Docs
ms.date: 04/12/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 52bc0371c7f60b7b6fcff5c64c5972d7a178b629
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926527"
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>Como contribuir para a documentação do SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Qualquer pessoa pode contribuir para a documentação do SQL Server. Isso inclui corrigir erros de digitação, sugerir melhores explicações e melhorar a precisão técnica. Este artigo explica como começar com as contribuições de conteúdo e como o processo funciona.

Há dois fluxos de trabalho principais que você pode usar para contribuir:

|||
|---|---|
| [Editar no navegador](#githubui) | Bom para edições simples e breves de qualquer artigo. |
| [Editar localmente com ferramentas](#tools) | Bom para edições mais complexas, edições que envolvem vários artigos e contribuições frequentes para docs.microsoft.com. |

## <a id="githubui"></a> Editar no navegador

As etapas a seguir fornecem uma visão geral de como fazer edições simples no conteúdo do SQL Server no navegador. O processo completo é documentado no artigo [Fluxo de trabalho de contribuição do GitHub para alterações pequenas ou raras](https://docs.microsoft.com/contribute/light-workflow).

1. Cada artigo, inclusive este, tem um botão **Editar** à direita. Encontre um artigo que você deseja alterar e clique no botão **Editar** para começar.

   ![Botão Editar para o artigo do SQL](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   Todo o conteúdo em docs.microsoft.com é gerenciado em vários Repositórios do GitHub. Ao clicar no botão Editar, você será direcionado para o artigo no repositório **sql-docs**. Ou então, se estiver editando um artigo do SQL na documentação do Azure, você será direcionado para o repositório **azure-docs**. 

1. Em seguida, clique no ícone de lápis na parte superior direita do artigo no GitHub.

   ![Botão Editar](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > É necessário estar conectado ao GitHub para editar um artigo. Se você não tiver uma conta do GitHub, consulte [Configuração de conta do GitHub](https://docs.microsoft.com/contribute/get-started-setup-github). Depois de criar uma nova conta, também será necessário confirmar seu endereço de email no GitHub antes que você possa editar.

1. Editar o artigo no navegador. Todos os artigos são escritos em Markdown. Se você precisar de ajuda com o Markdown, revise as [Noções básicas de Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/). Você também pode aprender observando como os artigos publicados renderizam o Markdown existente.

1. Role para baixo até a parte inferior da janela de edição, digite um título para a alteração e clique no botão **Propor alteração de arquivo**.

   ![Propor solicitação de pull](./media/sql-server-docs-contribute/propose-file-change.png)

1. Na próxima página, clique em **Criar solicitação de pull**.

   ![Criar solicitação de pull](./media/sql-server-docs-contribute/create-pull-request.png)

1. Digite um título e uma descrição para a solicitação de pull. Em seguida, clique em **Criar solicitação de pull** novamente.

   ![Criar solicitação de pull](./media/sql-server-docs-contribute/create-pull-request2.png)

Neste ponto, você deverá ser guiado pelo resto do processo nos comentários da solicitação de pull. O processo completo e detalhes adicionais podem ser encontrados no [guia do colaborador](https://docs.microsoft.com/contribute/light-workflow).

## <a id="tools"></a> Editar localmente com ferramentas

Outra opção de edição é criar fork nos repositórios **sql-docs** ou **azure-docs** e cloná-los localmente para seu computador. Dessa forma, você poderá usar um editor de Markdown e um cliente git para enviar as alterações. Este fluxo de trabalho é bom para edições mais complexas ou que envolvem vários arquivos. Também é bom para colaboradores frequentes do docs.microsoft.com.

Para contribuir com esse método, consulte os seguintes artigos:

- [Criar uma conta do GitHub](https://docs.microsoft.com/contribute/get-started-setup-github)
- [Instalar as ferramentas de criação de conteúdo](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [Configurar um repositório Git localmente](https://docs.microsoft.com/contribute/get-started-setup-local)
- [Usar as ferramentas para colaborar](https://docs.microsoft.com/contribute/how-to-write-workflows-majo)

Se enviar uma solicitação de pull com alterações significativas na documentação, você receberá um comentário no GitHub solicitando o envio de um **CLA (contrato de licença de contribuição)** online. É necessário preencher o formulário online para que sua solicitação de pull seja aceita.

## <a name="recognition"></a>Reconhecimento

Se as alterações forem aceitas, você será reconhecido como um colaborador na parte superior do artigo.

![Reconhecimento de contribuição de conteúdo](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>Visão geral de sql-docs

Esta seção fornece algumas diretrizes adicionais sobre como trabalhar no repositório **sql-docs**.

> [!IMPORTANT]
> As informações nesta seção são específicas para o **sql-docs**. Se você estiver editando um artigo do SQL na documentação do Azure, veja [o Leiame do repositório azure-docs no GitHub](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md).

O repositório [sql-docs](https://github.com/MicrosoftDocs/sql-docs) usa várias pastas padrão para organizar o conteúdo.

| Pasta | Descrição |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | Contém todo o conteúdo publicado do SQL Server. As subpastas organizam logicamente as diferentes áreas do conteúdo. |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | Contém arquivos include. Esses arquivos são blocos de conteúdo que pode ser incluído em um ou mais tópicos. |
| **./media** | Cada pasta pode ter uma subpasta **media** para imagens do artigo. A pasta **media**, por sua vez, tem subpastas com o mesmo nome que os tópicos nos quais a imagem aparece. As imagens devem ser arquivos .png com todas as letras minúsculas e sem espaços. |
| **TOC.MD** | Um arquivo de índice. Cada subpasta tem a opção de usar um arquivo TOC.MD. |

#### <a name="applies-to-includes"></a>Includes Applies-to

Cada artigo do SQL Server contém um arquivo include **applies-to** após o título. Isso indica a quais áreas ou versões do SQL Server o artigo se aplica.

Considere o seguinte exemplo de Markdown que efetua pull no arquivo include **appliesto-ss-asdb-asdw-pdw-md.md**.

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

Isso adiciona o seguinte texto à parte superior do artigo:

![Texto do Applies to](./media/sql-server-docs-contribute/applies-to.png)

Para encontrar o include applies-to correto para o artigo, use as dicas a seguir:

- Examine outros artigos que abordam o mesmo recurso ou uma tarefa relacionada. Se você editar esse artigo, poderá copiar o Markdown para o link do include applies-to (será possível cancelar a edição sem enviá-la).
- Pesquise no diretório [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) para arquivos que contém o texto “applies-to”. Você pode usar o botão **Localizar** no github filtrar rapidamente. Clique no arquivo para ver como ele é renderizado.
- Atente-se à convenção de nomenclatura. Se não houver letras x no nome, geralmente tratam-se de espaços reservados que indicam a falta de suporte para um serviço. Por exemplo, **appliesto-xx-xxxx-asdw-xxx-md.md** indica suporte apenas para o SQL Data Warehouse do Azure, porque somente **asdw** está escrito, enquanto os outros campos mostram letras x.
- Alguns deles incluem um número de versão específica, como **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**. Use esses includes somente se você conhecer o recurso que foi introduzido em uma versão específica do SQL Server. 

## <a name="contributor-resources"></a>Recursos do colaborador

- [Guia do colaborador para docs.microsoft.com](https://docs.microsoft.com/en-us/contribute/)
- [Guia de Estilo da Microsoft](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Noções básicas de Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> Se você tiver comentários sobre o produto, em vez de comentários sobre a documentação, [deixe seus comentários sobre o produto SQL Server aqui](https://feedback.azure.com/forums/908035-sql-server).

## <a name="next-steps"></a>Próximas etapas

Explore o [repositório sql-docs](https://github.com/MicrosoftDocs/sql-docs) no GitHub.

Localize um artigo, envie uma alteração e ajude a comunidade do SQL Server. 

Obrigado.