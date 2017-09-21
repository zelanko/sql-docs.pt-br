---
title: "Atualizado – documentos do SSMS para SQL Server | Microsoft Docs"
description: "Trechos de exibição de conteúdo atualizado com alterações recentes na documentação, para o SSMS (SQL Server Management Studio) para Microsoft SQL Server."
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
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Novos e atualizados recentemente: SSMS (SQL Server Management Studio) para SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **18-07-2017** &nbsp; até &nbsp; **11-09-2017**
- *Área de assunto:* &nbsp; **SSMS (SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Janela de Saída no SQL Server Management Studio](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma grande atualização recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Baixar o SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [Conectar ao SQL Server ou ao Banco de Dados SQL do Azure](#TitleNum_2)
3. [SQL Server Management Studio – Changelog (SSMS)](#TitleNum_3)
4. [Criar e atualizar tabelas de banco de dados](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp;[Baixar o SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Atualizado: 2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Próximo](#TitleNum_2))

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



O SMS 17.2 é a versão mais recente do SQL Server Management Studio. A geração 17.X do SSMS oferece suporte a quase todas as áreas de recursos do SQL Server 2008 por meio do SQL Server 2017. A Versão 17.x também oferece suporte ao PaaS do SQL Analysis Service.

A versão 17.2 inclui:

- MFA (Autenticação Multifator do Microsoft Azure)
  - Autenticação de vários usuários do Azure AD para Autenticação universal com Autenticação Multifator do Microsoft Azure (UA com MFA)
  - Foi adicionado um novo campo de entrada de credenciais do usuário para autenticação Universal com MFA para oferecer suporte à autenticação de vários usuários.
- A caixa de diálogo de conexão agora oferece suporte aos 5 seguintes métodos de autenticação:
  - Autenticação do Windows
  - Autenticação do SQL Server
  - Active Directory – Universal com suporte à MFA
  - Active Directory – Senha
  - Active Directory – Integrado

- A exportação/importação do banco de dados para o assistente de DacFx agora pode usar a Autenticação universal com MFA.
- Para suporte de API, consulte a [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Biblioteca ADAL gerenciada usada pela Autenticação universal do Azure AD com MFA foi atualizada para a versão 3.13.9.
- Uma nova interface de CLI com suporte para a configuração de administrador do Azure AD para o banco de dados SQL e SQL Data Warehouse.

 Para obter mais informações sobre os métodos de autenticação do Active Directory, consulte [Autenticação universal com o banco de dados SQL e SQL Data Warehouse (suporte de SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) e [configure a autenticação multifator do Banco de Dados SQL do Azure para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- A janela de saída tem entradas para consultas executadas durante a expansão de nós do Pesquisador de Objetos do SQL Server
- Designer de exibição para os Bancos de dados SQL do Azure habilitado
- As opções de script padrão para gerar scripts de objetos no Pesquisador de Objetos do SQL Server no SSMS foram alteradas:



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2. &nbsp; [Conectar ao SQL Server ou ao Banco de Dados SQL do Azure](object/connect-to-an-instance-from-object-explorer.md)

*Atualizado: 2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_1) | [Próximo](#TitleNum_3))

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![firewall--../media/connect-to-server/new-firewall-rule.png)

1. Para criar a regra de firewall e conectar-se ao servidor, clique em **OK**.

1. Após a conexão ser bem-sucedida, o servidor aparecerá no **Pesquisador de Objetos**:

   ![connected--../media/connect-to-server/connected.png)

**Próximas etapas**


[Design, Create, and Update Tables--../visual-db-tools/design-tables-visual-database-tools.md)

**Confira também**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [Download SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3. &nbsp; [SQL Server Management Studio – Log de alterações (SSMS)](sql-server-management-studio-changelog-ssms.md)

*Atualizado: 2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_2) | [Próximo](#TitleNum_4))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



Este artigo fornece detalhes sobre atualizações, aprimoramentos e correções de bug para as versões atuais e anteriores do SSMS. Download [previous SSMS versions below--#previous-ssms-releases).

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


Disponibilidade geral | Número de build: 14.0.17177.0

**Aprimoramentos**


- MFA (Autenticação Multifator do Microsoft Azure)
  - Autenticação de vários usuários do Azure AD para autenticação Universal com Autenticação Multifator do Microsoft Azure (UA com MFA)
  - Foi adicionado um novo campo de entrada de credenciais do usuário para autenticação Universal com MFA para oferecer suporte à autenticação de vários usuários.
- A caixa de diálogo de conexão agora oferece suporte aos 5 seguintes métodos de autenticação:
  - Autenticação do Windows
  - Autenticação do SQL Server
  - Active Directory – Universal com suporte à MFA
  - Active Directory – Senha
  - Active Directory – Integrado

- Exportação/importação do banco de dados para o assistente de DacFx usando a Autenticação universal com MFA.
- Para suporte de API, consulte a [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Biblioteca ADAL gerenciada usada pela Autenticação universal do Azure AD com MFA foi atualizada para a versão 3.13.9.
- Além disso, uma nova interface de CLI foi entregue com suporte para a configuração de administrador do Azure AD para o banco de dados SQL e SQL Data Warehouse.

 Para obter mais informações sobre os métodos de autenticação do Active Directory, consulte [Autenticação universal com o banco de dados SQL e SQL Data Warehouse (suporte de SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) e [configure a autenticação multifator do Banco de Dados SQL do Azure para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- A janela de saída tem entradas para consultas executadas durante a expansão de nós do Pesquisador de Objetos do SQL Server



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4. &nbsp; [Criar e atualizar tabelas de banco de dados](visual-db-tools/design-tables-visual-database-tools.md)

*Atualizado: 2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_3))

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**Criar uma tabela**


1. Clique com o botão direito do mouse no nó **Tabelas** do banco de dados e selecione **Nova** > **Tabela**:

    ![New table--../media/design-tables/new-table.png)

1. Add [columns--column-properties-visual-database-tools.md) to your table:

    ![design table--../media/design-tables/new-table2.png)

1. Feche o Designer e salve as alterações.

**Atualizar uma tabela**


1. Clique com o botão direito do mouse no nó **Tabelas** do banco de dados e selecione **Criar**:

   ![Update table--../media/design-tables/update-table.png)

1. Atualize as configurações desejadas da tabela:

   ![--../media/design-tables/update-table2.png)

1. Feche o Designer e salve as alterações.

**Confira também**


[Tabelas](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [Table Properties &#40;Visual Database Tools&#41;--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [Column Properties--column-properties-visual-database-tools.md) [Add Columns to a Table--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [Primary and Foreign Keys--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Indexes--../../relational-databases/indexes/indexes.md) [Data types (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [Download SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista os artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, dentro do nosso repositório GitHub.com: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 12): documentos de **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (5 + 0): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (5 + 1): documentos do **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (19 + 82): documentos do **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (1 + 8): documentos do **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (12 + 1): documentos de **Bancos de Dados Relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (0 + 1): documentos do **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (7 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (1 + 1): documentos do **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 2): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (1 + 4): documentos do **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (4 + 1): documentos do **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (0 + 1): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0 + 0): documentos do **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



