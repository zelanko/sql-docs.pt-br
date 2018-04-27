---
title: Atualizado – documentos do SSMS para SQL Server | Microsoft Docs
description: Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para o SSMS (SQL Server Management Studio) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: 8f2ad52b9741a3220a8c5db0a60924a41cc62d27
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Novos e atualizados recentemente: SSMS (SQL Server Management Studio) para SQL Server



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-12-2017** &nbsp; até &nbsp; **03-02-2018**
- *Área de assunto:* &nbsp; **SSMS (SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Baixar o SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio – Changelog (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp;[Baixar o SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Atualizado: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



O SMS 17.4 é a versão mais recente do SQL Server Management Studio. A geração 17.X do SSMS oferece suporte a quase todas as áreas de recursos do SQL Server 2008 por meio do SQL Server 2017. A Versão 17.x também oferece suporte ao PaaS do SQL Analysis Service.

A versão 17.4 inclui:

Avaliação de Vulnerabilidades:
- Adicionado um novo serviço de Avaliação de Vulnerabilidade de SQL para verificar seus bancos de dados para possíveis vulnerabilidades e desvios das práticas recomendadas, como configurações incorretas, excesso de permissões e dados confidenciais expostos.
- Os resultados da avaliação incluem etapas práticas para resolver cada problema e scripts de correções personalizadas quando aplicável. O relatório de avaliação pode ser personalizado para cada ambiente e ajustado de acordo com requisitos específicos. Saiba mais em [Avaliação de Vulnerabilidades SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Correção do problema no qual *HasMemoryOptimizedObjects* gerava exceção no Azure.
- Adicionado suporte para o novo recurso CATALOG_COLLATION.

Painel AlwaysOn:
- Melhorias para análise de latência em Grupos de disponibilidade.
- Adicionados dois novos relatórios: *AlwaysOn\_Latency\_Primary* e *AlwaysOn\_Latency\_Secondary*.

Plano de execução:
- Links atualizados para apontar para a documentação correta.
- Permita a análise de plano único diretamente do plano real produzido.
- Novo conjunto de ícones.
- Adicionado suporte para reconhecer "Aplicar operadores lógicos" como GbApply, InnerApply.

XE Profiler:
- Renomeado para XEvent Profiler.
- Os comandos de menu Parar/Iniciar agora param/iniciam a sessão por padrão.
- Atalhos de teclado habilitados (por exemplo, CTRL-F para pesquisar).
- Ações de nome de host \_nome e cliente\_ do banco de dados adicionadas a eventos apropriados nas sessões do XEvent Profiler. Para que a alteração entre em vigor, talvez seja necessário excluir instâncias existentes da sessão do QuickSessionStandard ou QuickSessionTSQL nos servidores – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2. &nbsp; [SQL Server Management Studio – Log de alterações (SSMS)](sql-server-management-studio-changelog-ssms.md)

*Atualizado: 29-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

Geralmente disponível| Número de build: 14.0.17213.0

**Novidades**


**SSMS geral**

Avaliação de Vulnerabilidades:
- Adicionado um novo serviço de Avaliação de Vulnerabilidade de SQL para verificar seus bancos de dados para possíveis vulnerabilidades e desvios das práticas recomendadas, como configurações incorretas, excesso de permissões e dados confidenciais expostos.
- Os resultados da avaliação incluem etapas práticas para resolver cada problema e scripts de correções personalizadas quando aplicável. O relatório de avaliação pode ser personalizado para cada ambiente e ajustado de acordo com requisitos específicos. Saiba mais em [Avaliação de Vulnerabilidades SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Correção do problema no qual *HasMemoryOptimizedObjects* gerava exceção no Azure.
- Adicionado suporte para o novo recurso CATALOG_COLLATION.

Painel AlwaysOn:
- Melhorias para análise de latência em Grupos de disponibilidade.
- Adicionados dois novos relatórios: *AlwaysOn\_Latency\_Primary* e *AlwaysOn\_Latency\_Secondary*.

Plano de execução:
- Links atualizados para apontar para a documentação correta.
- Permita a análise de plano único diretamente do plano real produzido.
- Novo conjunto de ícones.
- Adicionado suporte para reconhecer "Aplicar operadores lógicos" como GbApply, InnerApply.

XE Profiler:
- Renomeado para XEvent Profiler.
- Os comandos de menu Parar/Iniciar agora param/iniciam a sessão por padrão.
- Atalhos de teclado habilitados (por exemplo, CTRL-F para pesquisar).
- Ações de nome de host \_nome e cliente\_ do banco de dados adicionadas a eventos apropriados nas sessões do XEvent Profiler. Para que a alteração entre em vigor, talvez seja necessário excluir instâncias existentes da sessão do QuickSessionStandard ou QuickSessionTSQL nos servidores – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

Linha de comando:
- Adicionada uma nova opção de linha de comando ("-G") que pode ser usada para fazer com que o SSMS se conectar automaticamente a um servidor/banco de dados usando a Autenticação do Active Directory ('Integrado' ou 'Senha'). Para obter detalhes, consulte [Utilitário de Ssms](ssms-utility.md).







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente


- [Novo + Atualizado (1 + 3):&nbsp; documentos sobre a **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre o **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre a **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (12 + 1): **documentos sobre o** Integration Services para SQL](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (6 + 2):&nbsp; documentos sobre o **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + atualizado (15 + 0): **documentos sobre o** PowerShell para SQL](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (2 + 9):&nbsp; documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (1 + 0):&nbsp; documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (1 + 1):&nbsp; documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (1 + 1):&nbsp; documentos sobre o **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (0+1):&nbsp; documentos sobre o **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1+2):&nbsp; documentos sobre o **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2):&nbsp; documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente


- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


