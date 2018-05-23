---
title: Atualizado – documentos do SSDT para SQL Server | Microsoft Docs
description: Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para SSDT (SQL Server Data Tools) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 04/28/2018
ms.openlocfilehash: 99b0844803e1ce95bd6f73b0d45a2baf867428ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Novos e atualizados recentemente: SSDT (SQL Server Data Tools)



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **SSDT (SQL Server Data Tools)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Suporte do Azure Active Directory no SSDT (SQL Server Data Tools)](azure-active-directory.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Log de alterações do SSDT (SQL Server Data Tools)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Log de alterações do SSDT (SQL Server Data Tools)](changelog-for-sql-server-data-tools-ssdt.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 29.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 de18314845cffa197b3fd2ed868f2c330760bedb 5487de1ed57c16a6517a3a8849f412c208f1889f  (PR=5676  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->





**SSDT para Visual Studio 2017 (15.6.0)**

Número de build: 14.0.16162.0 Data de lançamento: 10 de abril de 2018

**Novidades**


**SSIS:**

1.  Correção de um problema em que a tarefa de processamento AS não registra quaisquer etapas de processamento ao direcionar para o SQLServer2016 e SQLServer2017
2.  Correção de um problema em que a violação de acesso acontecerá ao abrir o dtsx com nomes de tarefa muitos longos e que não estejam em inglês no SSDT.
3.  Correção de um problema em que, às vezes, uma lista variável de ScriptTask desaparecerá na interface do usuário da tarefa.
4.  Correção de um problema em que a adição de uma cópia de um pacote existente falhará quando o local do pacote for o SQL Server.
5.  Correção de um problema em que o foco fica paralisado ao acessar a caixa de combinação em uma caixa de diálogo do editor.
6.  Correção de um problema em que a tela de fundo não será alterada ao modificar o tema do VS.
7.  Correção de um problema em que os rótulos de anotação e carregamento ficam invisíveis no tema escuro.
8.  Correção de um problema em que a propriedade de estado não está definida corretamente para os itens desabilitados da caixa de ferramentas do SSIS.
9.  Correção de um problema em que sempre há falha ao executar WebServiceTask.
10. Correção de um problema em que a implantação de pacote falhará se a cadeia de conexão estiver definida como variável com expressão dependente de parâmetros do projeto.

**Instalador:**

1.  Adicione o link do "Programa de Aperfeiçoamento da Experiência do Usuário para SQL Server Data Tools" ao aviso de isenção de responsabilidade de privacidade.
2.  Correção de um problema em que a janela de instalação do VS é exibida ao selecionar "Instale uma nova instância do SQL Server Data Tools para Visual Studio 2017"

**Problemas conhecidos:**

1.  A Tarefa Executar Pacote do SSIS não é compatível com a depuração quando ExecuteOutOfProcess está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.



**SSDT para Visual Studio 2017 (15.5.2)**

Número de build: 14.0.16156.0

**Novidades**


**SSIS**
1.  Correção de um problema em que a migração de projetos do SSIS 2008 falha quando o SSAS e o SSIS são instalados na mesma instância do VS 2017.
2.  Correção de um problema em que projetos Rdlc não podem ser criados quando o designer de relatórios Rdlc e o SSIS são instalados na mesma instância do VS 2017.







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente

- [Novo + Atualizado (11+6): &nbsp;documentos sobre a&nbsp; **Análise Avançada para SQL** ](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (18+0): &nbsp; documentos sobre o &nbsp;**Analysis Services para SQL** ](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (218+14): documentos sobre a **Conexão ao SQL** ](../connect/new-updated-connect.md)
- [Novo + Atualizado (14+0): &nbsp;documentos sobre o&nbsp; **Mecanismo de Banco de Dados para SQL** ](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (3+2): &nbsp;documentos sobre o&nbsp; **Integration Services para SQL** ](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (3+3): &nbsp;documentos sobre o&nbsp; **Linux para SQL** ](../linux/new-updated-linux.md)
- [Novo + Atualizado (7+10): &nbsp;documentos sobre o&nbsp; **Bancos de Dados Relacionais para SQL** ](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (0+2): &nbsp;documentos sobre o&nbsp; **Reporting Services para SQL** ](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (1+3): &nbsp;documentos sobre o&nbsp; **SQL Operations Studio** ](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (2+3): &nbsp;documentos sobre o&nbsp; **Microsoft SQL Server** ](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (1+1): &nbsp;documentos sobre o&nbsp; **SSDT (SQL Server Data Tools)** ](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (5+2): &nbsp;documentos sobre o&nbsp; **SSMS (SQL Server Management Studio)** ](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0+2): &nbsp;documentos sobre o&nbsp; **Transact-SQL** ](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (1+1): &nbsp;documentos sobre as&nbsp; **Ferramentas para SQL** ](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0+0): documentos sobre o **Sistema de Plataforma Analítica para SQL** ](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)

