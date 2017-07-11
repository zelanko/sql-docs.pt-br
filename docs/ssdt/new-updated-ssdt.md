---
title: "Atualizado – documentos do SSDT para SQL Server | Microsoft Docs"
description: "Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para SSDT (SQL Server Data Tools) para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 06/30/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 5e43cb76dac922b3c43318b2a9f539ab19ec7bfe
ms.contentlocale: pt-br
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-sql-server-data-tools-ssdt" class="xliff"></a>

# Novos e atualizados recentemente: SSDT (SQL Server Data Tools)



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **17-05-2017** &nbsp; até &nbsp; **30-06-2017**
- *Área de assunto:* &nbsp; **SSDT (SQL Server Data Tools)**.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


*Não existem novos artigos a serem listados, no momento.*



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd" class="xliff"></a>

### 1. &nbsp; [Log de alterações do SSDT (SQL Server Data Tools)](changelog-for-sql-server-data-tools-ssdt.md)

*Atualizado: 19-05-2017* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 21.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cf17883ce0daf75fdf88881171bf4042558b1cf4 536fe0fe41b023a4186f494a509fa14fcbafccf4  (PR=1777  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



Para obter posts detalhados sobre as novidades e alterações, visite [o blog da equipe do SSDT](https://blogs.msdn.microsoft.com/ssdt/)

**SSDT 17.1**

Número da compilação: 14.0.61705.170

**Novidades**

**Projetos do AS:**
- Os usuários podem definir a codificação de dicas de colunas na interface do usuário em modelos de 1400
- O IntelliSense não relacionados ao modelo agora está disponível no modo offline
- Gerenciador de modelos de tabela agora contém um nó para representar nomeadas expressões M disponíveis no modelo (modelos de tabela do nível de compatibilidade 1400)
- Azure Active Directory seletor de pessoas semelhante ao IAM do Portal do Microsoft Azure agora disponível ao configurar os membros da função em modelos de tabela

**Projetos de bancos de dados:**
- Atualizado para DacFx 17.1

**Correções de Bugs**

- Corrigido um problema em que o nome do grupo de Designers do Business Intelligence foi exibido incorretamente em Opções do Visual Studio em VS2017
- Corrigido um problema em que uma falha pode ocorrer a geração de um mapa de código para uma solução com um projeto de relatório ou como o projeto
- Um número fixo de problemas com a integração de PowerQuery para modelos de tabela do Analysis Services 1400 nível de compatibilidade
- Corrigido um problema no novo editor DAX em que o operador de atribuição não pôde ser em uma linha separada ao definir uma medida de janela de ferramenta
- Corrigido um problema que impediu a exibição de tabela medidas de atualização ao renomear medidas na perspectiva
- Atualizado mecanismo do Analysis Services integrada de espaço de trabalho e modelo de objeto de tabela que corrige uma regressão que causou a projetos de tabela 1200, que contém traduções em implantar o servidor SQL Server 2016 Analysis Services
- Corrigido um problema de desempenho que fez creation\deletion de novas fontes de dados tabulares 1400 muito lentas
- Corrigido um problema em que o diagrama DSV em modelos multidimensionais foi parar renderização se alterar o modo de exibição rapidamente entre diferentes DSVs

**DacFx 17.1**

- Corrigido um problema ao criptografar uma coluna com tabelas com otimização de memória com outras colunas de identidade
- Suporte SQLDOM para a opção CATALOG_COLLATION para criar o banco de dados





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção anterior.

1. [Log de alterações do SSDT (SQL Server Data Tools)](#TitleNum_1)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## Artigos irmã

Esta seção lista os artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.com: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (12 + 2): documentos de **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 2): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + atualizado (3 + 0): documentos do **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (1 + 2): documentos do **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (2 + 8): documentos do **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + atualizado (1 + 0): documentos do **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (5 + 5): documentos de **Bancos de dados relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (2 + 0): documentos do **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 4): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + atualizado (1 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): documentos do **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


&nbsp;


