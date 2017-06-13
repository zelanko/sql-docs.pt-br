---
title: Atualizado - documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, do SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: pt-br
ms.lasthandoff: 05/25/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>Novos e recentemente atualizado: documentos do SQL Server



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-05-01** &nbsp; - para - &nbsp; **2017-05-23**
- *Área de assunto:* &nbsp; **do SQL Server**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp;[Notas de versão do SQL Server de 2017](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**2017 CTP 2.1 (maio de 2017) do SQL Server**

**Documentação (CTP 2.1)**

- **Impacto do problema e o cliente:** documentação para [! INCLUIR [ssSQLv14_md-... /Includes/sssqlv14-MD.MD]) é limitado e conteúdo está incluído com a [! INCLUIR [ssSQL15_md-... conjunto de documentação /Includes/sssql15-MD.MD]).  Conteúdo em artigos que é específico para [! INCLUIR [ssSQLv14_md-... /Includes/sssqlv14-MD.MD)] será anotado com **aplica-se a**. 
- **Impacto do problema e o cliente:** nenhum conteúdo offline está disponível para [! INCLUIR [ssSQLv14_md-... /Includes/sssqlv14-MD.MD)].

**SQL Server Reporting Services (CTP 2.1)**


- **Impacto do problema e o cliente:** se você tiver o SQL Server Reporting Services e Power BI servidor de relatório no mesmo computador e desinstale um deles, você não poderá se conectar ao servidor de relatório restantes com o Gerenciador de configuração de servidor de relatório.
- **Solução alternativa** para contornar esse problema, você deve executar as seguintes operações depois de desinstalar um dos servidores.

    1. Inicie um prompt de comando no modo de administrador.
    2. Vá para o diretório onde o servidor restante do relatório está instalado.

        *Local padrão para o servidor de relatório do Power BI: o servidor de relatório do C:\Program Files\Microsoft Power BI*

        *Local padrão para o SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. Em seguida, vá para a próxima pasta. Isso será *SSRS* ou *PBIRS* dependendo de qual é restantes.
    4. Vá para a pasta WMI.
    5. Execute o seguinte comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Você pode ignorar o erro a seguir, se você vê-lo.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP 2.1)**


- **Impacto do problema e o cliente:** depois de instalar em um computador que tenha uma versão de 2016 do *TSqlLanguageService.msi* instalado (por meio da instalação do SQL ou autônomos redistribuível) as versões v13.* (SQL 2016) *Microsoft.SqlServer.Management.SqlParser.dll* e *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* são removidos. Os aplicativos que têm uma dependência nas versões 2016 desses assemblies, em seguida, deixará de funcionar, fornecendo um erro semelhante a: *erro: não foi possível carregar arquivo ou assembly ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2. &nbsp;[Qual &#39; s no SQL Server de 2017](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**Novidades no SQL Server de 2017 CTP 2.1 (maio de 2017)**

* * Mecanismo de banco de dados do servidor SQL * *

- Um novo DMF, [sys.dm_db_log_stats-... / relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), foi introduzido para expor atributos de nível de resumos e obter informações sobre arquivos de log de transações; útil para monitorar a integridade do log de transações.  
- Este CTP contém correções e melhorias de desempenho para o mecanismo de banco de dados.
- Para obter uma lista detalhada de 2017 aprimoramentos do CTP em versões anteriores do CTP, consulte [Novidades no SQL Server 2017 (mecanismo de banco de dados –)... / database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

**SQL Server Reporting Services (SSRS)**

- SQL Server Reporting Services não está mais disponível para instalar por meio da instalação do SQL Server a partir do CTP 2.1.
- Comentários agora estão disponíveis para relatórios. Comentários que você adicionar perspectiva ao que está em um relatório e colaborar com outras pessoas em sua organização. Você também pode incluir os anexos com o seu comentário.
- Para o SSRS mais detalhadas novidades, incluindo detalhes de versões anteriores, consulte [Novidades no Reporting Services-... / reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Para obter informações sobre o servidor de relatório do Power BI, consulte [Introdução ao servidor de relatório do Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

**Serviços de aprendizado de máquina do SQL Server**

- Não há recursos novos serviços de aprendizado de máquina neste CTP.
- Serviços de aprendizado de máquina mais detalhadas novidades, incluindo detalhes de CTPs anteriores, consulte [o que há de novo no SQL Server Machine Learning Services--... / advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

**SQL Server Analysis Services (SSAS)**

- Não há recursos novos do SSAS neste CTP.  
- Para obter mais detalhes sobre melhorias e correções nesta versão, consulte [Novidades no SQL Server de 2017 Analysis Services--... / analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção anterior.

1. [Notas de versão do SQL Server de 2017](#TitleNum_1)
2. [O que &#39; s no SQL Server de 2017](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Artigos irmã

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.


&nbsp;

[Microsoft /**sql de documentos de pr** ](https://github.com/microsoftdocs/sql-docs-pr/) repositório em GitHub.com:

- [Atualizado recentemente: **bancos de dados relacionais e o Microsoft SQL Server** documentos](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Atualizado recentemente: **Microsoft SQL Server** documentos](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Atualizado recentemente: **Transact-SQL no SQL Server** documentos](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



