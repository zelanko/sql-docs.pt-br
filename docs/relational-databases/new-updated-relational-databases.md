---
title: "Atualizado — Documentos de bancos de dados relacionais | Microsoft Docs"
description: "Exibir trechos de conteúdo atualizado para documentação de Bancos de Dados Relacionais alterada recentemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: relational-databases-misc
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 70cb071dc7b6f4ff15c5c7dee3f24bb352d6eb61
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Novos e recém-atualizados: documentos de Bancos de Dados Relacionais
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **11-09-2017** &nbsp; até &nbsp; **27-09-2017**
- *Área de assunto:* &nbsp; **Bancos de dados relacionais**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Importar e exportar dados do SQL Server e do Banco de Dados SQL do Azure](import-export/overview-import-export.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Visão geral de tipos de dados espaciais](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-spatial-data-types-overviewspatialspatial-data-types-overviewmd"></a>1. &nbsp; [Visão Geral de Tipos de Dados Espaciais](spatial/spatial-data-types-overview.md)

*Atualizado: 26-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 27.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96dd44cf49e96d1d543a629d49de297dba9c1753 2e9629f852ea42a213c7c24831bcfa53e40358f2  (PR=0  ,  Filename=spatial-data-types-overview.md  ,  Dirpath=docs\relational-databases\spatial\  ,  MergeCommitSha40=b33976cf92f23fbb13cee0c353fd40608d002d94) -->



 -  Há dois tipos de dados espaciais. O tipo de dados **geometry** dá suporte a dados planares ou a dados euclidianos (planisfério). O tipo de dados **geometry** está de acordo com os Recursos Simples do Open Geospatial Consortium (OGC) para o SQL Specification versão 1.1.0 e compatível com o SQL MM (padrão ISO).
 -
 - Além disso, ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] dá suporte ao tipo de dados **geography** que armazena dados elipsoidais (globo), como coordenadas de latitude e longitude de GPS.
 -
 -> [!IMPORTANT]
 -> Para obter uma descrição detalhada e exemplos de recursos espaciais apresentados no ..!NCLUDE-NotShown--ssSQL11--../../includes/sssql11-md.md)], incluindo aprimoramentos nos tipos de dados espaciais, baixe o white paper, [New Spatial Features in SQL Server Code-Named "Denali" (Novos Recursos Espaciais no SQL Server com Codinome "Denali")](http://go.microsoft.com/fwlink/?LinkId=226407).
 -
 -##  <a name="objects"></a> Objetos de Dados Espaciais
 - Os tipos de dados **geometry** e **geography** oferecem suporte a dezesseis objetos de dados espaciais, ou tipos de instâncias. No entanto, apenas onze desses tipos de instâncias *podem ser instanciados*. É possível criar e trabalhar com essas instâncias (ou criar uma instância delas) em um banco de dados. Essas instâncias derivam determinadas propriedades de seus tipos de dados pai que as distingue como **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** ou como instâncias **geometry** ou **geography** múltiplas em uma **GeometryCollection**. O tipo**Geography** tem um tipo de instância adicional, **FullGlobe**.
 -
 - A figura a seguir ilustra a hierarquia **geometry** na qual os tipos de dados **geometry** e **geography** se baseiam. Os tipos a partir dos quais se podem criar instâncias de **geometry** e **geography** são indicados em azul.
 -
 - ![geom_hierarchy--../../relational-databases/spatial/media/geom-hierarchy.gif)
 -
 - Como a figura indica, os dez tipos dos quais se pode criar uma instância dos tipos de dados **geometry** e **geography** são **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**e **GeometryCollection**. Há um tipo adicional do qual se pode criar uma instância para o tipo de dados de geography: **FullGlobe**. Os tipos **geometry** e **geography** podem reconhecer uma instância específica desde que ela esteja bem-formada, ainda que não esteja definida explicitamente. Por exemplo, se você definir uma instância de **Point** explicitamente usando o método STPointFromText(), **geometry** e **geography** a reconhecerão como uma instância de **Point**, desde que a entrada do método esteja bem formada. Se você definir a mesma instância usando o método `STGeomFromText()` , os tipos de dados **geometry** e **geography** reconhecem a instância como um **Point**.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (0 + 1): documentos sobre o **Advanced Analytics para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (0+1): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (4+1): documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (17+0): documentos sobre o **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (3+0): documentos sobre o **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (1+1): documentos sobre os **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (2+0): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (0+1): documentos sobre o **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0+1): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0 + 0): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (0 + 0): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (0 + 0): documentos do **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



