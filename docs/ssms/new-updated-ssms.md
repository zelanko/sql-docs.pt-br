---
title: Atualizado – documentos do SSMS para SQL Server | Microsoft Docs
description: Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para o SSMS (SQL Server Management Studio) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 04/28/2018
ms.openlocfilehash: 1ce446219f71baca0f4cdedc835fca929b572a0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Novos e atualizados recentemente: SSMS (SQL Server Management Studio) para SQL Server



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **SSMS (SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Tutorial: Conectar-se a uma instância do SQL Server e consultá-la usando o SQL Server Management Studio](tutorials/connect-query-sql-server.md)
2. [Tutorial: gerar script de objetos no SQL Server Management Studio](tutorials/scripting-ssms.md)
3. [Tutorial: componentes e configuração do SQL Server Management Studio](tutorials/ssms-configuration.md)
4. [Tutorial: mais dicas e truques para usar o SSMS](tutorials/ssms-tricks.md)
5. [Tutorial: usando Modelos no SQL Server Management Studio](tutorials/templates-ssms.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [SQL Server Management Studio – Changelog (SSMS)](#TitleNum_1)
2. [Tutoriais do SQL Server Management Studio (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1. &nbsp; [SQL Server Management Studio – Log de alterações (SSMS)](sql-server-management-studio-changelog-ssms.md)

*Atualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 eb641ac39386a26a76dc303f5bd55eb3f9f4c78d f560f09b51ea30b255c10f7eb86857c3090881d9  (PR=5676  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**SSMS 17.6**


Número da versão: 17.6<br>
Número de build: 14.0.17230.0<br>
Data do lançamento: 20 de março de 2018

**Novidades**


**SSMS geral**

Instância Gerenciada do Banco de Dados SQL:

- Suporte adicionado à [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance). Instância Gerenciada do Banco de Dados SQL do Azure (versão prévia) é um novo tipo do Banco de Dados SQL do Azure, fornecendo quase 100% de compatibilidade com o SQL Server local, uma implementação [VNet (rede virtual)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) nativa que aborda questões comuns de segurança e um [modelo de negócios](https://azure.microsoft.com/pricing/details/sql-database/) favorável para clientes do SQL Server local.
- Suporte para cenários comuns de gerenciamento, como:
   - Criar e alterar bancos de dados.
   - Fazer backup e restauração de bancos de dados.
   - Importar, exportar, extrair e publicar Aplicativos da Camada de Dados.
   - Exibir e alterar as propriedades do servidor.
   - Suporte completo para o Pesquisador de Objetos.
   - Gerando scripts de objetos de banco de dados.
   - Suporte para trabalhos do SQL Agent.
   - Suporte para servidores vinculados.
- Saiba mais sobre Instâncias Gerenciadas [aqui](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/).

Pesquisador de Objetos:
- Configurações adicionadas para não forçar colchetes em volta de nomes ao arrastar e soltar do Pesquisador de Objetos para a Janela de Consulta. (Sugestões do usuário [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) e [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051).)

Classificação de dados:
- Melhorias e correções de bug gerais.

**IS (Integration Services)**

- Suporte adicionado para implantar pacotes em uma [Instância Gerenciada do Banco de Dados SQL](docs/ssms/https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tutorials-for-sql-server-management-studio-ssmstutorialstutorial-sql-server-management-studiomd"></a>2. &nbsp; [Tutoriais do SQL Server Management Studio (SSMS)](tutorials/tutorial-sql-server-management-studio.md)

*Atualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 49.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b272c75bab04912ebb706098cf6b6a6c80d9e2b8 d453ebc8251fb83ffcb1af58c9a08bb65b3e9fa2  (PR=5676  ,  Filename=tutorial-sql-server-management-studio.md  ,  Dirpath=docs\ssms\tutorials\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- Tutorial: Como conectar e consultar o SQL Server usando o SSMS

    Neste tutorial, você aprenderá como se conectar à Instância do SQL Server. Você também aprenderá alguns comandos básicos do T-SQL (Transact-SQL) para criar e consultar um novo banco de dados.

- Tutorial: Como gerar scripts de objetos no SSMS

    Neste tutorial, você aprenderá a gerar scripts de vários objetos no SSMS, incluindo bancos de dados e consultas.

- Tutorial: Como usar modelos no SSMS

    Neste tutorial, você aprenderá como trabalhar com os Modelos predefinidos no SSMS. Os modelos são um recurso pouco conhecido que armazenam diversos trechos de código Transact-SQL para várias tarefas de administração de banco de dados.

- Tutorial: Configuração do SSMS

    Neste tutorial, você aprenderá os conceitos básicos de como configurar o ambiente do SSMS, como a alterar o layout do ambiente. Este tutorial também explica quais são os diferentes componentes do SSMS.


- Tutorial: mais dicas e truques para usar o SSMS

    Neste tutorial, você aprenderá mais dicas e truques para usar o SSMS. Este tutorial inclui o seguinte:
    - Comentar e remover marca de comentário do texto
    - Recuando texto
    - Filtrando objetos no Pesquisador de Objetos
    - Acessar o log de erros do SQL Server
    - Encontrando o nome da sua instância








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

