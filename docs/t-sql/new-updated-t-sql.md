---
title: Atualizado - T-SQL de documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Transact-SQL."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: t-sql
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fa2ad3f4bc6071c54b9996a893ee584ba215100f
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Novos e recentemente atualizado: documentos do Transact-SQL



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-07-18** &nbsp; - para - &nbsp; **2017-09-11**
- *Área de assunto:* &nbsp; **T-SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir saltar para novos artigos que foram adicionados recentemente.


1. [PREVER (Transact-SQL)](queries/predict-transact-sql.md)
2. [ALTER biblioteca externa (Transact-SQL)](statements/alter-external-library-transact-sql.md)
3. [Criar biblioteca externa (Transact-SQL)](statements/create-external-library-transact-sql.md)
4. [SOLTE a biblioteca externa (Transact-SQL)](statements/drop-external-library-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção foram extraídas.

1. [CAST e CONVERT (Transact-SQL)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-cast-and-convert-transact-sqlfunctionscast-and-convert-transact-sqlmd"></a>1. &nbsp;[CAST e CONVERT (Transact-SQL)](functions/cast-and-convert-transact-sql.md)

*Atualizado em: 08 / 09 / 2017* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 647.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b805ecddecda72ffc026c3866b5284a79b69fb3f f2906eaf87c7cdf1409922d4efba8cd1c5635674  (PR=0  ,  Filename=cast-and-convert-transact-sql.md  ,  Dirpath=docs\t-sql\functions\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



**K. Usando CAST com operadores aritméticos**

O exemplo a seguir calcula uma computação de coluna única, dividindo o preço de unidade do produto (`UnitPrice`) pela porcentagem de desconto (`UnitPriceDiscountPct`). Esse resultado é convertido em um tipo de dados `int` depois de ser arredondado para o número inteiro mais próximo. Usa AdventureWorksDW.

```
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice
FROM dbo.FactResellerSales
WHERE SalesOrderNumber = 'SO47355'
      AND UnitPriceDiscountPct > .02;
```

..! NCLUIR-NotShown - ssResult-... /.. /Includes/ssresult-MD.MD])

```
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1
```

**L. Usando CAST para concatenar**

O exemplo a seguir concatena expressões não são de caractere usando CONVERSÃO. Usa AdventureWorksDW.

```
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice
FROM dbo.DimProduct
WHERE ListPrice BETWEEN 350.00 AND 400.00;
```

..! NCLUIR-NotShown - ssResult-... /.. /Includes/ssresult-MD.MD])

```
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09
```

**M. Usando CAST para produzir texto mais legível**

O exemplo a seguir usa a CONVERSÃO na lista de seleção para converter o `Name` coluna para um **char (10)** coluna. Usa AdventureWorksDW.

```
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice
FROM dbo.DimProduct
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';
```

..! NCLUIR-NotShown - ssResult-... /.. /Includes/ssresult-MD.MD])







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público de GitHub.com: [sql/MicrosoftDocs-documentos](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (3 + 12): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (5 + 0): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (5 + 1): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (1 + 8): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (12 + 1): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 2): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



