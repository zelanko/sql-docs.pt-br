---
title: Atualizado – documentos sobre o T-SQL | Microsoft Docs
description: Exibir trechos de conteúdo atualizado para alterações recentes na documentação do Transact-SQL.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.date: 04/28/2018
ms.openlocfilehash: 294ecf21f39eda34d2fe10d6dc07b7280c6b6954
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409105"
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Novos e recentemente atualizado: Documentos do Transact-SQL



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **T-SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


***Não existem novos artigos a serem listados no momento.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](#TitleNum_1)
2. [Instruções RESTORE (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-alter-database-scoped-configuration-transact-sqlstatementsalter-database-scoped-configuration-transact-sqlmd"></a>1. &nbsp; [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](statements/alter-database-scoped-configuration-transact-sql.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 150.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f6833910b664d0059a9073589807b195052325b3 bf969f123b22e6ebc650380a6905156f26ed6ca6  (PR=0  ,  Filename=alter-database-scoped-configuration-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**Aplica-se a**: *{Included-Content-Goes-Here}*

Habilita ou desabilita a coleta de estatísticas de execução no nível do módulo para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_procedure_stats].

As estatísticas de execução de nível de módulo para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_proc_exec_stats].

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**Aplica-se a**: *{Included-Content-Goes-Here}*

Habilita ou desabilita a coleta de estatísticas de execução no nível de instrução para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_query_stats] e no [Repositório de Consultas].

As estatísticas de execução de nível de instrução para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_query_exec_stats].

Para ver mais detalhes sobre monitoramento de desempenho de módulos T-SQL compilados nativamente, veja [Monitorando o desempenho de procedimentos armazenados compilados nativamente].



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-restore-statements-transact-sqlstatementsrestore-statements-transact-sqlmd"></a>2. &nbsp; [Instruções RESTORE (Transact-SQL)](statements/restore-statements-transact-sql.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 339.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2902efb58bb964d3e9a0660956690d37f0397c00 36186a7cffd26ffa54a83e383ffd752dbc568a4d  (PR=0  ,  Filename=restore-statements-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Comentários gerais – Instância Gerenciada do Banco de Dados SQL**


Para uma restauração assíncrona, a restauração continuará mesmo se a conexão de cliente for interrompida. Se sua conexão for interrompida, será possível marcar a exibição [sys.dm_operation_status] para o status de uma operação de restauração (bem como para o banco de dados CREATE e DROP).

As opções de banco de dados a seguir são definidas/substituídas e não podem ser alteradas posteriormente:

- NEW_BROKER (se o agente não estiver habilitado no arquivo .bak)
- ENABLE_BROKER (se o agente não estiver habilitado no arquivo .bak)
- AUTO_CLOSE=OFF (se um banco de dados no arquivo .bak tiver AUTO_CLOSE=ON)
- RECOVERY FULL (se um banco de dados no arquivo .bak tiver modo de recuperação SIMPLE ou BULK_LOGGED)
- O grupo de arquivos otimizado para memória será adicionado e o XTP, chamado, se ele não estiver no arquivo .bak de origem. Qualquer grupo de arquivos otimizado para memória existente é renomeado para XTP
- As opções SINGLE_USER e RESTRICTED_USER são convertidas em MULTI_USER

**Limitações – Instância Gerenciada do Banco de Dados SQL**

Estas limitações se aplicam:

- Arquivos .BAK que contêm vários conjuntos de backup não podem ser restaurados.
- Arquivos .BAK que contêm vários arquivos de log não podem ser restaurados.
- A restauração falhará se o .bak contiver dados FILESTREAM.
- Os backups que contêm banco de dados que têm objetos na memória ativos não podem ser restaurados no momento.
- Os backups que contêm bancos de dados em que, em algum ponto, havia objetos na memória não podem ser restaurados no momento.
- Os backups que contêm bancos de dados em modo somente leitura não podem ser restaurados no momento. Essa limitação será removida em breve.

Para saber mais, veja [Instância gerenciada]







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

