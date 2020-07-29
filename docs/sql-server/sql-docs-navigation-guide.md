---
title: Dicas de navegação de documentos do SQL Server
description: Dicas e truques para navegar na documentação técnica do SQL Server – explica coisas como a página de hub, o sumário, o cabeçalho e como usar as trilhas de navegação e o filtro de versão.
ms.date: 10/15/2019
ms.prod: sql
ms.technology: release-landing
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: f85c97e36900d3c6f4372004819690a8ede49d22
ms.sourcegitcommit: 903856818acc657e5c42faa16d1c770aeb4e1d1b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83731596"
---
# <a name="sql-server-docs-navigation-guide"></a>Guia de navegação de documentos do SQL Server 

Este tópico fornece algumas dicas e truques para navegar no espaço da documentação técnica do SQL Server.  

## <a name="hub-page"></a>Página de hub

A página de hub do SQL Server pode ser encontrada em [https://aka.ms/sqldocs](https://aka.ms/sqldocs) e é o ponto de entrada para localizar conteúdo relevante sobre o SQL Server.

Você sempre pode navegar de volta para esta página selecionando **Documentos do SQL** no cabeçalho na parte superior de todas as páginas do conjunto da documentação técnica do SQL Server: 

![Documentos do SQL no cabeçalho](media/sql-server-docs-navigation-guide/sql-docs-in-header.png)

## <a name="offline-documentation"></a>Documentação offline

Se você deseja exibir a documentação do SQL Server em um sistema offline, há duas opções para fazer isso. Você pode criar um PDF sempre que estiver na documentação técnica do SQL Server ou pode baixar o conteúdo offline usando [Visualizador da Ajuda offline do SQL Server](sql-server-help-installation.md). 

Se quiser criar um PDF, selecione o link **Baixar PDF** localizado na parte inferior de cada sumário.


![Baixar PDF](media/sql-server-docs-navigation-guide/download-pdf.png)

## <a name="toc-symbols"></a>Símbolos de sumário 

Entradas no sumário que têm um `>` no final indicam que você será levado para a documentação técnica com um sumário diferente. 

![Carrots únicos no sumário](media/sql-server-docs-navigation-guide/single-carrots-in-sql-docs-toc.png)

Entradas no sumário que têm um `>>` indicam que você será levado para fora de docs.microsoft.com. 

![Marcadores de navegação no sumário](media/sql-server-docs-navigation-guide/double-carrots-in-sql-docs-toc.png)

Se navegar para uma dessas páginas, você poderá voltar para a página técnica principal do SQL Server e ao sumário selecionando a entrada "Bem-vindo ao SQL Server >" encontrada na parte superior de cada um desses sumários. 

![Navegar de volta para o sumário do SQL](media/sql-server-docs-navigation-guide/navigate-back-to-sql-toc.png)

## <a name="toc-search"></a>Pesquisa de sumário 
Em docs.microsoft.com, você pode pesquisar o conteúdo no sumário usando a caixa de pesquisa de filtro na parte superior: 

![Usar caixa de filtro](media/sql-server-docs-navigation-guide/sql-docs-toc-filter.gif)

## <a name="version-filter"></a>Filtro da versão
A documentação técnica do SQL Server fornece conteúdo sobre várias versões e tipos de SQL Server com suporte. Os recursos podem variar entre as versões e os tipos do SQL Server e, às vezes, o próprio conteúdo pode variar. 

Você pode usar o [filtro de versão](versioning-system-monikers-ui-sql-server.md) para garantir que está esteja vendo o conteúdo referente à versão e ao tipo corretos do SQL Server: 

![Filtro de versão dos documentos do SQL](media/sql-server-docs-navigation-guide/sql-docs-version-filter.gif)

Selecionar **Todo o SQL** \> **Não ocultar nada** garante que todo o conteúdo fique visível e nada fique oculto pelo filtro de versão. A opção **Não ocultar nada** pode revelar conteúdo relevante para várias versões diferentes do SQL Server no mesmo artigo, o que pode ser contraditório, incerto ou confuso. Sendo assim, a opção [**Não ocultar nada** não é recomendada para uso de rotina](versioning-system-monikers-ui-sql-server.md#anchor-allsql-hidenothing). 

## <a name="breadcrumbs"></a>Trilhas de navegação

As trilhas de navegação podem ser encontradas abaixo do cabeçalho e acima do sumário e indicam onde o artigo atual está localizado no sumário.  Isso não apenas ajuda a definir o contexto do tipo de conteúdo que você está lendo, mas também permite navegar de volta para a árvore de sumário:

![Trilhas de navegação dos documentos do SQL](media/sql-server-docs-navigation-guide/sql-docs-bread-crumbs.gif)

## <a name="article-section-navigation"></a>Navegação de seção do artigo

O painel de navegação à direita permite navegar rapidamente para as seções dentro de um artigo, bem como identificar onde você está no artigo.  

![Navegação à direita](media/sql-server-docs-navigation-guide/sql-docs-right-hand-navigation.gif)


## <a name="submit-docs-feedback"></a>Enviar comentários sobre documentos

Se encontrar algum erro em um artigo, você poderá enviar comentários à equipe de Conteúdo do SQL responsável pelo artigo rolando até a parte inferior da página e selecionando **Comentários sobre o conteúdo**.

![Comentários sobre o conteúdo do Problema do Git](media/sql-server-get-help/git-issues.png)

Também é possível enviar comentários e sugestões sobre a documentação geral em [https://aka.ms/sqldocsfeedback](https://aka.ms/sqldocsfeedback). 

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![Editar documentos do SQL](media/sql-server-docs-navigation-guide/edit-sql-docs.gif)

## <a name="next-steps"></a>Próximas etapas

- Introdução à [Documentação Técnica do SQL Server](index.yml).
- Para saber mais sobre como enviar comentários ou obter ajuda com o SQL Server, consulte a página [Obter ajuda](sql-server-get-help.md). 
- Para acessar rapidamente todos os guias de início rápido e tutoriais, confira [Recursos educativos do SQL](../sql-server/educational-sql-resources.yml).
