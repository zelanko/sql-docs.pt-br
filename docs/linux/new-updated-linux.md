---
title: Atualizado - SQL Server no Linux documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Microsoft SQL Server no Linux."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: sql-linux,UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: 
ms.date: 02/03/2018
ms.openlocfilehash: 827399587a8147c59caf6bf31bf8b10f10c83211
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Novos e recentemente atualizado: SQL Server no Linux docs



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-12-03** &nbsp; - para - &nbsp; **2018-02-03**
- *Área de assunto:* &nbsp; **Microsoft SQL Server no Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Configurar várias sub-redes grupos de disponibilidade AlwaysOn e instâncias de cluster de failover](sql-server-linux-configure-multiple-subnet.md)
2. [Criar e configurar um grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-create-availability-group.md)
3. [Implantar um cluster de Pacemaker para o SQL Server no Linux](sql-server-linux-deploy-pacemaker-cluster.md)
4. [SQL Server no Linux perguntas frequentes (FAQ)](sql-server-linux-faq.md)
5. [Noções básicas de disponibilidade do SQL Server para implantações do Linux](sql-server-linux-ha-basics.md)
6. [Configurar um contêiner do SQL Server no Kubernetes para alta disponibilidade](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Sempre em grupos de disponibilidade no Linux](#TitleNum_1)
2. [Extrair, transformar e carregar dados em Linux com o SSIS](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1. &nbsp;[Sempre em grupos de disponibilidade no Linux](sql-server-linux-availability-group-overview.md)

*Atualizado em: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



Failover automático de um grupo de disponibilidade é possível quando as seguintes condições forem atendidas:

-   O principal e a réplica secundária são definidos como a movimentação de dados síncrono.
-   O secundário tem um estado de sincronização (não Sincronizando), que significa que as duas estejam no mesmo ponto de dados.
-   O tipo de cluster é definido como externo. Failover automático não é possível com um tipo de cluster de None.
-   O `sequence_number` da réplica secundária se torne o primário tem o maior número de sequência – em outras palavras, a réplica secundária `sequence_number` corresponde da réplica primária original.

Se essas condições forem atendidas e o servidor que hospeda a réplica primária falha, o grupo de disponibilidade irá alterar a propriedade a uma réplica de síncrona. O comportamento de réplicas síncronas (do qual pode haver três total: uma primária e duas réplicas secundárias) adicional pode ser controlado por `required_synchronized_secondaries_to_commit`. Isso funciona com grupos de disponibilidade no Windows e Linux, mas será configurado completamente diferente. No Linux, o valor é configurado automaticamente pelo cluster no próprio recurso AG.

**Quorum e réplica somente configuração**


Também novo no SQL Server 2017 a partir de CU1 é uma réplica somente para configuração. Como Pacemaker é diferente de um WSFC, especialmente quando se trata de quorum e exigindo STONITH, ter apenas uma configuração de dois nós não funcionará quando se trata de um grupo de disponibilidade. Para uma FCI, os mecanismos de quorum fornecidos pelo Pacemaker podem ser bem, porque todos os arbitragem de failover FCI ocorre na camada do cluster. Para um grupo de disponibilidade, arbitragem em Linux ocorre no SQL Server, onde todos os metadados são armazenados. Isso é que a réplica somente configuração entra em cena.

Sem qualquer outra coisa, um terceiro nó e pelo menos uma réplica sincronizada seria necessárias. Isso não funcionaria para SQL Server Standard, pois ele pode ter apenas duas réplicas que participa de um grupo de disponibilidade. A réplica somente configuração armazena a configuração do grupo de disponibilidade no banco de dados mestre, mesmo que outras réplicas na configuração do grupo de disponibilidade. A réplica somente configuração não tem os bancos de dados de usuário participam do grupo de disponibilidade. Os dados de configuração são enviados de forma síncrona do primário. Esses dados de configuração, em seguida, são usados durante failovers, independentemente de estarem automática ou manual.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2. &nbsp;[Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

*Atualizado em: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Especifique o `/de[crypt]` opção para digitar a senha interativamente, conforme mostrado no exemplo a seguir:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  Especifique o `/de` opção para fornecer a senha na linha de comando, conforme mostrado no exemplo a seguir. Esse método não é recomendado porque ele armazena a senha de descriptografia com o comando no histórico de comandos.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**Criar pacotes**


**Conecte-se a fontes de dados ODBC**. Com o SSIS, sobre a atualização do Linux CTP 2.1 e posterior, os pacotes do SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para conectar-se aos dados de ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *fazer* new ou recentemente atualizou artigos


- [Novo + atualizado (1 + 3):&nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (0 + 1):&nbsp; **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 1):&nbsp; **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 1):&nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (12 + 1): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (6 + 2):&nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (15 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (2 + 9):&nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (1 + 0):&nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 1):&nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (1 + 1):&nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2):&nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Entidade áreas que fazer *não* qualquer novo ou recentemente atualizou artigos


- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): **ActiveX Data Objects (ADO) para o SQL** documentos](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)


