---
title: "Atualizado — Documentos do SQL Server | Microsoft Docs"
description: "Exibir trechos de conteúdo atualizado para documentação do SQL Server alterada recentemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: sql-non-specified
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.author: genemi
ms.openlocfilehash: 77a97d94d005b43bf4c1a313a15a501cbe74a216
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-docs"></a>Novos e recém-atualizados: documentos do SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de assunto:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Parceiros de desenvolvimento do SQL Server](partner-dev-sql-server.md)
2. [Parceiros de alta disponibilidade e recuperação de desastre do SQL Server](partner-hadr-sql-server.md)
3. [Parceiros de gerenciamento do SQL Server](partner-management-sql-server.md)
4. [Parceiros de monitoramento do SQL Server](partner-monitor-sql-server.md)
5. [Notas de versão do SQL Server 2012 SP4](sql-server-2012-sp4-release-notes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Notas de Versão do SQL Server 2017.](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp; [Notas de Versão do SQL Server 2017](sql-server-2017-release-notes.md)

*Atualizado: 20-11-2017* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 37.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c9ac7e027e32b17bb9b54a4a878f70a70404f1cb 5b1aa8dc715fbb08d82b241f1e47f6e443b3e2fc  (PR=4032  ,  Filename=sql-server-2017-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



- **Solução alternativa:** primeiro, reinicialize o computador e verifique se o compartilhamento de rede do FILESTREAM está disponível. Se o compartilhamento ainda não estiver disponível, conclua as seguintes etapas:

    1. No SQL Server Configuration Manager, clique com o botão direito do mouse na instância do SQL Server e clique em **Propriedades**.
    2. Na guia **FILESTREAM**, desmarque **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo** e, em seguida, clique em **Aplicar**.
    3. Marque **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo** novamente com o nome original do compartilhamento e clique em **Aplicar**.

**MDS (Master Data Services)**

- **Problema e impacto no cliente:** na página de permissões do usuário, ao conceder permissão para o nível raiz no modo de exibição de árvore da entidade, você pode ver o seguinte erro:`"The model permission cannot be saved. The object guid is not valid"`

- **Soluções alternativas:**
  - Conceder permissão aos sub-nós no modo de exibição de árvore, em vez do nível raiz.
  - ou
  - Execute o script descrito neste blog da equipe MDS [erro ao aplicar permissões no nível de entidade](http://sqlblog.com/blogs/mds_team/archive/2017/09/05/sql-server-2016-sp1-cu4-regression-error-while-applying-permission-on-entity-level-quick-workaround.aspx)

**Analysis Services**

- **Problema e impacto sobre o cliente:** os conectores de dados das fontes a seguir ainda não estão disponíveis para modelos de tabela no nível de compatibilidade 1400.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **Solução alternativa:** não há.

- **Problema e impacto no cliente:** modelos de consulta direta no nível de compatibilidade 1400 com perspectivas podem falhar em consultas ou descoberta de metadados.
- **Solução alternativa:** remova as perspectivas e implante-as novamente.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 14): documentos sobre **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (87 + 0): documentos sobre **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (5 + 4): documentos sobre **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1): documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (2 + 2): documentos sobre **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (10 + 9): documentos sobre **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (2 + 4): documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (4 + 2): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (0 + 1): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (21 + 0): documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (5 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1 + 0): documentos sobre o **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


