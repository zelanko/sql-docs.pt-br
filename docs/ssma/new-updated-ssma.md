---
title: Atualizado - SSMA para documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para SQL Server SSMA (Migration Assistant) para o Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssma-sql-server-migration-assistant
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 68df82bc7da6d7ef5aed3522c06704fb92bb0982
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-migration-assistant-ssma"></a>Novos e atualizados recentemente: SQL Server Migration Assistant (SSMA)



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-07-18** &nbsp; - para - &nbsp; **2017-09-11**
- *Área de assunto:* &nbsp; **SQL Server Migration Assistant**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir saltar para novos artigos que foram adicionados recentemente.


***Não existem novos artigos a serem listados no momento.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção foram extraídas.

1. [O que &#39; s do SSMA para DB2 (DB2ToSQL)](#TitleNum_1)
2. [Assistente de Migração do SQL Server](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-ssma-for-db2-db2tosqldb2what-s-new-in-ssma-for-db2-db2tosqlmd"></a>1. &nbsp;[Qual &#39; s do SSMA para DB2 (DB2ToSQL)](db2/what-s-new-in-ssma-for-db2-db2tosql.md)

*Atualizado em: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 24.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5dfb378ac578f54935a8a1fa7194398f3631017 f4427d1857894ad348cef5c92fbf6b51d00ee652  (PR=3070  ,  Filename=what-s-new-in-ssma-for-db2-db2tosql.md  ,  Dirpath=docs\ssma\db2\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**V 7.4 do SSMA**

A versão v 7.4 do SSMA for DB2 contém as seguintes alterações:
- O **tempo limite da consulta** opção agora está disponível durante a descoberta de objeto de esquema na origem e no destino.
! [opção de tempo limite de consulta –... /Media/Query-timeout_red.png)

- A métrica de qualidade e a conversão foi aprimorada com correções de destino, com base nos comentários dos clientes.

> [!IMPORTANT]
> O .net 4.5.2 é um pré-requisito de instalação v 7.4 do SSMA. Além disso, começando com v 7.4, a versão de 32 bits do SSMA está sendo descontinuada.

**O SSMA 7.3**

A versão 7.3 do SSMA for DB2 contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Estrutura de extensibilidade do SSMA exposta por meio de itens a seguir:
  - Exporte funcionalidade a um projeto do SQL Server Data Tools (SSDT).
    -   Agora você pode exportar os scripts de esquema do SSMA para um projeto do SSDT. Você pode usar os scripts de esquema para fazer alterações de esquema adicionais e implantar seu banco de dados.
! [Salvar como comando de projeto do SSDT-... /Media/Export-Schema-scripts_red.png)
  - Bibliotecas que podem ser consumidas por SSMA para realizar conversões personalizados.
    - Agora você pode construir o código que pode lidar com conversões de sintaxe personalizada e conversões que anteriormente não foram manipulados por SSMA.
      - Instruções sobre como construir um conversor personalizado estão disponíveis nesta postagem de blog, [recursos de conversão do estendendo o SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Projeto de exemplo para a conversão pode ser baixar este [postagem de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

**V 7.2 do SSMA**

A versão v 7.2 do SSMA for DB2 contém as seguintes alterações:
- Métrica de qualidade e conversão aprimorada com correções de destino com base nos comentários dos clientes.
- Aprimoramentos de telemetria para fornecer melhor pontos de dados para solucionar problemas do cliente e melhorar as taxas de conversão do SSMA.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-migration-assistantsql-server-migration-assistantmd"></a>2. &nbsp;[Assistente de migração do SQL Server](sql-server-migration-assistant.md)

*Atualizado em: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 36.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 340d718e85fa73c6722862a0a7ba90239b247389 b29f4be2b6d208fd6038c2f9e1c7f0b7bd6b9ed7  (PR=3070  ,  Filename=sql-server-migration-assistant.md  ,  Dirpath=docs\ssma\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**Fontes com suporte e versões de destino**

Para fontes com suporte, revise as informações no Centro de Download para baixar o SSMA.

As seguintes versões de destino têm suporte para o SSMA.

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Banco de dados SQL do Azure
- SQL Server 2017 no Windows e Linux (visualização)
- * * Do azure SQL Data Warehouse

* * Este destino só é suportado por SSMA para Oracle.









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



