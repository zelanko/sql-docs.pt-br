---
title: Atualizado - conectar-se com documentos do SQL Server | Microsoft Docs
description: Exiba trechos do conteúdo atualizado com alterações recentes na documentação "Conectar-se ao Microsoft SQL Server".
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: da7ff58d5930acb084220c8d0364147ae93ed963
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>Novos e atualizados recentemente: conectar-se ao SQL Server



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-12-2017** &nbsp; até &nbsp; **03-02-2018**
- *Área de assunto:* &nbsp; **conectar ao SQL Server**.




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

1. [Usando o recurso Always Encrypted com o Microsoft ODBC Driver for SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1. &nbsp; [Usando o recurso Always Encrypted com o Microsoft ODBC Driver for SQL Server](odbc/using-always-encrypted-with-the-odbc-driver.md)

*Atualizado em: 22-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

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


