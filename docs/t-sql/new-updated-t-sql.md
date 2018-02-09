---
title: Atualizado - T-SQL de documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Transact-SQL."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 02/03/2018
ms.openlocfilehash: c1f1ce751bd4bca781644e7e2f5282320c8c88a8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Novos e recentemente atualizado: documentos do Transact-SQL



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-12-03** &nbsp; - para - &nbsp; **2018-02-03**
- *Área de assunto:* &nbsp; **T-SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


***Não existem novos artigos a serem listados, no momento.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [CREATE STATISTICS (Transact-SQL)](#TitleNum_1)
2. [UPDATE STATISTICS (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-statistics-transact-sqlstatementscreate-statistics-transact-sqlmd"></a>1. &nbsp;[CREATE STATISTICS (Transact-SQL)](statements/create-statistics-transact-sql.md)

*Atualizado em: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 200.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 384e68493597bcc36876a3c7bada2630106256e2 c22168ea59b6020e8ebe1ccac5fa6a6049e6db4d  (PR=4460  ,  Filename=create-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*
**aplica-se a**: SQL Server (começando com o SQL Server de 2017 CU3).

 Substitui o **grau máximo de paralelismo** opção de configuração para a duração da operação de estatística. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.

 *max_degree_of_parallelism* pode ser:

 1 suprime geração de plano paralelo.

 \>1 restringe o número máximo de processadores usados em uma operação de estatística paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema.

 0 (padrão) usa o número real de processadores ou menos, com base na carga de trabalho atual do sistema.

 \<update_stats_stream_option > identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-update-statistics-transact-sqlstatementsupdate-statistics-transact-sqlmd"></a>2. &nbsp; [UPDATE STATISTICS (Transact-SQL)](statements/update-statistics-transact-sql.md)

*Atualizado em: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 167.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5721e21a9f43fa784fe9357c47cb2a814385e63d 24ae47c553635f389a182e5e643bf9bd6bf59e78  (PR=4460  ,  Filename=update-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*

**Aplica-se a**: SQL Server (começando com o SQL Server de 2017 CU3).

 Substitui o **grau máximo de paralelismo** opção de configuração para a duração da operação de estatística. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.

 *max_degree_of_parallelism* pode ser:

 1 suprime geração de plano paralelo.

 \>1 restringe o número máximo de processadores usados em uma operação de estatística paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema.

 0 (padrão) usa o número real de processadores ou menos, com base na carga de trabalho atual do sistema.








## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *fazer* new ou recentemente atualizou artigos


- [Novo + atualizado (1 + 3):&nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (0 + 1):&nbsp; **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 1):&nbsp; **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 1):&nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (12 + 1): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (6 + 2):&nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (15 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (2 + 9):&nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (1 + 0):&nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 1):&nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (1 + 1):&nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2):&nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Entidade áreas que fazer *não* qualquer novo ou recentemente atualizou artigos


- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): **ActiveX Data Objects (ADO) para o SQL** documentos](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)


