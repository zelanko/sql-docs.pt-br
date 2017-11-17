---
title: Atualizado - T-SQL de documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Transact-SQL."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: t-sql
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.author: genemi
ms.workload: t-sql
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 4d48c7df783ebe50f7b5d7fe3e72bef91559006e
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Novos e recentemente atualizado: documentos do Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]


A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-09-11** &nbsp; - para - &nbsp; **2017-09-27**
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

1. [sql_variant (Transact-SQL)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sqlvariant-transact-sqldata-typessql-variant-transact-sqlmd"></a>1. &nbsp; [sql_variant (Transact-SQL)](data-types/sql-variant-transact-sql.md)

*Atualizado em: 2017-09-13* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 111.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 659578de7de33d8672ceb9542093862107d13526 c80026de2b0deedab3722a874e9124c2cfefa049  (PR=0  ,  Filename=sql-variant-transact-sql.md  ,  Dirpath=docs\t-sql\data-types\  ,  MergeCommitSha40=5cd78481b3fac55ec34b59e7b1ad25e0e14d2a00) -->



**Exemplos**


**A. Usando um sql_variant em uma tabela**

 O exemplo a seguir, cria uma tabela com um tipo de dados sql_variant. Em seguida, o exemplo recupera `SQL_VARIANT_PROPERTY` informações sobre o `colA` valor `46279.1` onde `colB`  = `1689`, considerando que `tableA` tem `colA` que é do tipo `sql_variant` e `colB`.

```
CREATE   TABLE tableA(colA sql_variant, colB int)
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'
FROM      tableA
WHERE      colB = 1689
```

 ..! NCLUIR-NotShown - ssResult-... /.. /Includes/ssresult-MD.MD]) Observe que cada um destes três valores é uma **sql_variant**.

```
Base Type    Precision    Scale
---------    ---------    -----
decimal      8           2

(1 row(s) affected)
```

**B. Usando um sql_variant como uma variável**

 O exemplo a seguir, cria uma variável usando o tipo de dados sql_variant e, em seguida, recupera `SQL_VARIANT_PROPERTY` informações sobre uma variável chamada @v1.

```
DECLARE @v1 sql_variant;
SET @v1 = 'ABC';
SELECT @v1;
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');
```








## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (0 + 1): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (0 + 1): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizados (4 + 1): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (17 + 0): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (3 + 0): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (1 + 1): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (2 + 0): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 1): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (0 + 0): documentos do **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): **Tools para SQL** documentos](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



