---
title: Atualizado - documentos de bancos de dados relacionais | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para bancos de dados relacionais."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 06/30/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 19b664245f45ad45a4c7d1eba249858030fad718
ms.contentlocale: pt-br
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-relational-databases-docs" class="xliff"></a>

# Novos e recentemente atualizado: documentos de bancos de dados relacionais



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **17-05-2017** &nbsp; até &nbsp; **30-06-2017**
- *Área de assunto:* &nbsp; **bancos de dados relacionais**.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Visão geral interna do OLTP na memória do SQL Server para SQL Server 2016](in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016.md)
2. [Processamento de consultas adaptável em bancos de dados SQL](performance/adaptive-query-processing.md)
3. [Guide to enhancing privacy and addressing GDPR requirements with the Microsoft SQL platform](security/microsoft-sql-and-the-gdpr-requirements.md) (Guia para aprimorar a privacidade e atender aos requisitos com a plataforma Microsoft SQL)
4. [sys.dm_db_log_stats (Transact-SQL)](system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)
5. [sys.dm_exec_query_parallel_workers (Transact-SQL)](system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-altering-memory-optimized-tablesin-memory-oltpaltering-memory-optimized-tablesmd" class="xliff"></a>

### 1. &nbsp;[Alterando tabelas com otimização de memória](in-memory-oltp/altering-memory-optimized-tables.md)

*Atualizado: 23-06-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Próximo](#TitleNum_2))

<!-- Source markdown line 82.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8359700b5db24838f1bb273526794c2865bbbe11 41d77cf0bbcf53a1b64d6524a24e5736c5a073da  (PR=2171  ,  Filename=altering-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**Registro em log de ALTER TABLE em tabelas com otimização de memória**

Em uma tabela com otimização de memória, a maioria dos cenários de ALTER TABLE agora é executada em paralelo e resulta em uma otimização das gravações no log de transações. A otimização é obtida apenas registrando as alterações de metadados no log de transações. No entanto, as operações de ALTER TABLE a seguir são executadas em thread único e não têm otimização de log.

A operação single-threaded, nesse caso, registraria todo o conteúdo da tabela alterada no log de transações. A seguir, a lista das operações de thread único:

- Alterar ou adicionar uma coluna para usar um tipo de objeto grande (LOB): nvarchar(max), varchar(max) ou varbinary(max).

- Adicionar ou remover um índice COLUMNSTORE.

- Praticamente qualquer coisa que afeta um [off-row column--../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).

    - Fazer com que uma coluna na linha mova-se para fora de linha.

    - Fazer com que uma coluna fora de linha mova-se para dentro da linha.

    - Crie uma nova coluna fora de linha.

    - *Exceção:* o aumento de uma coluna já fora de linha é registrado de forma otimizada. 
  




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

<a id="2-nbsp-table-and-row-size-in-memory-optimized-tablesin-memory-oltptable-and-row-size-in-memory-optimized-tablesmd" class="xliff"></a>

### 2. &nbsp;[Tamanho da tabela e da linha em tabelas com otimização de memória](in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)

*Atualizado: 22-06-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_1) | [Avançar](#TitleNum_3))

<!-- Source markdown line 114.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 27ce0fa2e7bb464f9c3d6e32dd195de3b79abfcd 0a3cacd86024e2b734704ffd37e55ca0b17a0c94  (PR=2163  ,  Filename=table-and-row-size-in-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=fe6de2b16b9792a5399b1c014af72a2a5ee52377) -->



 
  
 O cálculo do [tamanho do corpo da linha] é abordado na tabela a seguir.  
  
 Há dois cálculos diferentes para o tamanho do corpo da linha: tamanho calculado e o tamanho real:  
  
-   O tamanho calculado, marcado com [tamanho do corpo da linha calculado], é usado para determinar se a limitação do tamanho da linha de 8.060 bytes foi excedida.  
  
-   O tamanho real, marcado com [tamanho do corpo da linha real], é o tamanho real do armazenamento do corpo da linha na memória e nos arquivos de ponto de verificação.  
  
 O [tamanho do corpo da linha calculado] e o [tamanho do corpo da linha real] são calculados de modo semelhante. A única diferença é o cálculo do tamanho das colunas (n)varchar(i) e varbinary(i), como refletido na parte inferior da tabela seguinte. O tamanho do corpo da linha calculado usa o tamanho declarado *i* como o tamanho da coluna, enquanto o tamanho do corpo da linha real usa o tamanho real dos dados.  
  
 A tabela a seguir descreve o cálculo do tamanho do corpo da linha, fornecido como [tamanho do corpo real da linha] = SUM([tamanho de tipos rasos]) + 2 + 2 * [número de colunas de tipo profundo].  
  
|Seção|Tamanho|Comentários|  
|-------------|----------|--------------|  
|Colunas do tipo superficial|SUM([tamanho dos tipos superficiais]). O tamanho dos tipos individuais em bytes é o seguinte:<br /><br /> **Bit**: 1<br /><br /> **Tinyint**: 1<br /><br /> **Smallint**: 2<br /><br /> **Int**: 4<br /><br /> **Real**: 4<br /><br /> **Smalldatetime**: 4<br /><br /> **Smallmoney**: 4<br /><br /> **Bigint**: 8<br /><br /> **Datetime**: 8<br /><br /> **Datetime2**: 8<br /><br /> **Float**: 8<br /><br /> **Money**: 8<br /><br /> **Numeric** (precisão < = 18): 8<br /><br /> **Time**: 8<br /><br /> **Numeric** (precisão > 18): 16<br /><br /> **Uniqueidentifier**: 16||  
|Preenchimento da coluna superficial|Os valores possíveis são:<br /><br /> 1 se houver colunas do tipo profundas e o tamanho total dos dados das colunas superficiais for como um número ímpar.<br /><br /> Caso contrário, será 0|Os tipos profundos são os tipos (var)binary e (n)(var)char.|  




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

<a id="3-nbsp-post-migration-validation-and-optimization-guidepost-migration-validation-and-optimization-guidemd" class="xliff"></a>

### 3. &nbsp;[Validação após a migração e guia de otimização](post-migration-validation-and-optimization-guide.md)

*Atualizado: 21-06-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_2) | [Avançar](#TitleNum_4))

<!-- Source markdown line 27.  ms.author= "harinid".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 faa2e3dd8be3aeb475bf8c7f71617ebf17969892 f2760dfecda10baeb121929b72a4d8164e81185b  (PR=2126  ,  Filename=post-migration-validation-and-optimization-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=dcbeda6b8372b358b6497f78d6139cad91c8097c) -->



Abaixo estão alguns dos cenários de desempenho comuns encontrados após a migração para a plataforma [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] e como resolvê-los. Estão inclusos cenários que são específicos da migração do [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] para o [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] (versões mais antigas para versões mais recentes), bem como a migração da plataforma externa (como, Oracle, DB2, MySQL e Sybase) para o [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)].

**<a name="CEUpgrade"></a> Regressões de consulta devido à alteração na versão CE**


**Aplica-se a:** migração de [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)].

Ao migrar de versões mais antigas do [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] para o [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] ou mais recente e atualizar o [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para o mais recente, uma carga de trabalho pode ser exposta ao risco de regressão de desempenho.

Isso ocorre porque a partir [!INCLUDE[ssSQL14--../includes/sssql14-md.md)], todas as alterações do otimizador de consulta são associadas à versão mais recente [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md), portanto, os planos não são alterados diretamente no ponto de atualização, mas sim quando um usuário altera a opção de banco de dados `COMPATIBILITY_LEVEL` para o mais recente. Esse recurso, em combinação com o Repositório de Consultas, fornece um excelente nível de controle sobre o desempenho da consulta no processo de atualização. 

Para obter mais informações sobre as alterações do Otimizador de Consulta introduzidas no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], consulte [Otimizando seus planos de consulta com o estimador de cardinalidade do SQL Server 2014](http://msdn.microsoft.com/library/dn673537.aspx).




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

<a id="4-nbsp-sysquerystoreplan-transact-sqlsystem-catalog-viewssys-query-store-plan-transact-sqlmd" class="xliff"></a>

### 4. &nbsp; [sys.query_store_plan (Transact-SQL)](system-catalog-views/sys-query-store-plan-transact-sql.md)

*Atualizado: 05-06-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Anterior](#TitleNum_3) | [Avançar](#TitleNum_5))

<!-- Source markdown line 58.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1b77e34309ba7033578b3c82ed83c8c2fbc93e24 ce4ade9ab906c35cb87068a1fb91c4e1d7549aac  (PR=1940  ,  Filename=sys-query-store-plan-transact-sql.md  ,  Dirpath=docs\relational-databases\system-catalog-views\  ,  MergeCommitSha40=1d363db8e8bd0e1460cdea3c3a7add68e48714c9) -->



**Limitações forçadas do plano**

O Repositório de Consultas tem um mecanismo para forçar o otimizador de consulta a usar um determinado plano de execução. No entanto, existem algumas limitações que podem impedir que um plano seja forçado. 

Primeiro, se o plano contém as seguintes construções:
* Instrução insert bulk.
* Instrução insert bulk.
* Referência a uma tabela externa
* Consulta distribuída ou operações de texto completo
* Uso de consultas globais 
* Cursores
* Especificação de junção em estrela inválida 

Segundo, quando os objetos dos quais o plano depende, não estão mais disponíveis:
* Banco de dados (se o banco de dados no qual o plano se originou não existe mais)
* Índice (não existe mais ou está desabilitado)

Por fim, problemas com o próprio plano:
* Não é válido para consulta
* O otimizador de consulta excedeu o número de operações permitidas
* XML do plano formatado incorretamente




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

<a id="5-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd" class="xliff"></a>

### 5. &nbsp;[Gerenciar a retenção de dados históricos em tabelas temporais com versão do sistema](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_4))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b  (PR=1777  ,  Filename=manage-retention-of-historical-data-in-system-versioned-temporal-tables.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



**Usando a abordagem de política de retenção de histórico Temporal**

> **Observação:** usando a política de retenção de histórico Temporal abordagem aplica-se a [! INCLUIR [sqldbesa-... /.. /Includes/sqldbesa-MD.MD]) e a partir do CTP 1.3 de 2017 do SQL Server.  

Retenção de histórico temporal pode ser configurado no nível de tabela individuais, que permite aos usuários criar vencimento flexível políticas. A aplicação de retenção temporal é simple: requer apenas um parâmetro a ser definido durante a alteração de esquema ou criação de tabela.

Depois de definir a política de retenção, o banco de dados do SQL Azure inicia verificando regularmente se há linhas de histórico que são qualificadas para a limpeza automática de dados. Identificação de linhas correspondentes e sua remoção da tabela de histórico ocorrem de modo transparente, na tarefa em segundo plano que é programada e executada pelo sistema. Condição de idade para as linhas da tabela de histórico é verificada com base na coluna que representa o final do período SYSTEM_TIME. Se o período de retenção, por exemplo, é definido como seis meses, linhas de tabela qualificadas para limpeza atendem a seguinte condição:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
No exemplo anterior, supomos que a coluna de ValidTo corresponde ao final do período SYSTEM_TIME.
**Como configurar a política de retenção?**

Antes de configurar a política de retenção para uma tabela temporal, verifique primeiro se a retenção de histórico temporal está habilitada no nível do banco de dados:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
Sinalizador de banco de dados **is_temporal_history_retention_enabled** é definida como ON, por padrão, mas os usuários podem alterá-lo com a instrução ALTER DATABASE. Automaticamente, ela é definida como OFF após ponto na operação de restauração do tempo. Para ativar a limpeza de retenção de histórico temporal para seu banco de dados, execute a seguinte instrução:





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção anterior.

1. [Alterando tabelas com otimização de memória](#TitleNum_1)
2. [Tamanho da tabela e da linha em tabelas com otimização de memória](#TitleNum_2)
3. [Validação após a migração e guia de otimização](#TitleNum_3)
4. [sys.query_store_plan (Transact-SQL)](#TitleNum_4)
5. [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](#TitleNum_5)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## Artigos irmã

Esta seção lista os artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.com: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (12 + 2): documentos de **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 2): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + atualizado (3 + 0): documentos do **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (1 + 2): documentos do **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (2 + 8): documentos do **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + atualizado (1 + 0): documentos do **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (5 + 5): documentos de **Bancos de dados relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (2 + 0): documentos do **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 4): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + atualizado (1 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): documentos do **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


&nbsp;


