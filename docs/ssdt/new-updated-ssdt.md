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
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 8ae9a49443525524cf7f6ffceba4fb44984c7052
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Novos e atualizados recentemente: SSDT (SQL Server Data Tools)



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **18-07-2017** &nbsp; até &nbsp; **11-09-2017**
- *Área de assunto:* &nbsp; **SSDT (SQL Server Data Tools)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [SQL Server Data Tools – Termos de Licença](sql-server-data-tools-license-terms-vs2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma grande atualização recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Log de alterações do SSDT (SQL Server Data Tools)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Log de alterações do SSDT (SQL Server Data Tools)](changelog-for-sql-server-data-tools-ssdt.md)

*Atualizado: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 536fe0fe41b023a4186f494a509fa14fcbafccf4 e5bc7b76c1755f5a1af77f6cd63d8e8691dafe7b  (PR=2927  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=71a2cbf181c94c4c1aff877614aadf890b2496e0) -->



**SSDT para Visual Studio 2017 (versão prévia 15.3.0)**

Número de build: 14.0.16121.0

**Novidades**


Esta versão prévia é a primeira versão do SSDT para Visual Studio 2017. Essa versão apresenta uma experiência de instalação Web autônoma para projetos do Banco de Dados do SQL Server, do Analysis Services, do Reporting Services e do Integration Services no Visual Studio 2017 15.3 ou posterior.


**Problemas conhecidos**

- O instalador não foi localizado.
- O SSIS não foi localizado.
- A tarefa Executar Pacote do SSIS não dá suporte à depuração quando *ExecuteOutofProcess* está definido como *True*. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.
- Para obter uma lista completa de alterações, confira [changelog--changelog-for-sql-server-data-tools-ssdt.md).
- Relate problemas no site de [Comentários do SSDT Connect](https://connect.microsoft.com/SQLServer/Feedback).
- Os pacotes do SSIS que contêm extensões de terceiros não poderão ser mudados para serem direcionados a outras versões do servidor.


**SSDT 17.2 para Visual Studio 2015**

Número de build: 14.0.61707.300

**Novidades**



**Projetos do AS:**
- A Segurança em nível de objeto agora pode ser configurada na caixa de diálogo *Funções* para segurança avançada em modelos de tabelas de nível de compatibilidade 1400.
- Nova seleção de membro de função AAD para usuários sem endereços de email em modelos do AS Azure em projetos SSDT AS para VS2017.
- Nova propriedade de projeto "Sempre solicitar" do AS Azure em projetos de tabela do SSDT AS para personalizar o comportamento de armazenamento em cache de credenciais ADAL.


**Correções de Bugs**


**Geral**
- Referências de identidade visual atualizada para SQL Server 2017.

**Projetos do AS**
- Correções de desempenho significativas feitas para melhorar a experiência ao confirmar as alterações de medida DAX e outras edições no modelo.
- Correção de diversos problemas com a integração do Power Query em projetos do Analysis Services usando modelos de tabela de nível de compatibilidade 1400.
- Correção de um problema em projetos multidimensionais no VS2017 somente quando o designer do Design Aggregation não conseguir carregar.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista os artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, dentro do nosso repositório GitHub.com: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 12): documentos de **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (5 + 0): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (5 + 1): documentos do **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (19 + 82): documentos do **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (1 + 8): documentos do **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (12 + 1): documentos de **Bancos de Dados Relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (0 + 1): documentos do **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (7 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (1 + 1): documentos do **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 2): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (1 + 4): documentos do **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (4 + 1): documentos do **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (0 + 1): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0 + 0): documentos do **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



