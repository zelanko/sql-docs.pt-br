---
title: Atualizado - documentos Analytics Platform System | Microsoft Docs
description: Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o sistema de plataforma de análise do Microsoft SQL Server.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 94b7666476874e610991ebf838ad259f3d0bb85a
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="new-and-recently-updated-analytics-platform-system-for-sql-server"></a>Novos e atualizados recentemente: Analytics Platform System para SQL Server

Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **03-12-2017** &nbsp; até &nbsp; **03-02-2018**
- *Área de assunto:* &nbsp; **Analytics Platform System para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


***Não existem novos artigos a serem listados, no momento.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Configurar a conectividade do PolyBase para dados externos](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-polybase-connectivity-to-external-dataconfigure-polybase-connectivity-to-external-datamd"></a>1. &nbsp; [Configurar a conectividade do PolyBase para dados externos](configure-polybase-connectivity-to-external-data.md)

*Atualizado: 29-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 132.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 947f789480da66b9f636f39b30caec6be60d8c4d d4d4d45fbbb8e10ed6f26fe12f9a25d2e8e4f068  (PR=4741  ,  Filename=configure-polybase-connectivity-to-external-data.md  ,  Dirpath=docs\analytics-platform-system\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**Configuração do Kerberos**

Observe que, quando o PolyBase é autenticado para um cluster protegido Kerberos, a configuração hadoop.rpc.protection deve ser definida para autenticação. Isso faz com que a comunicação de dados entre os nós do Hadoop não seja criptografada.

 Para se conectar a um cluster Hadoop protegido por Kerberos [usando MIT KDC]:


1.  Localize o diretório de configuração do Hadoop no caminho de instalação no nó de controle:

    ```
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```

2.  Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)

3.  Copie os valores de configuração para a propriedade de valor nos arquivos correspondentes no nó de controle.

    |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|
    |------------|----------------|---------------------|----------|
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|
    |2|core-site.xml|polybase.kerberos.realm|Especifique o realm do Kerberos. Por exemplo: YOUR-REALM.COM|
    |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|
    |6|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: 10.193.26.174:10020|
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: yarn/_HOST@YOUR-REALM.COM|







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
- [Novo + atualizado (0 + 0): **ActiveX Data Objects (ADO) para o SQL** documentos](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)


