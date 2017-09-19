---
title: "Atualizado — Documentos do SQL Server | Microsoft Docs"
description: "Exibir trechos de conteúdo atualizado para documentação do SQL Server alterada recentemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: bd22355518bde09b5af006062b2ec03cf11a7597
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>Novos e recém-atualizados: documentos do SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **18-07-2017** &nbsp; até &nbsp; **11-09-2017**
- *Área de assunto:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [SQL Server 2008 R2 SP2 Release Notes](sql-server-2008-r2-sp2-release-notes.md)
2. [Notas de Versão do SQL Server 2012](sql-server-2012-release-notes.md)
3. [SQL Server 2012 SP1 Release Notes](sql-server-2012-sp1-release-notes.md)
4. [SQL Server 2012 SP2 Release Notes](sql-server-2012-sp2-release-notes.md)
5. [Notas de Versão do SQL Server 2012 SP3](sql-server-2012-sp3-release-notes.md)
6. [SQL Server 2014 Release Notes](sql-server-2014-release-notes.md)
7. [Help Viewer e conteúdo offline para o SQL Server](sql-server-help-installation.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma grande atualização recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Novidades no SQL Server 2016](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-whats-new-in-sql-server-2016what-s-new-in-sql-server-2016md"></a>1. &nbsp;[Novidades no SQL Server 2016](what-s-new-in-sql-server-2016.md)

*Atualizado: 08-09-2017* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 34.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e5bc0c05f120289f09a535400a4d521e4113ae55 0607d0a9af1c9a8dd9d3d7b0606895ff23bbffdc  (PR=0  ,  Filename=what-s-new-in-sql-server-2016.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



- Baixe **gratuitamente** a [**edição do desenvolvedor do SQL Server 2016!**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers).
- Baixe a versão mais recente do [SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx).
- Tem uma conta do Azure? Ative uma [Máquina Virtual com o SQL Server 2016 já instalado](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/).

**Mecanismo de Banco de Dados do SQL Server 2016**

- Agora você pode configurar **vários arquivos de banco de dados tempDB** durante a instalação e configuração do SQL Server.
- Novo **Repositório de Consultas** armazena textos de consulta, planos de execução e métricas de desempenho no banco de dados, permitindo monitoramento e solução de problemas de desempenho com facilidade. Um painel mostra quais consultas consumiram mais tempo, memória ou recursos de CPU.
- As **tabelas temporais** são tabelas de histórico que registram todas as alterações de dados, incluindo as datas e horas em que ocorreram.
- O novo **suporte interno a JSON** no SQL Server dá suporte a importações, exportações, análise e armazenamento de JSON.
- O novo mecanismo de consulta **PolyBase** integra o SQL Server com dados externos no Hadoop ou no Armazenamento de Blobs do Azure. Você pode importar e exportar dados, bem como executar consultas.
- O novo recurso **Stretch Database** permite que você arquive dados de forma dinâmica e segura a partir de um banco de dados SQL Server local para um banco de dados SQL do Azure na nuvem. O SQL Server consulta automaticamente os dados locais e remotos em bancos de dados vinculados.
- **OLTP in-memory:**
    - Agora dá suporte a restrições FOREIGN KEY, UNIQUE e CHECK e procedimentos armazenados compilados nativos OR, NOT, SELECT DISTINCT, OUTER JOIN e subconsultas em SELECT.
    - Dá suporte a tabelas de até 2 TB (acima de 256 GB).
    - Tem aprimoramentos de índice de armazenamento de coluna para classificação e suporte ao Grupo de Disponibilidade AlwaysOn.
- Novos recursos de segurança:
    - **Always Encrypted:** quando esta opção está habilitada, somente o aplicativo que tem a chave de criptografia pode acessar os dados confidenciais criptografados no banco de dados SQL Server 2016. A chave nunca é passada para o SQL Server.







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



