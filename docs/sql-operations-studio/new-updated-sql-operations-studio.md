---
title: Atualizado - operações de SQL Studio documentos | Microsoft Docs
description: Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para operações de SQL Studio.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssops
ms.date: 04/28/2018
ms.openlocfilehash: 074ed6176480655d9d87a55eb87cbb76b3011b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32686516"
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>Novos e recentemente atualizado: documentos de operações de SQL Studio



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2018-02-03** &nbsp; - para - &nbsp; **2018-04-28**
- *Área de assunto:* &nbsp; **Studio de operações SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


- [Estender a funcionalidade de operações do SQL Studio (visualização)](extensions.md)

<!-- GeneMi:  I MANUALLY replace the ugly !INCLUDE with the name from inside the includes file. -->


&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Baixe e instale o Studio de operações do SQL (visualização)](#TitleNum_1)
2. [Notas de versão do SQL Studio de operações (visualização)](#TitleNum_2)
3. [Tutorial: Adicionar o *cinco consultas mais lentas* widget de exemplo para o painel de banco de dados](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1. &nbsp; [Baixe e instale o Studio de operações do SQL (visualização)](download.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6b4f80ad54c599e4354303a736f62e9715f99a32 18b22f464bbd8676348248ba5717b71acbab1c0d  (PR=5676  ,  Filename=download.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



   **Instalação Debian:**
```
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
```

   **rpm instalação:**
```
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
```

   **gz instalação:**



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2. &nbsp; [Notas de versão do SQL Studio de operações (visualização)](release-notes.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[Baixar a visualização de abril público]**


**De 2018 de abril (visualização pública de abril)**


Data de lançamento: versão 25 de abril de 2018: 0.28.6

O *visualização pública abril* contém correções e aprimoramentos.

- Melhorias para a extensão de visualização do agente SQL.
- Maior suporte a arquivos grandes e protegido para salvar Admin protegido e > 256 milhões de arquivos no Studio de operações do SQL.
- Integrado a divisão de Terminal para trabalhar com vários terminais abertos ao mesmo tempo.
- Imprimir pé de contagem de arquivos no disco reduzido de instalação para instalações mais rápidas e tempos de inicialização.
- Continue corrigir problemas do GitHub:
   - Corrigir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): quando o Visualizador gráfico gera um erro, ocorrerá um comportamento inesperado.
   - Corrigir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitação de recurso: opção para grupos de servidor a ser expandido por padrão.
   - Corrigir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - sugestão incorreta para o comando 'Atualizar'.
   - Corrigir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): espera que o plano de consulta quando seleciona showplan XML na grade de resultados.
   - Corrigir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): Adicionar colchetes para chamada ms_foreachdb de flyfishingdba.
   - Corrigir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): erro de handshake de PRÉ-LOGON SSL/TLS.
   - Corrigir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): Exibir insights criptografado antes de mostrar o erro.
   - Corrigir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): novas ações de consulta no Gerenciador de widget e restauração são interrompidas.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3. &nbsp; [Tutorial: Adicionar o *cinco consultas mais lentas* widget de exemplo para o painel de banco de dados](tutorial-qds-sql-server.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2))

<!-- Source markdown line 94.  ms.author= "erickang".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bc128acd966898cafc04381d7d83187d28466052 a47bf93ea4165618e0e514d7900ce1461f691aae  (PR=5676  ,  Filename=tutorial-qds-sql-server.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente

- [Novo + atualizado (11 + 6): &nbsp; &nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (18 + 0): &nbsp; &nbsp; **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (218 + 14): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (14 + 0): &nbsp; &nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (3 + 2): &nbsp; &nbsp; **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (3 + 3): &nbsp; &nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (7 + 10): &nbsp; &nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 3): &nbsp; &nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **Tools para SQL** documentos](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)

