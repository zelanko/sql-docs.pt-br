---
title: Como contribuir para a documentação do SQL Server | Microsoft Docs
ms.date: 08/13/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 3628c3b8e3e740beb93c5da744f0336a1409d167
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461061"
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

Você pode fazer edições simples no conteúdo do SQL Server em seu navegador e, em seguida, enviá-las à Microsoft. O processo completo é documentado no artigo [Visão geral do guia de colaborador do Microsoft Docs](https://docs.microsoft.com/contribute/#quick-edits-to-existing-documents). O seguinte vídeo mostra o processo de ponta a ponta para enviar as alterações ao seu navegador:

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE23pxh]

> [!TIP]
> Observe que o local do botão **Editar** é um pouco diferente do que é mostrado no vídeo, mas o processo é o mesmo.
>
> ![Botão Editar](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

## <a id="tools"></a> Editar localmente com ferramentas

Outra opção de edição é criar fork nos repositórios **sql-docs** ou **azure-docs** e cloná-los localmente para seu computador. Dessa forma, você poderá usar um editor de Markdown e um cliente git para enviar as alterações. Este fluxo de trabalho é bom para edições mais complexas ou que envolvem vários arquivos. Também é bom para colaboradores frequentes do docs.microsoft.com.

Para contribuir com esse método, consulte os seguintes artigos:

- [Criar uma conta do GitHub](https://docs.microsoft.com/contribute/get-started-setup-github)
- [Instalar as ferramentas de criação de conteúdo](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [Configurar um repositório Git localmente](https://docs.microsoft.com/contribute/get-started-setup-local)
- [Usar as ferramentas para colaborar](https://docs.microsoft.com/contribute/how-to-write-workflows-major)

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

- Para obter uma lista dos includes mais usados, veja [Versão do SQL Server e arquivos do include applies-to](applies-to-includes.md).
- Examine outros artigos que abordam o mesmo recurso ou uma tarefa relacionada. Se você editar esse artigo, poderá copiar o Markdown para o link do include applies-to (será possível cancelar a edição sem enviá-la).
- Pesquise no diretório [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) para arquivos que contém o texto “applies-to”. Você pode usar o botão **Localizar** no github filtrar rapidamente. Clique no arquivo para ver como ele é renderizado.
- Atente-se à convenção de nomenclatura. Se não houver letras x no nome, geralmente tratam-se de espaços reservados que indicam a falta de suporte para um serviço. Por exemplo, **appliesto-xx-xxxx-asdw-xxx-md.md** indica suporte apenas para o SQL Data Warehouse do Azure, porque somente **asdw** está escrito, enquanto os outros campos mostram letras x.
- Alguns deles incluem um número de versão específica, como **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**. Use esses includes somente se você conhecer o recurso que foi introduzido em uma versão específica do SQL Server.

## <a name="contributor-resources"></a>Recursos do colaborador

- [Guia do colaborador para docs.microsoft.com](https://docs.microsoft.com/contribute/)
- [Guia de Estilo da Microsoft](https://docs.microsoft.com/teamblog/style-guide)
- [Noções básicas de Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> Se você tiver comentários sobre o produto, em vez de comentários sobre a documentação, [deixe seus comentários sobre o produto SQL Server aqui](https://feedback.azure.com/forums/908035-sql-server).

## <a name="next-steps"></a>Próximas etapas

Explore o [repositório sql-docs](https://github.com/MicrosoftDocs/sql-docs) no GitHub.

Localize um artigo, envie uma alteração e ajude a comunidade do SQL Server. 

Obrigado.
