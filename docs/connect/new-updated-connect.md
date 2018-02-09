---
title: Atualizado - conectar-se com documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para conectar-se ao Microsoft SQL Server."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: cc4eb05dc4dcd74623c8ce7dfa7b7842449d79b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>Novos e atualizados recentemente: conectar-se ao SQL Server



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-12-03** &nbsp; - para - &nbsp; **2018-02-03**
- *Área de assunto:* &nbsp; **conectar ao SQL Server**.




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

1. [Use sempre criptografado com o Driver ODBC para SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1. &nbsp;[Usando sempre criptografado com o Driver ODBC para SQL Server](odbc/using-always-encrypted-with-the-odbc-driver.md)

*Atualizado em: 2018-01-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 524.  ms.author= "v-chojas".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a52abae2a8f27c3b5bc411ef758610116a608f9f 352368eb269b98ab5ca3a9791fae2e70bf26277a  (PR=4686  ,  Filename=using-always-encrypted-with-the-odbc-driver.md  ,  Dirpath=docs\connect\odbc\  ,  MergeCommitSha40=82c9868b5bf95e5b0c68137ba434ddd37fc61072) -->



**Recuperar dados em partes com SQLGetData**

Antes de 17 do Driver ODBC para SQL Server, criptografada colunas binárias e caractere não podem ser recuperadas em partes com SQLGetData. Pode ser feita apenas uma chamada SQLGetData com um buffer de tamanho suficiente para conter os dados da coluna inteira.

**Enviar dados em partes com SQLPutData**

Não não possível enviar dados para uma comparação ou inserção em partes com SQLPutData. Pode ser feita apenas uma chamada para SQLPutData com um buffer que contém todos os dados. Para inserir dados longos em colunas criptografadas, use a API de cópia em massa, descrito na próxima seção, com um arquivo de dados de entrada.

**Smallmoney e dinheiro criptografado**

Criptografado **money** ou **smallmoney** colunas não podem ser direcionadas por parâmetros, porque não há não específica de tipo de dados ODBC que é mapeado para esses tipos, resultando em erros de tipo de operando podem conflitar.

**Cópia em massa de colunas criptografadas**


Usar o [funções de cópia em massa de SQL](odbc/../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) e **bcp** utilitário é suportado com o sempre criptografado desde 17 de Driver ODBC para SQL Server. Texto sem formatação (inserção criptografada no e descriptografados em recuperação) e o texto cifrado (transferidos textualmente) podem ser inseridos e recuperados usando a cópia em massa (bcp_ *) APIs e **bcp** utilitário.

- Para recuperar o texto cifrado no formulário varbinary (max) (por exemplo, para o carregamento em massa no outro banco de dados), conecte-se sem o `ColumnEncryption` opção (ou defina-a como `Disabled`) e executar uma operação BCP OUT.

- Para inserir e recuperar o texto sem formatação e permitir que o driver transparentemente executar criptografia e descriptografia como configuração necessária, `ColumnEncryption` para `Enabled` é suficiente. Caso contrário, a funcionalidade da API BCP permanece inalterada.

- Para inserir texto cifrado no formulário varbinary (max) (por exemplo, como aqueles recuperados acima), configure o `BCPMODIFYENCRYPTED` opção como TRUE e executar uma operação BCP IN. Em ordem para os dados resultantes ser decryptable, certifique-se de que o destino CEK da coluna é o mesmo do qual o texto cifrado foi originalmente obtido.







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


