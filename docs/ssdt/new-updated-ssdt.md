---
title: Atualizado – documentos do SSDT para SQL Server | Microsoft Docs
description: Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para SSDT (SQL Server Data Tools) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 02/03/2018
ms.openlocfilehash: ad139f5ff9389c1a04a7f077d61facc7643db323
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Novos e atualizados recentemente: SSDT (SQL Server Data Tools)



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-12-2017** &nbsp; até &nbsp; **03-02-2018**
- *Área de assunto:* &nbsp; **SSDT (SQL Server Data Tools)**.




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

1. [Log de alterações do SSDT (SQL Server Data Tools)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Log de alterações do SSDT (SQL Server Data Tools)](changelog-for-sql-server-data-tools-ssdt.md)

*Atualizado: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6416949beaee91da2f77dfebb9eb5ed363db4cb7 de18314845cffa197b3fd2ed868f2c330760bedb  (PR=4652  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**SSDT para Visual Studio 2017 (15.5.1)**

Número de build: 14.0.16148.0

**Novidades**


O Visual Studio 2017 (15.5.1) é a mesma versão da versão 15.5.0, com exceção das seguintes correções de bug no instalador:

1.  Correção de um problema no qual o instalador trava na pós-instalação do SQL Server Integration Services.
2.  Correção de um problema no qual a instalação falha com a seguinte mensagem de erro: “Não há suporte para a operação de metarquivo solicitada (0x800707D3)”.

Além dessas duas correções de bug, os seguintes detalhes do 15.5.0 ainda se aplicam ao 15.5.1

**SSDT para Visual Studio 2017 (15.5.0)**

Número de build: 14.0.16146.0

**Novidades**


O SSDT para Visual Studio 2017 (15.5.0) passa da versão prévia para GA (disponibilidade geral).

**Instalador**
1. A interface do usuário da instalação está localizada.
1. Substitua o ícone por uma versão de qualidade superior.

**IS (Integration Services)**
1. Adição de uma etapa de validação de pacote no Assistente de Implantação ao implantar o Azure SSIS IR no ADF, que detecta problemas de compatibilidade potenciais em pacotes do SSIS a serem executados no Azure SSIS IR. Para obter mais informações, consulte [Validar pacotes do SSIS implantados no Azure](..\integration-services\lift-shift\ssis-azure-validate-packages.md).
1. A extensão do SSIS está localizada.

**Correções de bugs**


**IS (Integration Services)**
1. Correção de um problema no qual o layout do gerenciador de conexões OLEDB e ADO.NET está corrompido.
2. Correção de um problema no qual um erro de assembly não encontrado é acionado durante a tentativa de editar uma Tarefa de Processamento de Dimensão.

**Problemas conhecidos**


**IS (Integration Services)** A Tarefa Executar Pacote do SSIS não dá suporte à depuração quando ExecuteOutOfProcess está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.



**SSDT 17.4 para Visual Studio 2015**

Número de build: 14.0.61712.050

**Novidades**


**Projetos do AS (Analysis Services)**
- Adição de três novas opções aos projetos de tabela (em Opções > Tabela do Analysis Services > Importação de Dados):







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


