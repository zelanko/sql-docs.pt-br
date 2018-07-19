---
title: Atualizado — Documentos do SQL Server | Microsoft Docs
description: Exibir trechos de conteúdo atualizado para documentação do SQL Server alterada recentemente.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.date: 04/28/2018
ms.openlocfilehash: f1e3d0fd2b63ac3eb9ab0d66b14df15dad0c15ee
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926817"
---
# <a name="new-and-recently-updated-sql-server-docs"></a>Novos e recém-atualizados: documentos do SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Como contribuir com a documentação do SQL Server](sql-server-docs-contribute.md)
2. [Suplemento de privacidade do SQL Server](sql-server-privacy.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Notas de Versão do Service Pack do SQL Server 2012](#TitleNum_1)
2. [Notas de Versão do SQL Server 2016.](#TitleNum_2)
3. [SQL Server, documentação](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2012-service-pack-release-notessql-server-2012-sp4-release-notesmd"></a>1. &nbsp; [Notas de versão do SQL Server 2012 Service Pack](sql-server-2012-sp4-release-notes.md)

*Atualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 57.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ce108992ea942b4a11f30d67a1a52d7f26868caa a6269ba2cb2d3b3b54aebf5087dc4d513e476a96  (PR=5676  ,  Filename=sql-server-2012-sp4-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- **Particionamento do soft-NUMA automático** – com o SQL 2014 SP2, o particionamento [Soft-NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) automático é introduzido quando o sinalizador de rastreamento 8079 é habilitado no nível do servidor. Quando o Sinalizador de rastreamento 8079 é habilitado durante a inicialização, o SQL Server 2014 SP2 interroga o layout de hardware e configura automaticamente o soft-NUMA em sistemas que reportam oito ou mais CPUs por nó NUMA. O comportamento do soft-NUMa automático tem reconhecimento de hyperthread (HT/processador lógico). O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável testar primeiro o desempenho da carga de trabalho com o soft-NUMA automático antes que ele seja ATIVADO na produção.

**Notas de versão do Service Pack 3**


**Páginas de download**

- [Feature Pack do SQL Server 2012 SP3](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

Para obter mais informações detalhadas para identificar o local e o nome do arquivo a ser baixado com base na versão instalada no momento, consulte a seção “Selecionar o arquivo correto a ser baixado” em [Informações de versão do SQL Server 2012 Service Pack 3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information).

**Notas de versão do Service Pack 2**


**Páginas de download**

- [Feature Pack do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

Use a tabela abaixo para identificar o local e o nome do arquivo a ser baixado com base em sua versão atualmente instalada. As páginas de download têm requisitos de sistema e instruções básicas de instalação.

| Se sua versão instalada atual for.... | E você quiser... | Baixe e instale... |



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-2016-release-notessql-server-2016-release-notesmd"></a>2. &nbsp; [Notas de versão do SQL Server 2016](sql-server-2016-release-notes.md)

*Atualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Próximo](#TitleNum_3))

<!-- Source markdown line 25.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a15210866acf524dae49f3a7fd7957c9ffa6a78a 7257cb2017779242cbb8fa2b562f4b102502e942  (PR=5695  ,  Filename=sql-server-2016-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->



  Este artigo descreve as limitações e os problemas com as versões do SQL Server 2016, incluindo service packs. Para obter informações sobre as novidades, veja [Novidades no SQL Server 2016](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016).

- Baixar o SQL Server 2016 do **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
- Máquina Virtual pequena do Azure: Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** para criar uma Máquina Virtual com o SQL Server 2016 SP1 já está instalado.
- Baixar o SSMS: para obter a versão mais recente do SQL Server Management Studio, veja **[Baixar o SSMS (SQL Server Management Studio)]**.

**<a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)**


O SQL Server 2016 SP2 inclui todas as atualizações cumulativas liberadas após SP1 2016, até e incluindo CU8.

- [Download do Microsoft SQL Server 2016 Service Pack 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- Para obter uma lista completa de atualizações, veja [informações de versão do SQL Server 2016 Service Pack 2](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-documentationsql-server-technical-documentationmd"></a>3. &nbsp; [SQL Server, documentação](sql-server-technical-documentation.md)

*Atualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2))

<!-- Source markdown line 77.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0262010ba39785a6d46b42f8469fb17701f13008 c69a83236391d039381a93c65ebbb2efa53e11b8  (PR=5695  ,  Filename=sql-server-technical-documentation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->




<!-- : : : m-r -->
**Experimente o SQL Server!**
- Baixar no Centro de Avaliação: [Baixar o SQL Server para Windows](http://go.microsoft.com/fwlink/?LinkID=829477)
- Baixar no Centro de Avaliação: Baixar o SSMS (SQL Server Management Studio)
- Baixar no Centro de Avaliação: Baixar o SSDT (SQL Server Data Tools)
- Criar uma máquina virtual: [Criar uma máquina virtual com o SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)





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

