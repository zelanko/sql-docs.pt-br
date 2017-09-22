---
title: "Atualizado – Documentos do Mecanismo de Banco de Dados | Microsoft Docs"
description: "Exiba trechos de conteúdo atualizado da documentação com alterações recentes do Mecanismo de Banco de Dados."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: ce80496cdf82c2bc2df2447ed043216e6c78ad7e
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-database-engine-docs"></a>Novo e atualizado recentemente: Documentos do Mecanismo de Banco de Dados



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **18-07-2017** &nbsp; até &nbsp; **11-09-2017**
- *Área de assunto:* &nbsp; **Mecanismo de Banco de Dados**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Instalação do SQL Server](install-windows/installation-for-sql-server.md)
2. [Upgrades de versão e edição com suporte do SQL Server 2017](install-windows/supported-version-and-edition-upgrades-2017.md)
3. [Mecanismo de Banco de Dados do SQL Server](sql-server-database-engine-overview.md)
4. [Novidades do Mecanismo de Banco de Dados – SQL Server 2016](whats-new-in-sql-server-2016.md)
5. [Novidades do Mecanismo de Banco de Dados – SQL Server 2017](whats-new-in-sql-server-2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Propagação automática para réplicas secundárias](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-automatic-seeding-for-secondary-replicasavailability-groupswindowsautomatic-seeding-secondary-replicasmd"></a>1. &nbsp; [Propagação automática para réplicas secundárias](availability-groups/windows/automatic-seeding-secondary-replicas.md)

*Atualizado em: 21-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 55.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0b7b6a23f38bfe5959ccd170527a9bbdb308dc4b dc51fdf69649ed6cae03584cff7bc900d5b72149  (PR=2896  ,  Filename=automatic-seeding-secondary-replicas.md  ,  Dirpath=docs\database-engine\availability-groups\windows\  ,  MergeCommitSha40=80642503480add90fc75573338760ab86139694c) -->



No SQL Server 2016 e nas versões anteriores, a pasta na qual o banco de dados é criado pela propagação automática já deve existir e ser a mesma que a do caminho da réplica primária.

No SQL Server 2017, a Microsoft recomenda usar os mesmos dados e o mesmo caminho do arquivo de log em todas as réplicas que participam de um grupo de disponibilidade, mas você poderá usar caminhos diferentes, se for necessário. Por exemplo, em um grupo de disponibilidade de plataforma cruzada, uma instância do SQL Server está no Windows e a outra instância do SQL Server está no Linux. As plataformas diferentes têm caminhos padrão diferentes. O SQL Server 2017 dá suporte para réplicas de grupo de disponibilidade em instâncias do SQL Server com caminhos padrão diferentes.

A tabela a seguir apresenta exemplos dos layouts de disco de dados compatíveis que podem dar suporte à propagação automática:

|Instância Primária</br>Caminho de dados padrão|Instância secundária</br>Caminho de dados padrão|Instância Primária</br>Local do arquivo de origem|Instância secundária</br> Local do arquivo de destino
|:------|:------|:------|:------
|c:\\data\\ |/var/opt/mssql/data/ |c:\\data\\ |/var/opt/mssql/data/|
|c:\\data\\ |/var/opt/mssql/data/ |c:\\data\\group1\\ |/var/opt/mssql/data/group1/|
|c:\\data\\ |d:\\data\\ |c:\\data\\ |d:\\data\\
|c:\\data\\ |d:\\data\\ |c:\\data\\group1\\ |d:\\data\\group1\

Os cenários em que a localização do banco de dados da réplica primária e da secundária não forem os caminhos padrão da instância não serão afetados por esta alteração. Os requisitos para os caminhos de arquivo da réplica secundária serem compatíveis com os caminhos do arquivo da réplica primária permanecem os mesmos.

|Instância Primária</br>Caminho de dados padrão|Instância secundária</br>Caminho de dados padrão|Instância Primária</br>Local do arquivo|Instância secundária</br> Local do arquivo
|:------|:------|:------|:------
|c:\\data\\ |c:\\data\\ |d:\\group1\\ |d:\\group1\\
|c:\\data\\ |c:\\data\\ |d:\\data\\ |d:\\data\\
|c:\\data\\ |c:\\data\\ |d:\\data\\group1\\ |d:\\data\\group1\\

Se você mesclar os caminhos que estiverem dentro e fora do padrão nas réplicas primária e secundária, o SQL Server 2017 se comportará de forma diferente das versões anteriores. A tabela a seguir mostra o comportamento do SQL Server 2017.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3+12): documentos sobre a **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (5+0): documentos sobre a **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (5+1): documentos sobre o **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (19+82): documentos sobre o **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (1+8): documentos sobre o **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (12+1): documentos sobre os **Bancos de Dados Relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (0+1): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (7+1): documentos sobre o **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (1+1): documentos sobre o **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (0+2): documentos sobre o **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (1+4): documentos sobre o **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (4+1): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (0+1): documentos sobre as **Ferramentas para SQL**](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



