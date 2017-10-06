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
ms.date: 09/27/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: dc4a5516662b200b4224facbb4c9cf4588c1b42e
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-database-engine-docs"></a>Novo e atualizado recentemente: Documentos do Mecanismo de Banco de Dados



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **11-09-2017** &nbsp; até &nbsp; **27-09-2017**
- *Área de assunto:* &nbsp; **Mecanismo de Banco de Dados**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Adicionar recursos a uma instância do SQL Server (instalação)](install-windows/add-features-to-an-instance-of-sql-server-setup.md)
2. [Instalar o SQL Server do prompt de comando](install-windows/install-sql-server-from-the-command-prompt.md)
3. [Instalar o SQL Server usando um arquivo de configuração](install-windows/install-sql-server-using-a-configuration-file.md)
4. [Recuperação de banco de dados e continuidade dos negócios – SQL Server](sql-server-business-continuity-dr.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Instalar atualizações do prompt de comando](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-installing-updates-from-the-command-promptinstall-windowsinstalling-updates-from-the-command-promptmd"></a>1. &nbsp; [Instalando Atualizações no Prompt de Comando](install-windows/installing-updates-from-the-command-prompt.md)

*Atualizado: 12-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 48.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 04abb23d0682c23654a55e7926d2140f0b6ae408 a4bb1e27ae99460a66da72848ace1417b148f85c  (PR=3122  ,  Filename=installing-updates-from-the-command-prompt.md  ,  Dirpath=docs\database-engine\install-windows\  ,  MergeCommitSha40=1df54edd5857ac2816fa4b164d268835d9713638) -->



- Atualize todas as instâncias de ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] no computador e todos os componentes compartilhados, como ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] e Ferramentas de Gerenciamento:

```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.
```

- Remova uma atualização de uma instância única do ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] e todos os componentes compartilhados, como ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] e Ferramentas de Gerenciamento:

```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.
```

- Remova somente uma atualização do ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] e todos os componentes compartilhados, como ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] e Ferramentas de Gerenciamento:

```
    <package_name>.exe /qs /Action=RemovePatch
```







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



