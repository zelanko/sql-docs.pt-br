---
title: "Atualizado – Documentos do Reporting Services para SQL Server | Microsoft Docs"
description: "Exiba trechos do conteúdo atualizado com alterações recentes na documentação do Reporting Services para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: reporting-services
ms.suite: pro-bi
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.author: genemi
ms.workload: reporting-services
ms.openlocfilehash: a4bb2b714a4a20d299c22e6952f135cd9786748c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>Novos e atualizados recentemente: Reporting Services para SQL Server



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de assunto:* &nbsp; **Reporting Services para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Log de alterações do SQL Server Reporting Services](change-log-sql-server-reporting-services.md)
2. [Desenvolver com as APIs REST para o Reporting Services](developer/rest-api.md)
3. [Web Part do Visualizador de Relatórios em um site do SharePoint](report-server-sharepoint/report-viewer-web-part-sharepoint-site.md)
4. [Configurações do site do SharePoint para a web part do Visualizador de Relatórios](report-server-sharepoint/report-viewer-web-part-sharepoint-site-settings.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Instalar o SQL Server Reporting Services](#TitleNum_1)
2. [Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-sql-server-reporting-servicesinstall-windowsinstall-reporting-servicesmd"></a>1. &nbsp; [Instalar o SQL Server Reporting Services](install-windows/install-reporting-services.md)

*Atualizado: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 66.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c959622d4d10a71ed598256e8e284130eb49af5b 77dc1b4f6696e911ed036fc27724ff8a96b79f57  (PR=4150  ,  Filename=install-reporting-services.md  ,  Dirpath=docs\reporting-services\install-windows\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    > The default path is C:\Program Files\Microsoft SQL Server Reporting Services.

7. Após uma instalação bem-sucedida, selecione **Configurar Servidor de Relatório** para iniciar o Gerenciador de Configurações do Reporting Services.

    ![Configurar o servidor de relatório--media/install-reporting-services/report-server-install-configure.png)

**Configuração do servidor de relatório**


Depois de selecionar **Configurar Servidor de Relatório** na instalação, você verá o **Gerenciador de Configurações do Servidor de Relatório**. Para obter mais informações, consulte [Report Server Configuration Manager--reporting-services-configuration-manager-native-mode.md).

Você precisa [criar um banco de dados do servidor de relatório--ssrs-report-server-create-a-report-server-database.md) para concluir a configuração inicial do Reporting Services. Um servidor de Banco de Dados do SQL Server é necessário para concluir esta etapa.

**Criando um banco de dados em um servidor diferente**


Caso você esteja criando o banco de dados do servidor de relatório em um servidor de banco de dados em outro computador, precisará alterar a conta de serviço do servidor de relatório para uma credencial que é reconhecida no servidor de banco de dados.

Por padrão, o servidor de relatório usa a conta de serviço virtual. Se você tentar criar um banco de dados em outro servidor, poderá receber o erro a seguir durante a etapa Aplicando direitos de conexão.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Para solucionar o erro, altere a conta de serviço para Serviço de Rede ou uma conta de domínio. A alteração da conta de serviço para Serviço de Rede aplica os direitos no contexto da conta do computador do servidor de relatório.

Para obter mais informações, consulte [Configurar a conta de serviço do servidor de relatório--configure-the-report-server-service-account-ssrs-configuration-manager.md).

**Serviço Windows**


Um serviço Windows é criado como parte da instalação. Ele é exibido como **SQL Server Reporting Services**. O nome do serviço é **SQLServerReportingServices**.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2. &nbsp; [Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint](report-server-sharepoint/deploy-report-viewer-web-part.md)

*Atualizado: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 129.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 99275aa597f491bb09688060b3f713406e2f0624 a282486da6df55154212c98fa06c7e62e66c8350  (PR=4150  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



A tentativa de exclusão da web part pode ser feita usando o PowerShell, mas não há um comando direto para isso. Para obter um exemplo de script, consulte [Como excluir web parts da Galeria de web parts](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

**Idiomas compatíveis**


Há suporte para os seguintes idiomas com a web part:

* Inglês (en)
* Alemão (de)
* Espanhol (sp)
* Francês (fr)
* Italiano (it)
* Japonês (ja)
* Coreano (ko)
* Português (pt)
* Russo (ru)
* Chinês (simplificado – zh-HANS e zh-CHS)







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 14): documentos sobre **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (87 + 0): documentos sobre **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (5 + 4): documentos sobre **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1): documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (2 + 2): documentos sobre **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (10 + 9): documentos sobre **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (2 + 4): documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (4 + 2): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (0 + 1): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (21 + 0): documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (5 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1 + 0): documentos sobre o **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


