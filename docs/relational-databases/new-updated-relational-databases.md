---
title: "Atualizado — Documentos de bancos de dados relacionais | Microsoft Docs"
description: "Exibir trechos de conteúdo atualizado para documentação de Bancos de Dados Relacionais alterada recentemente."
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
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Novos e recém-atualizados: documentos de Bancos de Dados Relacionais



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de assunto:* &nbsp; **Bancos de dados relacionais**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Usar o Profiler SSMS XEvent](extended-events/use-the-ssms-xe-profiler.md)
2. [Assistente Importar Arquivo Simples para SQL](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Banco de dados tempdb](#TitleNum_1)
2. [Guia de arquitetura de gerenciamento de memória](#TitleNum_2)
3. [Estatísticas](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1. &nbsp;[Banco de dados tempdb](databases/tempdb-database.md)

*Atualizado: 20-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**Otimizando o desempenho de tempdb**

 O tamanho e o posicionamento físico do banco de dados tempdb podem afetar o desempenho de um sistema. Por exemplo, se o tamanho definido para tempdb for muito pequeno, parte da carga de processamento do sistema poderá ser elevada com o crescimento automático de tempdb para o tamanho necessário para dar suporte à carga de trabalho sempre que você reiniciar a instância do ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)].

 Se possível, use [inicialização de arquivo instantâneo do banco de dados--../../relational-databases/databases/database-instant-file-initialization.md) para melhorar o desempenho das operações de crescimento de arquivo de dados.

 Aloque espaço antecipadamente para todos os arquivos do tempdb definindo o tamanho de arquivo com um valor grande o bastante para acomodar a carga de trabalho comum no ambiente. Isso impede que o tempdb seja expandido muito frequentemente, o que pode afetar o desempenho. O banco de dados tempdb deve ser definido como crescimento automático, mas isso deve ser usado para aumentar o espaço em disco para exceções não planejadas.

 Arquivos de dados devem ser de tamanho igual em cada [grupo de arquivos--../../relational-databases/databases/database-files-and-filegroups.md#filegroups), as ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] usa um algoritmo de preenchimento proporcional que favorece alocações em arquivos com mais espaço livre. A divisão do tempdb em vários arquivos de dados de tamanho igual fornece um alto grau de eficiência paralela em operações que usam o tempdb.

 Defina o incremento de crescimento do arquivo com um tamanho razoável para evitar que os arquivos do banco de dados tempdb cresçam com um valor muito pequeno. Se o crescimento do arquivo for muito pequeno, comparado à quantidade de dados que está sendo gravada no tempdb, o tempdb talvez tenha que se expandir constantemente. Isso afetará o desempenho.

 Para verificar o tamanho atual do tempdb e os parâmetros de crescimento, use a seguinte consulta:
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2. &nbsp; [Guia de arquitetura de gerenciamento de memória](memory-management-architecture-guide.md)

*Atualizado: 28-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Próximo](#TitleNum_3))

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



Em versões anteriores do SQL Server (..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)], ..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] e ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)]), a alocação de memória era feita usando cinco mecanismos diferentes:
-  **O alocador de página única (SPA)**, incluindo somente as alocações de memória que foram menores ou iguais a 8 KB no processo ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]. As opções de configuração *max server memory (MB)* e *min server memory (MB)* determinavam os limites de memória física que o SPA consumia. O pool de buffers era simultaneamente o mecanismo do SPA e o maior consumidor de alocações de uma página.
-  O **Alocador de várias páginas (MPA)**, para as alocações de memória que solicitam mais de 8 KB.
-  O **Alocador de CLR**, incluindo os heaps SQL CLR e suas alocações globais que são criadas durante a inicialização do CLR.
-  As alocações de memória para **[pilhas de thread--../relational-databases/memory-management-architecture-guide.md#stacksizes)** no processo ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)].
-  As **DWA (Alocações Diretas do Windows)**, para as solicitações de alocação de memória feitas diretamente no Windows. Isso inclui o uso de heap do Windows e alocações virtuais diretas feitas pelos módulos que são carregados no processo ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]. Exemplos de tais solicitações de alocação de memória incluem as alocações de DLLs de procedimento armazenado estendido, os objetos que são criados usando procedimentos de automação (chamadas sp_OA) e as alocações de provedores de servidor vinculados.

Do  ..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)] em diante, as alocações de uma página, as alocações de várias páginas e as alocações de CLR são consolidadas em um Alocador de Páginas de **"qualquer tamanho"** e ele é incluído nos limites de memória que são controlados pelas opções de configuração *memória máx. do servidor (MB)* e *memória mín. do servidor (MB)*. Esta alteração oferecia uma capacidade de dimensionamento mais precisa para todos os requisitos de memória que passam pelo gerenciador de memória ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)].



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3. &nbsp; [Estatísticas](statistics/statistics.md)

*Atualizado: 27-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Próximo](#TitleNum_4))

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> Histogramas em ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] são criados somente para uma única colunaΓÇöa primeira coluna no conjunto de colunas de chave do objeto de estatísticas.

Para criar o histograma, o otimizador de consulta classifica os valores de colunas, calcula o número de valores que correspondem a cada valor de coluna distinta e agrega os valores de colunas em um máximo de 200 etapas de histograma contíguas. Cada etapa do histograma inclui uma gama de valores de coluna seguidos por um valor de coluna de limite superior. O intervalo inclui todos os possíveis valores de coluna entre valores de limite, excluindo-se os próprios valores de limite em si. O mais baixo dos valores de coluna classificados é o valor do limite superior da primeira etapa do histograma.

Mais detalhadamente, ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] cria o **histograma** do conjunto classificado de valores de coluna em três etapas:

- **Inicialização do histograma**: na primeira etapa, uma sequência de valores que começa no início do conjunto classificado é processada e até 200 valores de *range_high_key*, *equal_rows*, *range_rows* e *distinct_range_rows* são coletados (*range_rows* e *distinct_range_rows* são sempre zero durante essa etapa). A primeira etapa termina quando toda a entrada foi esgotada ou quando 200 valores foram encontrados.
- **Examinar com a mesclagem de bucket**: cada valor adicional da coluna inicial da chave de estatísticas é processado na segunda etapa, na ordem classificada; cada valor sucessivo é adicionado ao último intervalo ou um novo intervalo no final é criado (isso é possível porque os valores de entrada são classificados). Se um novo intervalo for criado, um par dos intervalos vizinhos existentes será recolhido em um único intervalo. Esse par de intervalos é selecionado para minimizar a perda de informações. Esse método usa um algoritmo de *diferença máxima* para minimizar o número de etapas no histograma enquanto maximiza a diferença entre os valores de limite. O número de etapas após o recolhimento dos intervalos permanece em 200 durante toda esta etapa.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4. &nbsp; [sp_server_diagnostics (Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

*Atualizado: 21-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_3))

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



A consulta de exemplo abaixo lê a saída de resumo da tabela:
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

A consulta de exemplo abaixo lê algumas das saídas detalhadas de cada componente na tabela:
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







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


