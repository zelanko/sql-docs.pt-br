---
title: Atualizado – Documentos do Reporting Services para SQL Server | Microsoft Docs
description: Exiba trechos do conteúdo atualizado com alterações recentes na documentação do Reporting Services para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssrs
ms.date: 04/28/2018
ms.openlocfilehash: 5fc0153c45e12f8cef47ef2b9eef10f73343b87e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>Novos e atualizados recentemente: Reporting Services para SQL Server



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **Reporting Services para SQL Server**.




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

1. [Log de alterações do SQL Server Reporting Services](#TitleNum_1)
2. [Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-change-log-for-sql-server-reporting-serviceschange-log-sql-server-reporting-servicesmd"></a>1. &nbsp; [Log de alterações do SQL Server Reporting Services](change-log-sql-server-reporting-services.md)

*Atualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "edugonz".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025d58c01310215df423e7c3848e929b935bcfff 89310524b904dfba41e301cf1323b9a2a5e05064  (PR=575  ,  Filename=change-log-sql-server-reporting-services.md  ,  Dirpath=docs\reporting-services\  ,  MergeCommitSha40=98b04e2388872d1c7b8d819438c150c4ff2df94c) -->




- *Versão 14.0.600.744, Lançamento: 25 de abril de 2018*
    - Correções de bug:
        - A página de assinatura controlada por dados não mostra a opção de entrega quando ela é criada
        - O upgrade do SSRS 2012 para o SSRS 2017 no RSManagement rseulta na geração de uma exceção em intervalos de poucos segundos
        - Não é possível alterar os valores padrão para parâmetros de vários valores no IE11
        - As agendas ficam vazias sempre que a agenda compartilhada é executada

- *Versão 14.0.600.689, lançada em: 28 de fevereiro de 2018*
    - Correções de bug:
        - A visibilidade do Parâmetro de Relatório em um relatório vinculado é revertida após a edição das respectivas propriedades
        - O Parâmetro de URL rc:Toolbar=false não funciona na Express Edition
        - Colocar expressões na caixa de texto com a propriedade CanGrow definida como false faz com que os valores não sejam exibidos
        - Link "Saiba mais" adicionado à chave do produto (Product Key) na instalação
        - O portal da Web com autenticação de formulários personalizados está ignorando os cookies de sliding expiration
        - Exportar para o Word cria linhas com alturas diferentes, quando o conteúdo de uma linha está vazio



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2. &nbsp; [Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint](report-server-sharepoint/deploy-report-viewer-web-part.md)

*Atualizado: 10-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 154.  ms.author= "maghan".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 42b763a610d378a7cedc9b5778bc5048d65fa730 ce7e2619689fd50be51a2689b07e3137470d9adf  (PR=5481  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=31e0b2ebfc08c0b57870ac412fbd49bf3a1dffb8) -->



**Solucionar problemas**


* Erro ao desinstalar o SSRS se você configurou o modo integrado do SharePoint:

    Install-SPRSService : [A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService não pode ser convertido em [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService. O Tipo A é proveniente de 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' no contexto 'Default' e no local 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'. O Tipo B é proveniente de 'Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' no contexto 'Default' e no local 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'.

    Solução:
    1. Remover a web part do Visualizador de Relatórios
    2. Desinstalar o SSRS
    3. Reinstalar a web part do Visualizador de Relatórios

* Erro ao tentar atualizar o SharePoint se você configurou o modo integrado do SharePoint:

    Não foi possível carregar o arquivo ou o assembly 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado. 00000000-0000-0000-0000-000000000000

    Solução:
    1. Remover a web part do Visualizador de Relatórios
    2. Desinstalar o SSRS
    3. Reinstalar a web part do Visualizador de Relatórios







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

